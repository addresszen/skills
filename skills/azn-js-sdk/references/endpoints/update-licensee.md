# `updateLicensee`

Update

Updates a licensee's address, postcode, allowed URLs and daily limit. Returns the updated licensee. The name is fixed at creation.

## Endpoint

`POST /keys/{key}/licensees/{licensee}`

See the [API reference](https://docs.addresszen.com/docs/api/update-licensee) for this endpoint.

This operation needs a Management Key. Set it as `userToken` on the client, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/typescript/setup).

## Import

```ts
import { updateLicensee } from "@addresszen/sdk";
```

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `string` | yes | **API Key** The API Key to retrieve. Begins `ak_`. |
| `licensee` | `string` | yes | **Licensee Key** Uniquely identifies a licensee. |

## Query Parameters

_None._

## Request Body

```ts
LicenseeEditable
```

## Response Type

```ts
import type { UpdateLicenseeResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="update-licensee.ts"
import { createZenClient, updateLicensee } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({
    apiKey: "ak_test",
    userToken: "uk_example",
  });
  const { data } = await updateLicensee({
    client,
    path: { key: "ak_test", licensee: "sl_example" },
    body: { name: "Updated Company" },
  });
  return data;
};
```
