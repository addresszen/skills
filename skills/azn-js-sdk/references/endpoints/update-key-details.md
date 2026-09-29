# `updateKeyDetails`

Update Details

Updates a key's settings and returns its private details. Only the fields you send change. A key on an unlimited plan ignores changes to `datasets`, `daily_limit` and `monthly_limit`.

## Endpoint

`PUT /keys/{key}/details`

See the [API reference](https://docs.addresszen.com/docs/api/update-key-details) for this endpoint.

This operation needs a Management Key. Set it as `userToken` on the client, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/typescript/setup).

## Import

```ts
import { updateKeyDetails } from "@addresszen/sdk";
```

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `string` | yes | **API Key** The API Key to retrieve. Begins `ak_`. |

## Query Parameters

_None._

## Request Body

```ts
ApiKeyDetailsEditable
```

## Response Type

```ts
import type { UpdateKeyDetailsResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="update-key-details.ts"
import { createZenClient, updateKeyDetails } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({
    apiKey: "ak_test",
    userToken: "uk_example",
  });
  const { data } = await updateKeyDetails({
    client,
    path: { key: "ak_test" },
    body: { daily_limit: { limit: 1000 } },
  });
  return data;
};
```
