---
name: azn-js-sdk
description: Use when integrating the AddressZen fetch-based TypeScript SDK. Covers API calls, autocomplete, errors and React or Preact Query adapters.
license: SEE LICENSE IN LICENSE
metadata:
  author: addresszen
  homepage: https://addresszen.com
references:
  - setup.md
  - autocomplete.md
  - filter-and-bias.md
  - address-verify.md
  - react.md
  - errors.md
  - common.md
  - endpoints/
---

# AddressZen TypeScript SDK

Call the AddressZen API with typed functions over native fetch. Supports browsers and Node.js 22 or later.

```bash
npm install @addresszen/sdk
```

```ts
import { createZenClient, findAddress } from "@addresszen/sdk";

const client = createZenClient({ apiKey: "ak_test" });
const { data } = await findAddress({
  client,
  query: { query: "123 Main St", context: "USA" },
});
console.log(data.result.hits);
```

Each address search runs in one country, set with `context` to a three-letter ISO 3166-1 code such as `USA`, `CAN` or `JPN`. Without it, the search uses the account's default country. Address verification covers US addresses only.

Pass the client to each operation. Each instance holds its own configuration. ESM bundlers can remove unused operations; autocomplete and framework adapters use separate imports.

## Authentication and errors

Set `apiKey` on the client. Private account operations also need a Management Key, set as `userToken`. Never put a Management Key in browser code. HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](./references/errors.md).

## References

- [Setup](./references/setup.md)
- [Autocomplete](./references/autocomplete.md)
- [Filter and bias](./references/filter-and-bias.md)
- [Address verification](./references/address-verify.md)
- [React and Preact](./references/react.md)
- [Error handling](./references/errors.md)
- [Common behavior](./references/common.md)
- [Operations](./references/endpoints/)
