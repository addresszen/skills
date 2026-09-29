# Responses, cancellation and bundles

Every operation resolves to `{ data, request, response }`. A successful JSON response is in `data`, except `keyLogs`, which returns CSV text. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors) for failures.

## How do I cancel a request?

Pass an `AbortController` signal to the operation, then call `abort()`:

```ts title="cancel.ts"
const controller = new AbortController();
const pending = findAddress({
  client,
  query: { query: "123 Main St", context: "USA" },
  signal: controller.signal,
});
controller.abort();
await pending.catch(console.error);
```

## How do I import types?

Import request and response types with `import type`, for example `FindAddressData` and `FindAddressResponse`. Every address comes back in the flat `Address` model, whatever the country. Its `native` field is a union of each dataset's raw record. Narrow it on `dataset` before reading dataset-specific fields.

## How do I keep the bundle small?

Use named ESM imports so a bundler can remove the operations you do not use. The fetch transport is shared overhead. Autocomplete and the React and Preact adapters live behind separate subpaths, so a bare `@addresszen/sdk` import includes neither those helpers nor a framework runtime.
