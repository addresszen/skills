# Merge Address into a Single Field

Instead of writing each address attributes to individual fields, you may exercise fine control about how address data is presented using the `onAddressRetrieved` callback.

In this example, we merge the address fields and insert the result into a `textarea`.

```html
<form>
  <label for="input">Search Your Address</label>
  <input type="text" id="input" placeholder="Start typing address here" />
  <label for="output_field">Address</label>
  <textarea id="output_field" rows="5"></textarea>
</form>
```

```css
  textarea {
    width: 100%;
    padding: 0.5rem 0.75rem;
    font-family: inherit;
    font-size: 0.875rem;
    color: #111827;
    background-color: #ffffff;
    border: 1px solid #d1d5db;
    border-radius: 0.375rem;
    box-sizing: border-box;
    resize: vertical;
    transition: border-color 150ms ease, box-shadow 150ms ease;
  }
  textarea:focus {
    outline: none;
    border-color: #2933e6;
    box-shadow: 0 0 0 3px rgba(41, 51, 230, 0.15);
  }
  [data-theme="dark"] textarea {
    background-color: #2a2a2a;
    border-color: #444950;
    color: #e5e7eb;
  }
  [data-theme="dark"] textarea:focus {
    border-color: #545ceb;
    box-shadow: 0 0 0 3px rgba(84, 92, 235, 0.25);
  }
```

```javascript
  import { AddressLookup } from "@addresszen/address-lookup";

  AddressLookup.setup({
    apiKey: "ak_test",
    inputField: "#input",
    onAddressRetrieved: (address) => {
      const result = [
        address.line_1,
        address.line_2,
        address.city,
        address.state,
        address.zip_plus_4_code,
      ]
        .filter((elem) => elem !== "")
        .join("\\n");
      document.getElementById("output_field").textContent = result;
    },
  });
```
