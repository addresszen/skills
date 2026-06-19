# Add to your React Application

[`@addresszen/react`](https://www.npmjs.com/package/@addresszen/react) is the official React integration for Address Lookup. It renders an `<input>`, attaches the widget, and hands selected addresses back through callbacks - no `useEffect` or `useRef` wiring required.

## Install

```bash
npm install @addresszen/react
```

`react` and `react-dom` (`^18` or `^19`) are peer dependencies. The package depends on `@addresszen/address-lookup` internally; you don't need to install it separately.

## Quick Start

The default mode renders its own input. Pass an `apiKey` and capture the selected address via `onAddressRetrieved`. The component defaults to US addresses, so no `defaultCountry` prop is needed for the common case.

```tsx
"use client";

import { useState } from "react";
import { AddressLookup } from "@addresszen/react";
import "@addresszen/react/css/address-lookup.min.css";

type Address = {
  line_1: string;
  line_2: string;
  city: string;
  state: string;
  zip_plus_4_code: string;
};

const empty: Address = {
  line_1: "",
  line_2: "",
  city: "",
  state: "",
  zip_plus_4_code: "",
};

export default function CheckoutForm() {
  const [address, setAddress] = useState<Address>(empty);

  return (
    <form>
      <label htmlFor="search">Search address</label>
      <AddressLookup
        id="search"
        apiKey="ak_test"
        placeholder="Start typing your address"
        onAddressRetrieved={(a) =>
          setAddress({
            line_1: a.line_1,
            line_2: a.line_2,
            city: a.city,
            state: a.state,
            zip_plus_4_code: a.zip_plus_4_code,
          })
        }
      />

      <label>Line 1<input readOnly value={address.line_1} /></label>
      <label>Line 2<input readOnly value={address.line_2} /></label>
      <label>City<input readOnly value={address.city} /></label>
      <label>State<input readOnly value={address.state} /></label>
      <label>ZIP + 4<input readOnly value={address.zip_plus_4_code} /></label>
    </form>
  );
}
```

> Replace `ak_test` with your own API key from your [account dashboard](https://account.addresszen.com/tokens).

## Wrap an Existing Input

Pass a single `<input>` (or any element that renders one and forwards a ref) as `children`. The component attaches the widget to your input rather than rendering its own - useful for design systems like shadcn/ui, MUI, or Mantine, or for any input you've already styled.

```tsx
<AddressLookup
  apiKey="ak_test"
  onAddressRetrieved={(a) => console.log(a)}
>
  <input
    className="rounded-md border px-3 py-2 w-full"
    placeholder="Search address"
  />
</AddressLookup>
```

In wrap mode, HTML props on `<AddressLookup>` (like `placeholder`, `className`) are ignored - the child owns its own props.

## Common Options

All behavioural options from the underlying controller are supported as props.

```tsx
<AddressLookup
  apiKey="ak_test"
  restrictCountries={["USA"]}
  hideToolbar={true}
  injectStyle={true}
  queryOptions={{ limit: "10" }}
  resolveOptions={{ tags: ["react-demo"] }}
  onAddressRetrieved={(a) => console.log(a)}
/>
```

- [`defaultCountry`](https://docs.addresszen.com/docs/address-lookup/default-country) - ISO country code applied on mount. Defaults to `"USA"`; set `"GBR"` to opt into UK addresses, for example.
- [`restrictCountries`](https://docs.addresszen.com/docs/address-lookup/restrict-country) - array of ISO codes to restrict the search to.
- [`hideToolbar`](https://docs.addresszen.com/docs/address-lookup/hide) - hide the country selector toolbar.
- `injectStyle` - default `true`. Auto-injects the widget stylesheet. See [CSS](#css) below.
- `queryOptions` - forwarded to the [Autocomplete API](https://docs.addresszen.com/docs/api/find-address) endpoint.
- `resolveOptions` - forwarded to the resolve endpoint (e.g. `tags` for usage attribution).
- `detectCountry` - default `true`. Set `false` to skip IP-based country detection.

The legacy DOM-coupled options (`inputField`, `outputFields`, `hide`, `unhide`, `scope`, `inputStyle`, `listStyle`, `mainStyle`, `containerStyle`, `liStyle`) are intentionally absent. React owns the DOM - render your own form fields, update them from `onAddressRetrieved`, and style with CSS classes or your component library.

## Callbacks

Every callback supported by the underlying controller is exposed as a prop. Callbacks always read the latest closure, so you can pass inline functions without `useCallback`.

The three most common:

```tsx
<AddressLookup
  apiKey="ak_test"
  onAddressRetrieved={(address) => {
    // Full address resolved from the API after the user picks a suggestion
  }}
  onAddressSelected={(suggestion) => {
    // User clicked or keyboard-selected a suggestion (before resolve)
  }}
  onSearchError={(error) => {
    // Network or API error during search
  }}
/>
```

See [Callbacks](https://docs.addresszen.com/docs/address-lookup/callbacks) for the full list and semantics (`onAddressPopulated`, `onSuggestionsRetrieved`, `onCountrySelected`, `onOpen`, `onClose`, `onFocus`, `onBlur`, `onFailedCheck`, and more).

## CSS

The widget needs its stylesheet for the suggestion dropdown to render correctly.

By default the component injects the stylesheet into `<head>` on mount:

```tsx
<AddressLookup apiKey="ak_test" />
```

To bundle the CSS yourself (recommended for production builds with stricter CSP), set `injectStyle={false}` and import the stylesheet:

```tsx
import "@addresszen/react/css/address-lookup.min.css";

<AddressLookup apiKey="ak_test" injectStyle={false} />;
```

The unminified `@addresszen/react/css/address-lookup.css` is also exported if you'd like to override variables or compose with your own build pipeline.

## Next.js

In the Next.js App Router, mark any file that uses `<AddressLookup>` as a client component:

```tsx
"use client";

import { AddressLookup } from "@addresszen/react";
```

Read the API key from an environment variable to avoid hardcoding:

```tsx
<AddressLookup
  apiKey={process.env.NEXT_PUBLIC_ADDRESSZEN_KEY!}
  onAddressRetrieved={(a) => console.log(a)}
/>
```

Pages Router and any React Server Component setup that supports client components work the same way - the widget runs purely in the browser and the component does no work during SSR.
