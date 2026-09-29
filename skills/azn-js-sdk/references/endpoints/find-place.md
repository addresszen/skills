# `findPlace`

Find Place

Returns place suggestions for a query, ranked by relevance. Places cover countries, administrative areas, capitals and other administrative seats.

## Implementing Place Autocomplete

Retrieving a full place takes two requests:

1. Fetch suggestions from `/places`
2. Fetch the place using the `id` on a suggestion

A query returns at most 10 suggestions. An empty query returns an empty result set. Show users the `descriptive_name`. The API drops suggestions that share one, so each name in a response identifies a single place.

## Rate Limiting and Cost

The rate limit is 3,000 requests per 5 minutes.

`/places` does not decrement your lookup balance, but resolving a suggestion to a full place does. We rate limit and then suspend integrations that repeatedly call `/places` without resolving.

## Endpoint

`GET /places`

See the [API reference](https://docs.addresszen.com/docs/api/find-place) for this endpoint.

## Import

```ts
import { findPlace } from "@addresszen/sdk";
```

## Path Parameters

_None._

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `api_key` | `string` | no | **API Key** Your unique identifier that allows access to our APIs. Begins `ak_`. Available from your dashboard. |
| `query` | `string` | no | Specifies the place to query. Can be shortened to `q=` |
| `country_iso` | `string` | no | **Filter by Country** Filter by country ISO code. Uses 3 letter country code (ISO 3166-1) standard. Filter by multiple countries with a comma separated list. E.g. `GBR,IRL` |
| `bias_country_iso` | `string` | no | **Bias by Country** Bias by country ISO code. Uses 3 letter country code (ISO 3166-1) standard. Bias by multiple countries with a comma separated list. E.g. `GBR,IRL` |
| `bias_lonlat` | `string` | no | **Bias by Geolocation** Bias search to a geospatial circle determined by an origin and radius in meters. Max radius is `50000`. Uses the format bias_lonlat=[longitude],[latitude],[radius in meters]. Only one geospatial bias may be provided. |
| `bias_ip` | `"true"` | no | **Bias by Geolocation of IP** Biases search based on approximate geolocation of IP address. Set `bias_ip=true` to enable. |

## Response Type

```ts
import type { FindPlaceResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="find-place.ts"
import { createZenClient, findPlace } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({ apiKey: "ak_test" });
  const { data } = await findPlace({
    client,
    query: { query: "Springfield" },
  });
  return data;
};
```
