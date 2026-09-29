# Error handling

Every operation rejects with `ApiError`, a subclass of `Error`, when the API returns an HTTP error.

## What does `ApiError` contain?

| Property | Contents |
| --- | --- |
| `status` | HTTP status, such as `404` |
| `code` | API error code. `undefined` when the body is not JSON |
| `message` | API error message, or the HTTP status text |
| `body` | Parsed JSON body, or the raw text |
| `response` | The fetch `Response` |

```ts title="errors.ts"
import { ApiError, createZenClient, findAddress } from "@addresszen/sdk";

const client = createZenClient({ apiKey: "ak_test" });
try {
  const { data } = await findAddress({ client, query: { query: "123 Main St" } });
  console.log(data.result.hits);
} catch (e) {
  if (!(e instanceof ApiError)) throw e;
  console.error(e.status, e.code, e.message);
}
```

A network failure or an aborted request rejects with the runtime's native error instead, such as `TypeError` or `AbortError`. The [error codes guide](https://docs.addresszen.com/docs/guides/error-codes) lists each API error `code` and how to fix it.

## How do I handle errors without exceptions?

Pass `throwOnError: false` to get `{ data, error }` instead of a rejection. For an HTTP error, `error` is the API's error body, typed per operation, and `response` holds the HTTP status. For a network failure, `error` is the native error and `response` is `undefined`.

```ts title="result.ts"
const result = await findAddress({ client, query: { query: "123 Main St" }, throwOnError: false });
if (result.error) {
  console.error(result.response?.status, result.error.code, result.error.message);
} else {
  console.log(result.data.result.hits);
}
```
