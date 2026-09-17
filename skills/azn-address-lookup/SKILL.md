---
name: azn-address-lookup
description: |
  Use this skill whenever the user wants address autocomplete, address
  suggestions as the user types, address validation in a form, US or
  international address lookup, or any form field that should be
  auto-populated from a selected address — even if they don't name the
  package. Specifically covers `@addresszen/address-lookup` (vanilla JS).
  Includes npm and CDN install, initialisation via `AddressLookup.setup`,
  callbacks, CSS, country filter/bias, and common gotchas (API key
  allowed-URLs, source vs CDN build, default US addresses). For the React
  wrapper, use the `azn-react` skill instead.
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
references:
  - accessibility.md
  - additional-data.md
  - behavior.md
  - bias-by-geolocation.md
  - bias-by-ip.md
  - callbacks.md
  - configuration-reference.md
  - configure.md
  - css-classes.md
  - default-country.md
  - default-styling.md
  - detach.md
  - exclude-islands.md
  - exclude-military.md
  - exclude-po-box.md
  - filter-by-geospatial-box.md
  - gate-population.md
  - hide.md
  - home.md
  - how-it-works.md
  - key-usability.md
  - messages.md
  - multiple.md
  - no-match-action.md
  - npm.md
  - nudge.md
  - populate-country-select.md
  - prevent-autofill.md
  - react.md
  - restrict-country.md
  - restrict-to-mainland-us.md
  - restrict-to-states.md
  - script.md
  - separate-input.md
  - single-field.md
  - style-tweaks.md
  - validate-before-submitting.md
---

# Address Lookup

Address autocomplete widget for the AddressZen API. Suggests addresses as the user types and populates form fields when one is selected. Defaults to US addresses.

## Quick Start (npm + bundler)

```bash
npm install @addresszen/address-lookup
```

```js
import { AddressLookup } from "@addresszen/address-lookup";

const controller = AddressLookup.setup({
  apiKey: "ak_...",
  outputFields: {
    line_1: "#line_1",
    line_2: "#line_2",
    city: "#city",
    state: "#state",
    zip_plus_4_code: "#zipcode",
  },
});
```

## Quick Start (CDN / drop-in script)

```html
<script src="https://cdn.jsdelivr.net/npm/@addresszen/address-lookup@2"></script>
<script>
  AddressZen.AddressLookup.setup({
    apiKey: "ak_...",
    outputFields: {
      line_1: "#line_1",
      line_2: "#line_2",
      city: "#city",
      state: "#state",
      zip_plus_4_code: "#zipcode",
    },
  });
</script>
```

The CDN build is a polyfilled UMD bundle exposed on the global `AddressZen.AddressLookup`.

## React

