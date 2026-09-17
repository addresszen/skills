# Gate Population by Delivery Area

## Overview

`shouldAddressPopulate` runs after an address is retrieved and **before** it is written to the form. Return `false` to cancel population, or `true` to proceed. Use it to block addresses you can't serve - outside a delivery area, an unsupported state, or any custom rule - before the fields are filled in.

The predicate may be synchronous or return a promise, so you can call your own API to make the decision.

## Cancel synchronously

Return `false` from a plain function to block population. Here we only accept addresses in California and New York:

```javascript
import { AddressLookup } from "@addresszen/address-lookup";

const SERVED = ["CA", "NY"];

AddressLookup.setup({
  apiKey: "ak_test",
  outputFields: {
    line_1: "#line_1",
    line_2: "#line_2",
    city: "#city",
    state: "#state",
    zip_plus_4_code: "#zipcode",
  },
  shouldAddressPopulate: function (address) {
    const ok = SERVED.includes(address.state);
    if (!ok) this.setMessage("Sorry, we don't ship to this state yet");
    return ok;
  },
});
```

## Check asynchronously

Return a promise to defer to your own API. **Errors are your responsibility**: a rejecting promise **fails open** (population proceeds) rather than blocking the user on a broken check. Catch inside the predicate and return an explicit boolean - `return false` to cancel, `return true` to allow:

```javascript
shouldAddressPopulate: async function (address) {
  try {
    const res = await fetch(`/api/delivery-area?zip=${address.zip_plus_4_code}`);
    const { deliverable } = await res.json();
    if (!deliverable) this.setMessage("Sorry, we don't deliver to this address");
    return deliverable;
  } catch (err) {
    reportError(err);   // your telemetry - the widget will not surface this
    return true;        // fail open: don't block the customer on an outage
    // return false;    // ...or fail closed to be strict
  }
}
```

## Reacting to the decision

- **To show a message on cancel**, do it inside the predicate before `return false` (as above).
- **To confirm population actually happened** - for example to gate a form submit - use the [`onAddressPopulated`](https://docs.addresszen.com/docs/address-lookup/callbacks) callback. It fires only when population proceeds, so a canceled selection never trips it.

## Live Demo

Search for an address. Addresses outside California and New York are declined and the fields stay empty.

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
</form>
```

```javascript
  import { AddressLookup } from "@addresszen/address-lookup";

  const SERVED = ["CA", "NY"];

  AddressLookup.setup({
    apiKey: "ak_test",
    outputFields: {
      line_1: "#line_1",
      line_2: "#line_2",
      city: "#city",
      state: "#state",
      zip_plus_4_code: "#zipcode",
    },
    shouldAddressPopulate: function (address) {
      const ok = SERVED.includes(address.state);
      if (!ok) this.setMessage("Sorry, we don't ship to this state yet");
      return ok;
    },
  });
```
