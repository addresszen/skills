# `createLicensee`

Create

Creates a licensee on a key and returns it with its generated `sl_` key. The key must be enabled for sub-licensing.

## Endpoint

`POST /keys/{key}/licensees`

See the [API reference](https://docs.addresszen.com/docs/api/create-licensee) for this endpoint.

This operation needs a Management Key. Set it as `userToken` on the client, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/typescript/setup).

## Import

```ts
import { createLicensee } from "@addresszen/sdk";
```

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `string` | yes | **API Key** The API Key to retrieve. Begins `ak_`. |

## Query Parameters

_None._

## Request Body

```ts
LicenseeEditable
```

## Response Type

```ts
import type { CreateLicenseeResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="create-licensee.ts"
import { createZenClient, createLicensee } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({
    apiKey: "ak_test",
    userToken: "uk_example",
  });
  const { data } = await createLicensee({
    client,
    path: { key: "ak_test" },
    body: { name: "Example Company" },
  });
  return data;
};
```
