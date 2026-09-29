# `keyAvailability`

Availability

Returns public information on an API Key: whether it can be used right now (`available`), the search contexts the key is licensed for (`contexts`) and the context that best matches the caller's IP address (`context`).

The endpoint accepts API Keys (beginning `ak_`) and sub-licensed keys (beginning `sl_`), and needs no Management Key.

A key that exists but cannot be used, because it has no lookups left or has breached a limit, returns `200` with `"available": false`. An unknown or malformed key returns an error.

Supply a valid Management Key and the endpoint returns the key's private details instead, as `GET /keys/{key}/details` does. A Management Key that does not own the key is rejected.

## Endpoint

`GET /keys/{key}`

See the [API reference](https://docs.addresszen.com/docs/api/key-availability) for this endpoint.

## Import

```ts
import { keyAvailability } from "@addresszen/sdk";
```

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `string` | yes | **API Key** The API Key to retrieve. Begins `ak_`. |

## Query Parameters

_None._

## Response Type

```ts
import type { KeyAvailabilityResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="key-availability.ts"
import { createZenClient, keyAvailability } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({ apiKey: "ak_test" });
  const { data } = await keyAvailability({
    client,
    path: { key: "ak_test" },
  });
  return data;
};
```
