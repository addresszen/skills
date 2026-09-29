# `deleteConfig`

Delete

Permanently deletes a configuration object.

## Endpoint

`DELETE /keys/{key}/configs/{config}`

See the [API reference](https://docs.addresszen.com/docs/api/delete-config) for this endpoint.

This operation needs a Management Key. Set it as `userToken` on the client, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/typescript/setup).

## Import

```ts
import { deleteConfig } from "@addresszen/sdk";
```

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `string` | yes | **API Key** The API Key to retrieve. Begins `ak_`. |
| `config` | `string` | yes | **Configuration Name** User-provided configuration object name. |

## Query Parameters

_None._

## Response Type

```ts
import type { DeleteConfigResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="delete-config.ts"
import { createZenClient, deleteConfig } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({
    apiKey: "ak_test",
    userToken: "uk_example",
  });
  const { data } = await deleteConfig({
    client,
    path: { key: "ak_test", config: "checkout" },
  });
  return data;
};
```
