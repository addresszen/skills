# Address Lookup

> Add Address Verification to your address forms in moments with our Address Lookup JavaScript package.

![AddressZen Address Lookup Demo](https://docs.addresszen.com/../static/img/address-lookup.gif)

## Features

- **Rapid Address Entry.** Receive address suggestions as you type with a response time of less than 100ms.
- **Fuzzy Search.** Reduce keystrokes by compensating for spelling mistakes.
- **Word Abbreviations.** Accepts abbreviations such as av(avenue), hwy (highway), st (street), wy (way).
- **Transposed Letters.** Handle accidental switching of letters, for instance Nwe York (New York).
- **Inclusive.** WAI-ARIA compliant and works on screen readers for maximum accessibility.
- **Customizable.** Extensively customizable behavior and styling.

## Quick Setup

Enable Address Lookup by:
1. Adding your API Key with `apiKey`
2. Designating address fields to be autofilled with `outputFields`

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
    outputFields: {
      line_1: "#line_1",
      line_2: "#line_2",
      city: "#city",
      state: "#state",
      zip_plus_4_code: "#zipcode",
    },
  });
```
