# Checking the usability of your key

Your key may not be available at some times. For instance:

- Your key may have reached its daily cap set by you
- Your user has reached their individual usage cap for the day
- The balance on your key is exhausted

By default, Address Lookup will not initialize if your key is not usable for whatever reason. You may use the `onLoaded` and `onFailedCheck` callbacks to make necessary adjustments.

To disable key checking, set `checkKey` to `false`.

```html
<form>
  <p id="message"></p>
  <label for="input">Search Your Address</label>
  <input type="text" id="input" placeholder="Start typing address here" />
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
  #message {
    margin: 0 0 0.5rem;
    padding: 0.5rem 0.75rem;
    font-size: 0.8125rem;
    font-weight: 500;
    border-radius: 0.375rem;
  }
  #message:empty {
    display: none;
  }
  #message.success {
    color: #065f46;
    background-color: #d1fae5;
    border: 1px solid #a7f3d0;
  }
  #message.error {
    color: #991b1b;
    background-color: #fee2e2;
    border: 1px solid #fecaca;
  }
  [data-theme="dark"] #message.success {
    color: #6ee7b7;
    background-color: rgba(16, 185, 129, 0.12);
    border-color: rgba(110, 231, 183, 0.35);
  }
  [data-theme="dark"] #message.error {
    color: #fca5a5;
    background-color: rgba(239, 68, 68, 0.12);
    border-color: rgba(252, 165, 165, 0.35);
  }
```

```javascript
  import { AddressLookup } from "@addresszen/address-lookup";

  AddressLookup.setup({
    inputField: "#input",

    // Test key: 'ak_test' passes the check
    apiKey: "ak_test",
    // Test key: 'ak_fails' fails the key check
    // apiKey: 'ak_fails',

    // By default, checkKey is enabled
    checkKey: true,

    // Invoked if plugin loads
    onLoaded: function () {
      const el = document.getElementById("message");
      el.textContent = "Check passed! Start typing your address";
      el.className = "success";
    },

    // Invoked if key fails check
    onFailedCheck: function () {
      const el = document.getElementById("message");
      el.textContent = "Check failed. Please manually enter your address";
      el.className = "error";
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
