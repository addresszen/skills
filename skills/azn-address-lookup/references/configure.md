# Configure

Address Lookup exports a `setup` method to apply address verification to a form. `setup` requires the following configuration at minimum.

> `apiKey` and `outputFields` below are all you need to get Address Lookup working. For the complete set of controller options, see [Configuration Reference](https://docs.addresszen.com/docs/address-lookup/configuration-reference).

## API Key

`apiKey`

API Key from your AddressZen account. Typically begins `ak_`

## Address Targets

`outputFields`

Specify where to send address data given a selected address. `outputFields` is an object which maps an address attribute to an input field. The input field can be identified by CSS or reference to the DOM element itself.

```javascript
{
  line_1: "#line_1",
  line_2: "#line_2",
  city: document.getElementById("city"),
  state: document.getElementById("state"),
  zip_plus_4_code: document.getElementById("zip_code")
}
```

> The fields above (`line_1`, `line_2`, `city`, `state` and `zip_plus_4_code`) are the minimum set needed to capture a complete, deliverable US address. Collect all of them so the address you store reliably routes to the premises.

Two address lines, city, state, and zip code fields are all the addressing information required to identify a US address. You may extract more data for an address by passing more properties into the `outputFields` configuration object.

The configuration attributes for `outputFields` match the Address response object.

More complex, dynamic assignment can be performed using the `onAddressRetrieved` callback.

Output fields assigned with a query selector are evaluated lazily (i.e. when an address attribute needs to be piped to a field).

## Country

A third, optional attribute to be aware of is country. Use `country_iso` or `country_iso_2` to populate the 3 or 2 letter ISO code (`"USA"` or `"US"`, for example). For the full country name on an input, use `country`, which yields a value like `"United States"`.

Each of these targets can be an `<input>` or a `<select>`. When the target is a `<select>`, Address Lookup resolves the matching `<option>` for you - it first matches on the option `value`, then falls back to the option's visible text - so no callback is needed. See [Populate a country select](https://docs.addresszen.com/docs/address-lookup/populate-country-select) for a worked example.

<!--- [More information on addressing data can be found on our address data documentation](https://docs.addresszen.com/docs/data). --->
