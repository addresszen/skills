# Troubleshooting Address Lookup

The recurring failure modes when integrating `@addresszen/address-lookup`,
each with the cause and the fix. If the user is hitting one of these, jump
straight to the matching section — don't re-derive the diagnosis.

## Network errors

### 403 Forbidden on every request

**Cause:** the API key has an allowed-URL list and the page's origin isn't on
it. Frontend keys (`ak_*`) are domain-restricted by default — AddressZen
checks the `Origin`/`Referer` of every request.

**Fix:** in your AddressZen account → Keys → click the key → Allowed URLs, add
the exact origin. Match scheme and host (e.g. `https://example.com`, no
trailing slash, no path). For local dev, add `http://localhost:3000` (or
whatever port). `localhost` is allowed by default.

### 401 Unauthorized

**Cause:** the key is wrong, deleted, or paused.

**Fix:** verify the value in `apiKey` matches the key shown in the dashboard.
Common mistake: copying with surrounding whitespace, or using a *secret* key
on the frontend (those are server-only).

### 429 Too Many Requests

**Cause:** either daily lookup balance is exhausted, or the per-second rate
limit is hit (typically only seen with bot traffic or load tests).

**Fix:** check the account dashboard for balance and rate-limit settings.
For development, top up or use a test key. For production bursts, contact
support to raise the per-key cap.

### CORS error in browser console

**Cause:** mismatch between the origin the browser is sending and what's on
the key's allowed list. Or you're calling from a non-HTTPS origin to the
HTTPS API.

**Fix:** add the exact origin (with scheme) to the key's allowed URLs. For
local `file://` development, that won't work — serve over `http://localhost`.

### Content Security Policy (CSP) blocks the widget

**Cause:** the page's `Content-Security-Policy` header doesn't allow the
widget's script source or its API endpoint.

**Fix:** add to `connect-src`: `https://api.addresszen.com`. If using the CDN
bundle, add to `script-src`: `https://cdn.jsdelivr.net`. Because styling is
injected by default, add to `style-src`: `'unsafe-inline'`, or set
`injectStyle: false` and ship your own stylesheet.

## Initialisation problems

### `AddressLookup is not a constructor`

**Cause:** code is calling `new AddressLookup(...)`. It's a factory, not a
class.

**Fix:** `AddressLookup.setup({...})` (or `AddressLookup.watch({...})` for
React).

### `outputFields is required` / silent: form not populating after selection

**Cause:** missing or wrong `outputFields`. The widget retrieves the address
but has nowhere to put it.

**Fix:** map every field you want populated. Selectors are evaluated lazily,
so they can refer to fields rendered after setup runs:

```js
outputFields: {
  line_1: "#line_1",
  line_2: "#line_2",
  city: "#city",
  state: "#state",
  zip_plus_4_code: "#zipcode",
}
```

If selectors look right but fields still don't update, open devtools — the
selector probably matches a different element than expected. The
`onAddressRetrieved` callback receives the full address payload; logging it
confirms the data is arriving.

### Wrong fields populate / empty `state`, `zip_plus_4_code`

**Cause:** `outputFields` is using the UK shape while the lookup is returning
US addresses (the default), or vice versa.

**Fix:** match `outputFields` to the active country. US addresses use
`line_1`, `line_2`, `city`, `state`, `zip_plus_4_code`; UK addresses
(`defaultCountry: "GBR"`) use `line_1`, `post_town`, `postcode`, `county`.
See [`additional-data.md`](./references/additional-data.md).

### Widget looks unstyled

**Cause:** `injectStyle` was set to `false` without supplying a replacement
stylesheet.

**Fix:** either leave `injectStyle` at its default (`true`, the widget injects
its own styles), or provide your own CSS targeting the widget's classes. See
[`default-styling.md`](./references/default-styling.md) and
[`css-classes.md`](./references/css-classes.md).

### Bundler errors importing the npm package

**Cause:** an older bundler config that doesn't transpile dependencies.

**Fix:** the npm package works with most bundlers out of the box. If yours
can't process it, load the polyfilled UMD bundle from jsDelivr via a
`<script>` tag instead (global `AddressZen.AddressLookup`). See
[`script.md`](./references/script.md).

## React-specific

### Widget appears twice / `onLoaded` fires twice in dev

**Cause:** React 18 StrictMode mounts components twice in development. Each
mount calls `setup()` / `watch()` again.

**Fix:** guard with a ref so init runs once even on re-mount:

```jsx
const inited = useRef(false);
useEffect(() => {
  if (inited.current) return;
  inited.current = true;
  AddressLookup.watch({ inputField: "#search", apiKey: "ak_...", /* … */ });
}, []);
```

This is also the right pattern outside StrictMode — you don't want
re-initialisation on every render anyway. For a React-idiomatic surface,
prefer the `@addresszen/react` wrapper (its own `azn-react` skill).

### `setup` runs but no autocomplete appears

**Cause:** the input field referenced by `inputField` hadn't mounted when
`setup` ran.

**Fix:** use `AddressLookup.watch` instead of `.setup`. `watch` polls the DOM
and binds when the field appears. See [`react.md`](./references/react.md).

### Page navigation: widget stops working after route change

**Cause:** in SPAs, the input field gets unmounted on navigation but the
controller still references the old element.

**Fix:** detach and re-attach on navigation. See
[`detach.md`](./references/detach.md) and [`nudge.md`](./references/nudge.md).

## UX issues

### Country toolbar still shows after `restrictCountries: ["USA"]`

**Cause:** `restrictCountries` removes the country *picker control* but leaves
the toolbar container rendered. The two options are independent.

**Fix:** also hide the toolbar — see [`hide.md`](./references/hide.md).

### Browser autofill collides with the lookup dropdown

**Cause:** the lookup input gets `autocomplete` suggestions from the browser
on top of the widget's dropdown.

**Fix:** see [`prevent-autofill.md`](./references/prevent-autofill.md) — the
widget accepts an option to disable browser autofill on its input.

### Suggestions list is empty for valid input

**Cause:** a country filter, geospatial box, or exclusion (islands, military,
PO Box) is active and excluding the user's address.

**Fix:** check the filter options against where the user is actually typing.
`filter` is restrictive; `bias` only re-orders results. Loosen the filter or
switch to bias. See [`filter-by-geospatial-box.md`](./references/filter-by-geospatial-box.md).

## When the gotcha isn't here

1. Check the `onFailedCheck` callback fired during init — that's the API's way
   of telling the page the key isn't usable.
2. Open the network tab and inspect an autocomplete request to
   `https://api.addresszen.com`. The error body has a machine-readable `code`
   and human-readable `message`.
3. Reach support: `support@addresszen.com`. Include the API key (the public
   `ak_*` form is fine), the URL where the problem reproduces, and a request
   ID from the network tab.