For React / Next.js, prefer the dedicated [`@addresszen/react`](https://docs.addresszen.com/docs/address-lookup/react) wrapper (its own `azn-react` skill). To drive the vanilla library from React directly, use `AddressLookup.watch` inside `useEffect` — see [`react.md`](./references/react.md).

## Critical Gotchas

- **Use `AddressLookup.setup({...})` — not `new AddressLookup(...)`.** It's a factory method, not a constructor.
- **`apiKey` is camelCase**, not `api_key` or `API_KEY`.
- **`outputFields` is required** — it maps address attributes (`line_1`, `city`, `state`, `zip_plus_4_code`, …) to your form's input selectors. Without it, the widget has nothing to populate.
- **Defaults to US addresses.** The output fields above are the US shape. For UK set `defaultCountry: "GBR"` (fields become `line_1`, `post_town`, `postcode`, `county`, …); for another country use its ISO code. See [`default-country.md`](./references/default-country.md).
- **Pin your CDN version in production.** Pulling from `@latest` will silently break when a major bumps. Use `@addresszen/address-lookup@2` (or the current major).
- **Source vs CDN build:** use `@addresszen/address-lookup` via npm for bundlers (smaller, tree-shakable). Use the jsDelivr UMD bundle (global `AddressZen.AddressLookup`) for `<script>` tags.
- **API key allowed URLs.** Frontend keys are restricted by domain. If requests fail with 403, check your key's allowed URL list in your AddressZen account — match scheme + host (e.g. `https://example.com`, no trailing slash, no path). `localhost` is allowed by default for development.
- **Styling is injected by default.** The widget injects its stylesheet into `<head>` (`injectStyle` defaults to `true`). To supply your own CSS, set `injectStyle: false` and style the widget's classes yourself. See [`default-styling.md`](./references/default-styling.md).
- **Country toolbar vs country restriction are independent.** `restrictCountries: ["USA"]` removes the country *picker control* — it does **not** hide the toolbar bar itself. For a clean single-country setup, also hide the toolbar. See [`hide.md`](./references/hide.md).

For the long tail of error patterns and fixes, see [`troubleshooting.md`](./troubleshooting.md).

## When to read which reference

The references below are organised by intent. Read only the ones relevant to the user's task — not the whole list.

### Setup and initialisation
- [`npm.md`](./references/npm.md) — npm/bundler install
- [`script.md`](./references/script.md) — CDN `<script>` tag install (global `AddressZen.AddressLookup`)
- [`configure.md`](./references/configure.md) — minimum required config (`apiKey`, `outputFields`)
- [`configuration-reference.md`](./references/configuration-reference.md) — full options reference
- [`callbacks.md`](./references/callbacks.md) — `onAddressRetrieved`, `onLoaded`, `onFailedCheck`, etc.

### React / single-page apps
- [`react.md`](./references/react.md) — `AddressLookup.watch` + `useEffect` pattern
- [`detach.md`](./references/detach.md) — detach/re-attach on route change
- [`nudge.md`](./references/nudge.md) — manual re-init / re-attach

### Country handling
- [`restrict-country.md`](./references/restrict-country.md) — limit which countries the user can pick
- [`default-country.md`](./references/default-country.md) — pre-select / bias toward a country
- [`restrict-to-mainland-us.md`](./references/restrict-to-mainland-us.md) — exclude US territories
- [`restrict-to-states.md`](./references/restrict-to-states.md) — limit to specific US states

### Filter / bias suggestions
- [`bias-by-geolocation.md`](./references/bias-by-geolocation.md) — toward a lat/lng
- [`bias-by-ip.md`](./references/bias-by-ip.md) — toward the user's IP location
- [`filter-by-geospatial-box.md`](./references/filter-by-geospatial-box.md) — within a bounding box
- [`exclude-islands.md`](./references/exclude-islands.md) — exclude island addresses
- [`exclude-military.md`](./references/exclude-military.md) — exclude military addresses
- [`exclude-po-box.md`](./references/exclude-po-box.md) — exclude PO Box addresses

### Styling and UI
- [`default-styling.md`](./references/default-styling.md) — built-in look and `injectStyle`
- [`css-classes.md`](./references/css-classes.md) — class hooks for custom CSS
- [`style-tweaks.md`](./references/style-tweaks.md) — common style overrides
- [`messages.md`](./references/messages.md) — customise UI strings

### Form layout patterns
- [`single-field.md`](./references/single-field.md) — one input that captures the whole address
- [`separate-input.md`](./references/separate-input.md) — dedicated lookup input separate from output fields
- [`multiple.md`](./references/multiple.md) — more than one lookup on the page
- [`hide.md`](./references/hide.md) — hide output fields (and the toolbar) until an address is picked
- [`no-match-action.md`](./references/no-match-action.md) — offer an out (e.g. manual entry) when a search returns no matches (`msgNoMatchAction` + `onNoMatchAction`)
- [`prevent-autofill.md`](./references/prevent-autofill.md) — disable browser autofill on the lookup input
- [`key-usability.md`](./references/key-usability.md) — keyboard navigation tweaks
- [`validate-before-submitting.md`](./references/validate-before-submitting.md) — block submit until an address is verified

### Address data
- [`additional-data.md`](./references/additional-data.md) — populate fields beyond the standard output set

### Concepts
- [`how-it-works.md`](./references/how-it-works.md) — internal model: input field, dropdown, key check
- [`behavior.md`](./references/behavior.md) — the DOM the widget renders and how it reacts
- [`home.md`](./references/home.md) — feature overview

### Troubleshooting
- [`troubleshooting.md`](./troubleshooting.md) — common errors with root cause + fix (authored sibling, not in references/)

## Full documentation

The full AddressZen documentation — every guide, API reference, and integration — is available as a single file at [llms.txt](https://docs.addresszen.com/llms.txt). Point your agent there for anything this skill doesn't cover.
