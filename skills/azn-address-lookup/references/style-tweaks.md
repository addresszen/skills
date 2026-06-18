# Style Adjustments

It's possible that the default styling may require a small tweak to allow it to better match your design and site aesthetic. Rather than adding CSS assets, we recommend applying a style attribute as a setup configuration option. The configurations below apply a style attribute directly to a specific element of the Address Lookup.

## Input

`inputStyle`

Applies additional styling to the input field.

## Suggestion Element

`liStyle`

Applies custom styling to every list element `<li>` including address suggestions and messages.

## Suggestion List

`listStyle`

Applies additional styling to the suggestion list.

## Address Lookup Container

`containerStyle`

Applies additional styling to the container element.

## Main Style

`mainStyle`

## Demo

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
    inputStyle: {
      border: "4px solid #e11d48",
      backgroundColor: "#fff1f2",
      color: "#881337",
      fontWeight: "600",
      fontSize: "1.05rem",
    },
    listStyle: {
      borderRadius: "16px",
      border: "4px solid #e11d48",
      backgroundColor: "#fff1f2",
      boxShadow: "0 8px 24px rgba(225, 29, 72, 0.35)",
    },
    liStyle: {
      padding: "20px 24px",
      fontSize: "1.05rem",
      fontWeight: "600",
      color: "#881337",
      borderBottom: "1px solid #fecdd3",
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
