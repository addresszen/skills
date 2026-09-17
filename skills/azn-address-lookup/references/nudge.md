# Vertically Shift Address Lookup

From time to time, you may want to tweak the default style of Address Lookup to better match your application's design system.

[Style Adjustments](https://docs.addresszen.com/docs/address-lookup/style-tweaks) are the recommended means to make small changes.

A common issue is the alignment of the Address Lookup dropdown — this may be a few pixels too high or low. In these instances, we recommend a positive or negative `margin-top` style attribute.

```html
<form>
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
</form>
```

```javascript
  import { AddressLookup } from "@addresszen/address-lookup";

  AddressLookup.setup({
    apiKey: "ak_test",
    listStyle: {
      marginTop: "-1.4rem",
    },
    outputFields: {
      line_1: "#line_1",
      line_2: "#line_2",
      city: "#city",
      state: "#state",
      zip_plus_4_code: "#zipcode",
    },
  });
```
