# Drop-In Script

Address Lookup is shipped in a polyfilled, typed and minified package called `address-lookup`.

`address-lookup` is designed for rapid integration on a webpage or within a bundler.

## Browser Integration

The fastest and simplest way to start is to drop our pre-bundled script onto a webpage.

### Drop-In Script

```html
<script src="https://cdn.jsdelivr.net/npm/@addresszen/address-lookup"></script>
<script>
  AddressZen.AddressLookup.setup({
    apiKey: "zenkey",
    outputFields: {
      line_1: "#line_1",
      line_2: "#line_2",
      city: "#city",
      state: "#state",
      zip_plus_4_code: "#zipcode",
    },
  });
</script>
```

`address-lookup` ships a UMD compatible build, which targets IE11 and upwards.

The latest build can be downloaded [here](https://www.npmjs.com/package/@addresszen/address-lookup).

#### Demo

```html
<script src="https://cdn.jsdelivr.net/npm/@addresszen/address-lookup"></script>
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
<script>
  AddressZen.AddressLookup.setup({
    apiKey: "ak_test",
    outputFields: {
      line_1: "#line_1",
      line_2: "#line_2",
      city: "#city",
      state: "#state",
      zip_plus_4_code: "#zipcode",
    },
  });
</script>
```

### ES Module

`address-lookup` also ships an ESM compatible build, targeting browsers with ESM support and upwards.

```html
<script type="module">
  import { AddressLookup } from "https://cdn.jsdelivr.net/npm/@addresszen/address-lookup/dist/address-lookup.esm.js";
  AddressLookup.setup({
    apiKey: "zenkey",
    outputFields: {
      line_1: "#line_1",
      line_2: "#line_2",
      city: "#city",
      state: "#state",
      zip_plus_4_code: "#zipcode",
    },
  });
</script>
```

The latest build can be downloaded [here](https://cdn.jsdelivr.net/npm/@addresszen/address-lookup).

#### Demo

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
<script type="module">
  import { AddressLookup } from "https://cdn.jsdelivr.net/npm/@addresszen/address-lookup/dist/address-lookup.esm.js";
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
</script>
```

### Version Control

Serving your own versioned copy is recommended. If a JavaScript CDN is used (e.g. jsDelivr, cdnjs), we strongly recommend pinning the version.

It is important you pin your bundle version in production. Pulling directly from latest will cause your integration to fail at some point in the future.

For instance, follow the instructions on [jsdelivr.com/address-lookup](https://www.jsdelivr.com/package/npm/@addresszen/address-lookup) to pin a major version in production.

E.g.
```html
<script src="https://cdn.jsdelivr.net/npm/@addresszen/address-lookup"></script>
```
