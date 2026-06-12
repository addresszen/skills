---
name: addresszen-react
description: |
  Use this skill whenever the user wants address autocomplete in a React or
  Next.js application, address suggestions as the user types in a React form,
  React address validation, US or international address lookup in JSX, or any
  React component that should auto-populate fields from a selected address —
  even if they don't name the package. Covers `@addresszen/react`: install, the
  `<AddressLookup>` component (default and wrap-around-your-own-input modes),
  callbacks, CSS, country filter/bias, and the React-specific gotchas
  (`"use client"` for Next.js App Router, CSS import path, callbacks always
  see latest closure). For the underlying vanilla JS library and the full
  option reference, see the AddressZen Address Lookup docs at
  https://docs.addresszen.com/docs/address-lookup — the option surface is
  identical except for DOM-coupled options.
license: SEE LICENSE IN LICENSE
metadata:
  author: addresszen
  version: "0.1.0"
  homepage: https://addresszen.com
  source: https://github.com/addresszen/skills
inputs:
  - name: ADDRESSZEN_API_KEY
    description: API key for the AddressZen API. Get one at addresszen.com
    required: true
---

# Address Lookup for React

React component for the AddressZen address autocomplete widget. Thin wrapper around the vanilla [`@addresszen/address-lookup`](https://docs.addresszen.com/docs/address-lookup) library — same callbacks, same behavioural options, React-idiomatic surface. Defaults to US addresses.

## Quick Start (default mode — component renders its own input)

```bash
npm install @addresszen/react
```

`react` and `react-dom` (`^18` or `^19`) are peer dependencies. The package depends on `@addresszen/address-lookup` internally; you don't need to install it separately.

```tsx
"use client";

import { useState } from "react";
import { AddressLookup } from "@addresszen/react";
import "@addresszen/react/css/address-lookup.min.css";

export default function CheckoutForm() {
  const [address, setAddress] = useState<Record<string, string>>({});

  return (
    <form>
      <AddressLookup
        apiKey="ak_..."
        placeholder="Start typing your address"
        onAddressRetrieved={(a) => setAddress(a)}
      />
      <input value={address.line_1 ?? ""} readOnly />
      <input value={address.city ?? ""} readOnly />
      <input value={address.state ?? ""} readOnly />
      <input value={address.zip_plus_4_code ?? ""} readOnly />
    </form>
  );
}
```

The selected address arrives in `onAddressRetrieved` — caller owns the form fields and updates them via React state. This is intentionally different from the legacy `outputFields` pattern (see "What's different from the vanilla library" below).

## Wrap Mode (caller supplies the input)

Pass an `<input>` (or any component that renders one and accepts a ref) as children — `<AddressLookup>` wraps it instead of rendering its own. Use this when you already have a themed/styled input from your design system.

```tsx
<AddressLookup apiKey="ak_..." onAddressRetrieved={(a) => setAddress(a)}>
  <input
    className="bg-white border rounded px-3 py-2 w-full"
    placeholder="Search address"
  />
</AddressLookup>
```

Works with shadcn `<Input>`, MUI `<TextField>` (via `inputProps`/`InputProps`), Mantine `<TextInput>`, etc. — anything that forwards refs to its underlying `<input>`.

## API

### `<AddressLookup>` props

- **`apiKey`** *(required)* — API key from your AddressZen account.
- **`children`** *(optional)* — single React element. When present, wraps that element instead of rendering a default input.
- **`inputRef`** — ref forwarded to the rendered `<input>`. Ignored when `children` is provided (put your ref on the child instead).
- **All callbacks** from the underlying `ControllerOptions`: `onAddressRetrieved`, `onAddressSelected`, `onSearchError`, `onSuggestionError`, `onSuggestionsRetrieved`, `onLoaded`, `onFailedCheck`, `onCountrySelected`, `onContextChange`, `onOpen`, `onClose`, `onFocus`, `onBlur`, `onInput`, `onKeyDown`, `onMouseDown`, `onSelect`, `onMounted`, `onRemove`, `onAddressPopulated`.
- **Behavioural options**: `defaultCountry`, `restrictCountries`, `queryOptions`, `resolveOptions`, `removeOrganisation`, `titleizePostTown`, `checkKey`, `format`, `hideToolbar`, `detectCountry`, `injectStyle`, `populateCounty`, `populateOrganisation`, `alignToInput`, `offset`, `fixed`, `aria`, and all `msg*` / `*Class` strings. These map 1:1 to the vanilla `ControllerOptions` — see the [Address Lookup docs](https://docs.addresszen.com/docs/address-lookup) for full descriptions.
- **HTML input props** (default mode only): `id`, `name`, `className`, `placeholder`, `disabled`, `required`, `aria-label`, `aria-describedby`, `aria-labelledby`.

## What's different from the vanilla library

The React component drops legacy DOM-coupling options. React owns the DOM; the caller renders form fields and reads results from callbacks.

| Vanilla option         | React equivalent                                               |
| ---------------------- | -------------------------------------------------------------- |
| `inputField`           | the rendered `<input>` (or `children` in wrap mode)            |
| `outputFields`         | subscribe to `onAddressRetrieved`, update React state          |
| `hide` / `unhide`      | render output fields conditionally in JSX                      |
| `scope`                | the React subtree itself                                       |
| `inputStyle` / `listStyle` / `mainStyle` / `containerStyle` / `liStyle` | use `className` or override the bundled CSS variables |
| `injectStyle: false` + manual CSS link | `injectStyle={false}` + `import "@addresszen/react/css/address-lookup.min.css"` |

Everything else carries across unchanged.

## Critical Gotchas

- **Next.js App Router needs `"use client"`.** The component uses `useEffect` and DOM refs — it must run client-side. Either add `"use client"` to your page/component file, or import `<AddressLookup>` from a wrapper file that has the directive. Without it you'll get "useEffect is not a function" or "Cannot read properties of null" at build time.

- **CSS doesn't load automatically when bundled.** `injectStyle` defaults to `true`, which injects the stylesheet at runtime — works in plain React apps. For SSR/Next.js where you want CSS in the initial HTML, set `injectStyle={false}` and `import "@addresszen/react/css/address-lookup.min.css"` at app root. Pick one approach; don't do both or you'll get duplicate styles.

- **Callbacks always see the latest closure — don't reach for `useCallback`.** The component stashes the latest props in a ref every render, so `onAddressRetrieved={() => setX(latestState)}` works even when `latestState` updates. Wrapping in `useCallback` is unnecessary and can actually hurt (stale closures if you forget a dep). Just write inline callbacks.

- **`apiKey` is required as a prop.** There's no Provider in v0 — pass `apiKey` directly to every `<AddressLookup>`. Hooks and a Provider may land later; for now, prop or `process.env.NEXT_PUBLIC_ADDRESSZEN_KEY`-style env var.

- **`apiKey` is camelCase**, not `api_key` or `API_KEY`. Same convention as the vanilla library.

- **Defaults to US addresses.** No `defaultCountry` needed for the common US case. Set `defaultCountry="GBR"` (or another ISO code) to start elsewhere, and `restrictCountries={[...]}` to limit the picker.

- **Wrap mode requires exactly one child element.** Multiple children, text, or `null` children will throw. The child must render an `<input>` and accept a ref — most styled-input components do this via `React.forwardRef`.

- **The widget reparents the input on mount.** When the widget attaches, it wraps your `<input>` in an autocomplete container. React still owns the input element (same node reference), but if you're querying the parent in tests or styling based on direct-child selectors, account for the wrapper.

- **API key allowed URLs.** Frontend keys are restricted by domain. If requests fail with 403, check your key's allowed URL list in your AddressZen account — match scheme + host (e.g. `https://example.com`, no trailing slash, no path). For local development add `http://localhost:3000` (or your port).

- **StrictMode double-mount is handled.** The component cleans up on unmount and re-attaches on remount — no leaks, no double-attached widgets. You don't need to disable StrictMode.

## Reading the result

`onAddressRetrieved` receives an address object. The shape depends on the country. For US addresses (the default), the useful fields are:

```ts
{
  line_1: string;            // "20 W 34th St"
  line_2: string;            // ""
  city: string;              // "New York"
  state: string;             // "NY"
  zip_plus_4_code: string;   // "10001-2402"
  country: string;           // "United States"
  // ...plus more — see API docs
}
```

For UK addresses (`defaultCountry="GBR"`), the shape uses `post_town`, `postcode`, `county`, etc. See the [Address Lookup docs](https://docs.addresszen.com/docs/address-lookup) for the full per-country field reference.

## Country handling

Same options as the vanilla library. Most useful:

```tsx
<AddressLookup
  apiKey="ak_..."
  defaultCountry="USA"                       // start here (default)
  restrictCountries={["USA", "GBR", "CAN"]}  // limit the picker
  detectCountry={false}                      // disable IP geolocation auto-detect
  hideToolbar                                // remove the country-switcher UI
  onAddressRetrieved={...}
/>
```

See the [Address Lookup docs](https://docs.addresszen.com/docs/address-lookup) for the full set of country options — they all work as React props.

## Server Components and Streaming

The component is **client-only** — it uses DOM APIs (`useEffect`, refs, mutation) and can't render on the server. Strategies:

- **Next.js App Router**: mark the file `"use client"`. The component will be sent to the client and hydrate there.
- **Next.js Pages Router**: works out of the box (everything is client-rendered after hydration).
- **Remix**: import inside a client-only component or use `<ClientOnly>` from `remix-utils`.
- **Astro**: use `client:load` directive on the React island.

## When `<AddressLookup>` isn't enough

If you need a fully custom UI (your own dropdown, your own suggestion rendering), the hooks layer (`useAutocomplete`, `useResolveAddress`) is on the roadmap but not shipped yet. For now: either use the wrap-mode child slot to insert your themed input, or drop down to `@addresszen/address-lookup` directly.

## Linking out

- Live docs and full option reference: [docs.addresszen.com/docs/address-lookup](https://docs.addresszen.com/docs/address-lookup)
- React integration page: [docs.addresszen.com/docs/address-lookup/react](https://docs.addresszen.com/docs/address-lookup/react)
- API docs: [docs.addresszen.com](https://docs.addresszen.com)
