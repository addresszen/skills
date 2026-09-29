# `listLicensees`

List

Returns a key's licensees, oldest first, up to 100 per request. The list omits canceled licensees. The key must be enabled for sub-licensing.

## Endpoint

`GET /keys/{key}/licensees`

See the [API reference](https://docs.addresszen.com/docs/api/list-licensees) for this endpoint.

This operation needs a Management Key. Set it as `userToken` on the client, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/typescript/setup).

## Import

```ts
import { listLicensees } from "@addresszen/sdk";
```

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `string` | yes | **API Key** The API Key to retrieve. Begins `ak_`. |

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `starting_after` | `number` | no | ID of the licensee after which to list results |
| `limit` | `number` | no | **Limit** Specifies the maximum number of records to retrieve. By default the limit is 10. Requesting a larger result set adds latency. |
| `query` | `string` | no | Filter results by licensee name. Can be shortened to `q=` |

## Response Type

```ts
import type { ListLicenseesResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="list-licensees.ts"
import { createZenClient, listLicensees } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({
    apiKey: "ak_test",
    userToken: "uk_example",
  });
  const { data } = await listLicensees({
    client,
    path: { key: "ak_test" },
  });
  return data;
};
```
