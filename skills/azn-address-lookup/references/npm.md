# Package Manager (npm)

Address Lookup is also available without transpilation or minification on npm as [`@addresszen/address-lookup`](https://www.npmjs.com/package/@addresszen/address-lookup).

The `address-lookup` npm package works out-of-the-box with most bundlers. The advantages of consuming this package are:
- Finer control over which browsers you wish to support
- Dependency deduplication
- Tree shaking
- Smaller package sizes

### Add

Add address-lookup to your project via npm with

```bash
npm install @addresszen/address-lookup
```

### Instantiate

Instantiate Address Lookup with `AddressLookup.setup`.

```javascript
import { AddressLookup } from "@addresszen/address-lookup";

const controller = AddressLookup.setup({
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
