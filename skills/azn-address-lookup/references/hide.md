# Hide Address Fields

## Hide

In some instances, you may want to hide the address inputs and subsequently unhide them when the user has selected a verified address. This makes it harder for the user to input an incorrect address and bypass address verification.

Address Lookup provides this functionality natively using `hide`. Specify which HTML Elements you would like to hide as CSS Selector or references. When the user selects an address, or address verification fails (no balance, limit reached, etc), the fields will unhide.

A clickable link will also be provided to allow the user to manually enter an address.

```html
<form>
  <label for="input">Search Your Address</label>
  <input type="text" id="input" placeholder="Start typing address here" />
  <div id="hiddenfields">
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
  </div>
</form>
```

```javascript
  import { AddressLookup } from "@addresszen/address-lookup";

  AddressLookup.setup({
    apiKey: "ak_test",
    hide: ["#hiddenfields"],
    inputField: "#input",
    outputFields: {
      line_1: "#line_1",
      line_2: "#line_2",
      city: "#city",
      state: "#state",
      zip_plus_4_code: "#zipcode",
    },
  });
```

## Custom Unhide Element

You can assign a custom element to serve as a clickable element to unhide the address fields. Use the `unhide` option.
