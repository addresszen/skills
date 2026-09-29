# `retrieveConfig`

Retrieve

Returns a configuration by name. This request needs no `user_token`, so a browser integration can read its own configuration at runtime.

## Endpoint

`GET /keys/{key}/configs/{config}`

See the [API reference](https://docs.addresszen.com/docs/api/retrieve-config) for this endpoint.

## Import

```ts
import { retrieveConfig } from "@addresszen/sdk";
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
import type { RetrieveConfigResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="retrieve-config.ts"
import { createZenClient, retrieveConfig } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({ apiKey: "ak_test" });
  const { data } = await retrieveConfig({
    client,
    path: { key: "ak_test", config: "checkout" },
  });
  return data;
};
```
