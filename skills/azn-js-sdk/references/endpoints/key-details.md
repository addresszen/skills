# `keyDetails`

Details

Returns private data on a key: remaining lookups, licensed datasets, usage limits, notification settings and the search contexts the key can serve.

## Endpoint

`GET /keys/{key}/details`

See the [API reference](https://docs.addresszen.com/docs/api/key-details) for this endpoint.

This operation needs a Management Key. Set it as `userToken` on the client, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/typescript/setup).

## Import

```ts
import { keyDetails } from "@addresszen/sdk";
```

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `string` | yes | **API Key** The API Key to retrieve. Begins `ak_`. |

## Query Parameters

_None._

## Response Type

```ts
import type { KeyDetailsResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="key-details.ts"
import { createZenClient, keyDetails } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({
    apiKey: "ak_test",
    userToken: "uk_example",
  });
  const { data } = await keyDetails({
    client,
    path: { key: "ak_test" },
  });
  return data;
};
```
