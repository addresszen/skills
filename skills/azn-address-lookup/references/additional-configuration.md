# Additional Configuration

## Separate Input Field

`inputField`

Configure `inputField` if you want Address Lookup to render on an input field which is not your first address line.

CSS selector or HTML Element which specifies the `<input>` field which the Address Lookup interface should bind.

Defaults to `outputFields.line_1` (the first address line).

## Disable Key Check

`checkKey`

Enabled by default. This causes Address Lookup to check if the key is in a usable state before initializing itself.

Defaults to `true`.

The check can fail if:

- Your key has no remaining lookups
- Your key has run into its lookup limit for the day
- Your key is requested from a URL which is not on your whitelist
- The user seeking to use the key has exceeded their limit for the day

If the check fails, the plugin will not initialize. You can use the `onFailedCheck` callback to customize your response to a failed check.

## Title Case Post Town

`titleizePostTown`

An optional field to convert the case of the Post Town from upper case into title case. E.g. `"NEW YORK"` becomes `"New York"`.

Defaults to `true`.

## Query Options

`queryOptions`

Apply a query, like a filter or bias, to your suggestion queries. A complete list of query parameters are available in the [Autocomplete API Reference](https://docs.addresszen.com/docs/api/find-address).

To apply new parameters after the Controller has been instantiated, use `setQueryOptions`. Do not mutate `options.queryOptions` directly.

Defaults to `{}`.

## Remove Organization from Address Line

`removeOrganisation`

If set to `true`, organization name will be removed from the address.

Defaults to `false`.

## Disable Chrome Autofill

`autocomplete`

Sets the `autocomplete=` attribute of the input element. Setting this attribute aims to prevent some browsers (particularly Chrome) from providing a clashing autofill overlay.

The best practice for this attribute breaks over time (see [https://stackoverflow.com/questions/15738259/disabling-chrome-autofill](https://stackoverflow.com/questions/15738259/disabling-chrome-autofill)) and is specific to different forms. If you are observing Chrome's autofill clashing on your form, update this attribute to the current best practices.

Defaults to `"none"`.

## Hide Address Fields

`hide`

Accepts an array of HTMLElements or CSS selectors. E.g.

```javascript
{
  hide: [
    "#line_1",
    document.getElementById("line_2"),
    document.getElementById("line_3")],
  ],
}
```

When enabled, the HTMLElements supplied in `hide` are hidden with `display: none;` when Address Lookup initializes and attaches to the DOM. These elements will be subsequently unhidden if an address is selected or the user opts to manually input an address.

Enabling this feature will also create a clickable element in the Address Lookup, which provides users the option to manually input an address. You may provide your own clickable element with `unhide` or customize the clickable element with `msgUnhide` and `unhideClass`.

Defaults to `[]`.

## Custom Unhide Element

`unHide`

Specify a query selector (`string`) or (`HTMLElement`) as a custom clickable element to unhide and form fields configured with `hide`. This will prevent the default unhide element from being rendered.
