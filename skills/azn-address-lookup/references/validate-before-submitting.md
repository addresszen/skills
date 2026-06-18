# Validate Before Submitting

## Overview

This guide explains how to implement address validation using the AddressLookup library before allowing a form submission. The goal is to ensure users select a valid address, enhancing data integrity and user experience.

## Code Setup

```javascript
import { AddressLookup } from "@addresszen/address-lookup";

let shouldFormSubmit = false;

AddressLookup.setup({
  apiKey: "ak_test",
  outputFields: {
    line_1: "#line_1",
    line_2: "#line_2",
    city: "#city",
    state: "#state",
    zip_plus_4_code: "#zipcode",
  },
  onLoaded: function () {
    const form = this.input.closest("form");
    if (form === null) return;
    form.addEventListener("submit", (e) => {
      if (shouldFormSubmit === false) {
        e.preventDefault();
        // Add custom action - E.g. show a warning
        alert("Please select an address before proceeding");
        return false;
      }
    });
  },
  onAddressPopulated: function () {
    shouldFormSubmit = true;
  },
});
```

## How it Works

- When a user interacts with the input fields for address data and selects a valid address, the AddressLookup's onAddressPopulated callback is fired, setting shouldFormSubmit to true.

- If a user attempts to submit the form before selecting a valid address, the form's submit event is intercepted. A message is displayed, instructing the user to complete the address fields.

- Once a valid address is selected and populated, the user can submit the form successfully.

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
  <button type="submit">Submit</button>
</form>
```

```css
  button[type="submit"] {
    margin-top: 1rem;
    padding: 0.625rem 1rem;
    font-size: 0.875rem;
    font-weight: 500;
    color: #ffffff;
    background-color: #2933e6;
    border: 1px solid transparent;
    border-radius: 0.375rem;
    cursor: pointer;
    transition: background-color 150ms ease, box-shadow 150ms ease;
  }
  button[type="submit"]:hover {
    background-color: #1f29c7;
  }
  button[type="submit"]:focus {
    outline: none;
    box-shadow: 0 0 0 3px rgba(41, 51, 230, 0.25);
  }
  [data-theme="dark"] button[type="submit"] {
    background-color: #545ceb;
  }
  [data-theme="dark"] button[type="submit"]:hover {
    background-color: #6970ef;
  }
  [data-theme="dark"] button[type="submit"]:focus {
    box-shadow: 0 0 0 3px rgba(84, 92, 235, 0.35);
  }
```

```javascript
  import { AddressLookup } from "@addresszen/address-lookup";

  let shouldFormSubmit = false;

  AddressLookup.setup({
    apiKey: "ak_test",
    outputFields: {
      line_1: "#line_1",
      line_2: "#line_2",
      city: "#city",
      state: "#state",
      zip_plus_4_code: "#zipcode",
    },
    onLoaded: function () {
      const form = this.input.closest("form");
      if (form === null) return;
      form.addEventListener("submit", (e) => {
        e.preventDefault();
        if (shouldFormSubmit === false) {
          alert("Please select an address before proceeding");
          return false;
        }
        alert("Submitted");
      });
    },
    onAddressPopulated: function () {
      shouldFormSubmit = true;
    },
  });
```
