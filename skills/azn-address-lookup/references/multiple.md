# Attach Multiple Instances

Address Lookup can be invoked multiple times to attach multiple instances to your forms.

Each Address Lookup instance is isolated and can be configured individually.

```html
<form>
  <label for="input">Search Address</label>
  <input type="text" id="input" placeholder="Start typing address here" />
  <hr />
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

```css
  label[for="input"] {
    font-size: 0.9375rem;
    font-weight: 600;
  }
  #input {
    padding: 0.625rem 0.875rem;
    font-size: 0.9375rem;
    border-width: 2px;
  }
  hr {
    border: 0;
    border-top: 1px solid #e5e7eb;
    margin: 1.25rem 0 0.5rem;
  }
  [data-theme="dark"] hr {
    border-top-color: #374151;
  }
```

```javascript
  import { AddressLookup } from "@addresszen/address-lookup";

  AddressLookup.setup({
    apiKey: "ak_test",
    inputField: "#input",
    outputFields: {
      line_1: "#line_1",
      line_2: "#line_2",
      city: "#city",
      state: "#state",
      zip_plus_4_code: "#zipcode",
    },
  });

  AddressLookup.setup({
    apiKey: "ak_test",
    inputField: "#line_1",
    outputFields: {
      line_1: "#line_1",
      line_2: "#line_2",
      city: "#city",
      state: "#state",
      zip_plus_4_code: "#zipcode",
    },
  });
```
