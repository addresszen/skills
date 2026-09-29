# `updateConfig`

Update

Replaces a configuration's payload and returns the updated configuration. The name is fixed at creation.

## Endpoint

`POST /keys/{key}/configs/{config}`

See the [API reference](https://docs.addresszen.com/docs/api/update-config) for this endpoint.

This operation needs a Management Key. Set it as `userToken` on the client, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/typescript/setup).

## Import

```ts
import { updateConfig } from "@addresszen/sdk";
```

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `string` | yes | **API Key** The API Key to retrieve. Begins `ak_`. |
| `config` | `string` | yes | **Configuration Name** User-provided configuration object name. |

## Query Parameters

_None._

## Request Body

```ts
ConfigUpdateParam
```

## Response Type

```ts
import type { UpdateConfigResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="update-config.ts"
import { createZenClient, updateConfig } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({
    apiKey: "ak_test",
    userToken: "uk_example",
  });
  const { data } = await updateConfig({
    client,
    path: { key: "ak_test", config: "checkout" },
    body: { payload: JSON.stringify({ enabled: false }) },
  });
  return data;
};
```
