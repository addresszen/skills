# `deleteLicensee`

Cancel

Cancels a licensee. Its key stops working and it drops out of the licensee list. Contact us to reverse it.

## Endpoint

`DELETE /keys/{key}/licensees/{licensee}`

See the [API reference](https://docs.addresszen.com/docs/api/delete-licensee) for this endpoint.

This operation needs a Management Key. Set it as `userToken` on the client, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/typescript/setup).

## Import

```ts
import { deleteLicensee } from "@addresszen/sdk";
```

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `string` | yes | **API Key** The API Key to retrieve. Begins `ak_`. |
| `licensee` | `string` | yes | **Licensee Key** Uniquely identifies a licensee. |

## Query Parameters

_None._

## Response Type

```ts
import type { DeleteLicenseeResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="delete-licensee.ts"
import { createZenClient, deleteLicensee } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({
    apiKey: "ak_test",
    userToken: "uk_example",
  });
  const { data } = await deleteLicensee({
    client,
    path: { key: "ak_test", licensee: "sl_example" },
  });
  return data;
};
```
