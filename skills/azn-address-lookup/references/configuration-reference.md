# Configuration Reference

A complete reference for every option accepted by [`AddressLookup.setup`](https://docs.addresszen.com/docs/address-lookup/configure). Only [`apiKey`](#apikey) and [`outputFields`](#outputfields) are required; everything else is optional and has a sensible default.

Callbacks have their own page - see [Callbacks](https://docs.addresszen.com/docs/address-lookup/callbacks). Message strings, CSS classes and inline styles are summarised here and covered in depth under [Messages](https://docs.addresszen.com/docs/address-lookup/messages) and [Styling](https://docs.addresszen.com/docs/address-lookup/default-styling).

### `apiKey`

`string` · required

API Key from your AddressZen account. Typically begins `ak_`.

### `outputFields`

`object` · default `{}`

Specifies where to send address data when an address is selected. Maps an address attribute to an input field, identified by a CSS selector `string` or a direct `HTMLElement` reference.

```javascript
{
  line_1: "#line_1",
  line_2: "#line_2",
  city: document.getElementById("city"),
  state: document.getElementById("state"),
  zip_plus_4_code: document.getElementById("zip_code")
}
```

The attribute names match the Address response object. Fields assigned with a query selector are evaluated lazily (when an address attribute needs to be piped to a field). Using an `HTMLElement` instead binds eagerly at setup.

For dynamic assignment, use the [`onAddressRetrieved`](https://docs.addresszen.com/docs/address-lookup/callbacks) callback.

### `inputField`

`string | HTMLElement` · default `outputFields.line_1`

The `<input>` the Address Lookup binds to. Set this when the search field is not your first address line.

### `scope`

`Document | HTMLElement | string` · default `window.document`

Scopes the operable area of the DOM. Useful when the same form appears more than once on a page.

### `document`

`Document` · default `window.document`

The `Document` to operate on.

### `outputScope`

`string | HTMLElement | Document | null` · default `null`

Narrows where output fields are searched for. Defaults to the controller `scope`.

### `names`

`object` · default `{}`

Targets HTML input elements by their `name` attribute (falling back to `aria-label`) rather than by selector.

### `labels`

`object` · default `{}`

Targets HTML input elements by their associated label text.

### `format`

`"usa" | "gbr"` · default `"usa"`

The format the resolved address is returned in.

### `titleizePostTown`

`boolean` · default `false`

Converts the post town from upper case to title case - e.g. `"NEW YORK"` becomes `"New York"`.

### `removeOrganisation`

`boolean` · default `false`

Removes the organisation name from the address lines. Addresses that consist only of an organisation name are left untouched, as removing it would leave no premise identifier.

### `populateCounty`

`boolean` · default `true`

Set to `false` to suppress `county` from being populated.

### `populateOrganisation`

`boolean` · default `true`

Set to `false` to suppress `organisation_name` from being populated.

### `defaultCountry`

`string` · default `"USA"`

The country searched first, before the user changes it.

### `restrictCountries`

`string[]` · default `[]`

Narrows the supported countries. An empty array enables all countries. A single country disables country selection and hides the country toolbar.

### `detectCountry`

`boolean` · default `true`

Detects the user's country from their IP address.

### `hideToolbar`

`boolean` · default `false`

Hides the toolbar so users cannot change country.

### `contexts`

`object`

A custom list of countries/contexts the user can select from.

### `queryOptions`

`object` · default `{}`

A query - such as a filter or bias - applied to suggestion queries. See the [Autocomplete API Reference](https://docs.addresszen.com/docs/api/find-address) for available parameters.

To apply new parameters after setup, use `setQueryOptions` on the controller instance. Do not mutate `options.queryOptions` directly.

### `resolveOptions`

`object` · default `{}`

Additional query parameters applied to the address resolve request - the second API call that retrieves the full address when a user selects a suggestion. See the [Resolve Address API Reference](https://docs.addresszen.com/docs/api/resolve-address).

To apply new parameters after setup, use `setResolveOptions` on the controller instance. Do not mutate `options.resolveOptions` directly.

### `checkKey`

`boolean` · default `true`

Checks the key is usable before initialising. The check can fail if:

- Your key has no remaining lookups
- Your key has run into its daily lookup limit
- Your key is requested from a URL not on your allowed list
- The user has exceeded their daily limit

On failure the widget does not initialise. Use the [`onFailedCheck`](https://docs.addresszen.com/docs/address-lookup/callbacks) callback to handle this case.

### `autocomplete`

`string` · default `"none"`

Sets the input's `autocomplete=` attribute, aiming to stop browsers (particularly Chrome) presenting a clashing autofill overlay. Best practice changes over time and varies by form - see [this discussion](https://stackoverflow.com/questions/15738259/disabling-chrome-autofill).

### `hide`

`(string | HTMLElement)[]` · default `[]`

Elements to hide with `display: none;` when Address Lookup initialises. They are unhidden when an address is selected or the user opts to enter an address manually.

```javascript
{
  hide: [
    "#line_1",
    document.getElementById("line_2"),
    document.getElementById("city"),
  ],
}
```

Enabling this also renders a clickable element offering manual address entry. Provide your own with [`unhide`](#unhide), or customise the default with [`msgUnhide`](#msgunhide) and [`unhideClass`](#unhideclass).

### `unhide`

`string | HTMLElement | null` · default `null`

A custom clickable element to unhide fields hidden with [`hide`](#hide). Suppresses the default unhide element.

### `unhideClass`

`string` · default `"idpc-unhide"`

CSS class applied to the default unhide element.

### `msgUnhide`

`string` · default `"Enter address manually"`

Text of the default unhide element.

### `unhideStyle`

`object` · default `{}`

Inline styles applied to the unhide element.

### `alignToInput`

`boolean` · default `true`

Automatically aligns the suggestion list to the input.

### `offset`

`number` · default `2`

Vertical offset, in pixels, of the suggestion list from the input.

### `fixed`

`boolean` · default `false`

Sets `position: fixed` on the suggestion list element.

### `aria`

`"1.0" | "1.1"` · default `"1.0"`

The WAI-ARIA specification version to target. `"1.0"` enables regressions that receive the widest screen-reader support (notably VoiceOver and NVDA); `"1.1"` targets the more recent spec.

## Messages

Override any of the user-facing strings. See [Messages](https://docs.addresszen.com/docs/address-lookup/messages) for context.

| Option | Default |
|---|---|
| `msgPlaceholder` | `"Type the first line or postal code of your address"` |
| `msgPlaceholderCountry` | `"Select your country"` |
| `msgInitial` | `"Start typing to find address"` |
| `msgFallback` | `"Please enter your address manually"` |
| `msgNoMatch` | `"No matches found"` |
| `msgList` | `"Select your address"` |
| `msgCountryToggle` | `"Change Country"` |

## CSS classes

Override the class applied to each rendered element. See [CSS Classes](https://docs.addresszen.com/docs/address-lookup/css-classes).

| Option | Default |
|---|---|
| `containerClass` | `"idpc_autocomplete"` |
| `mainClass` | `"idpc_af"` |
| `listClass` | `"idpc_ul"` |
| `messageClass` | `"idpc_error"` |
| `toolbarClass` | `"idpc_toolbar"` |
| `countryToggleClass` | `"idpc_country"` |

## Inline styles

Apply inline styles (a `CSSStyleDeclaration` object) to rendered elements. See [Styling](https://docs.addresszen.com/docs/address-lookup/default-styling).

| Option | Applies to |
|---|---|
| `injectStyle` | `boolean \| string` - inject the default stylesheet (`true`), skip it (`false`), or load a stylesheet from a URL (`string`). Default `true` |
| `inputStyle` | the input field |
| `containerStyle` | the container wrapping all elements |
| `mainStyle` | the main component (list, toolbar, messages) |
| `listStyle` | the suggestion list |
| `liStyle` | each suggestion list item |

## Network and client

Inherited from the underlying API client. Defaults suit the production API and rarely need changing.

| Option | Type | Default |
|---|---|---|
| `baseUrl` | `string` | `"api.addresszen.com"` |
| `version` | `string` | `"v1"` |
| `tls` | `boolean` | `true` |
| `timeout` | `number` | `10000` (ms) |
| `strictAuthorisation` | `boolean` | `false` - force authorisation via HTTP headers only |
| `header` | `object` | `{}` - default headers added to each request |
| `tags` | `string[]` | `[]` - tags appended to requests for your lookup logs |

## Callbacks

Every lifecycle hook is documented on the [Callbacks](https://docs.addresszen.com/docs/address-lookup/callbacks) page: `onLoaded`, `onFailedCheck`, `onMounted`, `onRemove`, `onOpen`, `onClose`, `onFocus`, `onBlur`, `onInput`, `onKeyDown`, `onMouseDown`, `onSuggestionsRetrieved`, `onSuggestionError`, `onAddressSelected`, `onSelect`, `onAddressRetrieved`, `onAddressPopulated`, `onSearchError`, `onCountrySelected`, `onContextChange` and `onUnhide`.
