# CSS Classes

The Address Lookup can be styled with CSS classes.

## CSS Class Hierarchy

```html
<div class="idpc_autocomplete">
  <input type="text">
  <ul class="idpc_ul">
    <li class="idpc_error">This element only shows when a message is communicated to the user</li>
    <li class="idpc_action">This element only shows when a search returns no matches and msgNoMatchAction is configured</li>
    <li aria-selected="true">Address Suggestion One</li>
    <li aria-selected="false">Address Suggestion Two</li>
    <li aria-selected="false">Address Suggestion Three</li>
  </ul>
</div>
```

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

```css
.idpc_autocomplete {
  width: 100%;
  max-width: 400px;
  background-color: #b3e5fc;
  border: 1px solid #81d4fa;
}

.idpc_ul {
  list-style: none;
  padding: 0;
  margin: 0;
  background-color: #ffccbc;
  border: 1px solid #ffab91;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.idpc_error {
  color: #ffffff;
  background-color: #f44336;
  padding: 8px;
  border-bottom: 1px solid #d32f2f;
}

.idpc_toolbar {
  background-color: #64b5f6;
  color: #fff176;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 2px solid #42a5f5;
}

.idpc_country {
  background-color: #ffb74d;
  color: #6a1b9a;
  display: inline-block;
  margin: 5px 0;
  border-radius: 4px;
  font-weight: bold;
}
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
