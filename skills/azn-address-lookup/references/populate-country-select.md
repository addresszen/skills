# Populate a country select

Your form may capture country with a `<select>` rather than a free text `<input>` - for example a checkout that stores the ISO-3 country code (`"USA"`, `"CAN"`, `"GBR"`) against the order.

Point an `outputFields` country attribute at the `<select>` and Address Lookup selects the matching option for you. It matches the retrieved value against each option's `value` first, then falls back to the option's visible text, so you don't need a callback.

Map the attribute whose values line up with your option `value`s:

- `country_iso` for 3 letter ISO codes (`"USA"`)
- `country_iso_2` for 2 letter ISO codes (`"US"`)
- `country` for the full country name (`"United States"`)

## Live Demo

The country `<select>` below uses 3 letter ISO codes as its option values, so `country_iso` is mapped to it. Search for a US address and the `United States` option is selected automatically.

```html
<form style="max-width: 450px; padding: 10px;">
  <label for="line_1">Address First Line</label>
  <input type="text" id="line_1" />
  <label for="line_2">Address Second Line</label>
  <input type="text" id="line_2" />
  <label for="city">City</label>
  <input type="text" id="city" />
  <label for="state">State</label>
  <input type="text" id="state" />
  <label for="zipcode">Zip Code</label>
  <input type="text" id="zipcode" />
  <label for="country">Country</label>
  <select id="country" name="country">
    <option value="">Select a country</option>
    <option value="AUS">Australia</option>
    <option value="CAN">Canada</option>
    <option value="GBR">United Kingdom</option>
    <option value="USA">United States</option>
  </select>
</form>
```

```javascript
  import { AddressLookup } from "@addresszen/address-lookup";

  AddressLookup.setup({
    apiKey: "ak_test",
    outputFields: {
      line_1: "#line_1",
      line_2: "#line_2",
      city: "#city",
      state: "#state",
      zip_plus_4_code: "#zipcode",
      country_iso: "#country",
    },
  });
```
