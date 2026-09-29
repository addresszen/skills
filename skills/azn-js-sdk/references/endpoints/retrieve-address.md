# `retrieveAddress`

Retrieve Address

Returns the full address for an autocomplete suggestion id.

This is the charged step of address autocomplete. A successful retrieval decrements your lookup balance. An id which resolves to no address returns `404`.

Every address comes back in one US-shaped format, whatever country or dataset it came from: up to two address lines and US field names such as `zip_code`, `state` and `city`.

## Endpoint

`GET /autocomplete/addresses/{address}/usa`

See the [API reference](https://docs.addresszen.com/docs/api/retrieve-address) for this endpoint.

## Import

```ts
import { retrieveAddress } from "@addresszen/sdk";
```

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `address` | `string` | yes | **ID of address suggestion** ID of address suggestion provided by the API to fully retrieve. |

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `api_key` | `string` | no | **API Key** Your unique identifier that allows access to our APIs. Begins `ak_`. Available from your dashboard. |
| `licensee` | `string` | no | **Licensee Key** Uniquely identifies a licensee. |
| `filter` | `string` | no | **Restrict Result Fields** Comma separated whitelist of address elements to return. E.g. `filter=line_1,line_2,line_3` returns only the `line_1`, `line_2` and `line_3` address elements in your response. |
| `tags` | `string` | no | **Tags** A comma separated list of tags to query over. Useful if you want to specify the circumstances in which the request was made. If you specify multiple tags, the response comprises only requests that satisfy all of them. Searching `"foo,bar"` queries only requests tagged both `"foo"` and `"bar"`. |

## Response Type

```ts
import type { RetrieveAddressResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="retrieve-address.ts"
import { createZenClient, retrieveAddress } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({ apiKey: "ak_test" });
  const { data } = await retrieveAddress({
    client,
    path: { address: "usps_example" },
  });
  return data;
};
```
