# `resolvePlace`

Resolve Place

Returns the full place for a place ID taken from a `/places` suggestion.

On top of the fields carried by the suggestion, the response adds coordinates, language and the underlying dataset record.

Each request decrements your lookup balance. An unknown ID returns `404`.

## Endpoint

`GET /places/{place}`

See the [API reference](https://docs.addresszen.com/docs/api/resolve-place) for this endpoint.

## Import

```ts
import { resolvePlace } from "@addresszen/sdk";
```

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `place` | `string` | yes | ID of place suggestion |

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `api_key` | `string` | no | **API Key** Your unique identifier that allows access to our APIs. Begins `ak_`. Available from your dashboard. |
| `tags` | `string` | no | **Tags** A comma separated list of tags to query over. Useful if you want to specify the circumstances in which the request was made. If you specify multiple tags, the response comprises only requests that satisfy all of them. Searching `"foo,bar"` queries only requests tagged both `"foo"` and `"bar"`. |

## Response Type

```ts
import type { ResolvePlaceResponse2 } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="resolve-place.ts"
import { createZenClient, resolvePlace } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({ apiKey: "ak_test" });
  const { data } = await resolvePlace({
    client,
    path: { place: "geonames_2643743" },
  });
  return data;
};
```
