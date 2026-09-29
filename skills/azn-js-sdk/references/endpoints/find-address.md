# `findAddress`

Find Address

Returns address suggestions for a partial address, ranked by relevance. Use it to autofill an address form as the user types.

A suggestion is a display label and an `id`, not a full address. Retrieve the address with a second request to `/autocomplete/addresses/{id}/usa`. That second request is the one which decrements your lookup balance.

Autocomplete is not a free standalone resource. We rate limit, then suspend, keys that autocomplete without resolving suggestions.

Our address autocomplete JavaScript libraries add this to a form without calling the API directly.

## Coverage

Each search runs in one country, selected with `context`. A missing or unrecognized `context` falls back to your account default. Results come from the datasets enabled on your key: USPS Zip+4 for the US and its territories, and the country datasets you license elsewhere. Where a key has more than one dataset for a country, `dataset` narrows the search.

## Filters

Filters restrict results, e.g. `state_code=NY` searches New York only. A filter which matches no address returns an empty set. An unrecognized filter name is ignored. Neither affects your lookup balance.

Filters combine with `AND` logic, so `state_code=CA&city=San Francisco` requires both. A comma-separated value combines terms for one filter, e.g. `postal_code_3=11225,11226,11238` accepts any of the three ZIP codes. Unless a parameter states otherwise, every filter takes multiple terms. The maximum is 10 filter terms.

## Address bias

Bias terms carry the `bias_` prefix and promote addresses rather than restricting the set, so unmatched addresses still appear, lower down. For example, `bias_state_code=NY,NJ` favors addresses in New York and New Jersey, `bias_lonlat` favors addresses near a point. Invalid bias terms have no effect. Multiple bias terms are allowed unless stated otherwise, with a combined maximum of 5.

## Suggestion format

The suggestion string is subject to change. Present it to the user as it arrives rather than parsing it.

## Rate limiting and cost

The default rate limit is 3,000 requests per 5 minutes, counted per API key and IP address. The `X-RateLimit-Limit`, `X-RateLimit-Remaining` and `X-RateLimit-Reset` headers report the current window.

Autocomplete requests do not draw on your balance. Resolving a suggestion to a full address does.

## Endpoint

`GET /autocomplete/addresses`

See the [API reference](https://docs.addresszen.com/docs/api/find-address) for this endpoint.

## Import

```ts
import { findAddress } from "@addresszen/sdk";
```

## Path Parameters

_None._

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `api_key` | `string` | no | **API Key** Your unique identifier that allows access to our APIs. Begins `ak_`. Available from your dashboard. |
| `query` | `string` | no | **Address Query** The partial address string entered by the user to autocomplete. |
| `dataset` | `Array<Dataset>` | no | **Filter by Dataset** Comma-separated list of datasets to search within. Filters results to only include addresses from the specified datasets. Useful for keys with multiple overlapping datasets enabled (e.g. `paf` and `abp`). |
| `context` | `string` | no | **Context** Limits search results, typically within a country. |
| `limit` | `number` | no | **Limit** Specifies the maximum number of records to retrieve. By default the limit is 10. Requesting a larger result set adds latency. |
| `bias_lonlat` | `string` | no | **Bias by Geolocation** Bias search to a geospatial circle determined by an origin and radius in meters. Max radius is `50000`. Uses the format bias_lonlat=[longitude],[latitude],[radius in meters]. Only one geospatial bias may be provided. |
| `bias_ip` | `"true"` | no | **Bias by Geolocation of IP** Biases search based on approximate geolocation of IP address. Set `bias_ip=true` to enable. |
| `box` | `string` | no | **Filter by Bounding Box** Restrict search to a geospatial box determined by the "top-left" and "bottom-right" geolocations. Supply 4 comma separated values ordered `top_left_lon,top_left_lat,bottom_right_lon,bottom_right_lat`. The top-left longitude must be less than the bottom-right longitude, and the top-left latitude greater than the bottom-right latitude. A box which fails either check is ignored. Only one geospatial box can be provided. |
| `postal_code` | `string` | no | **Filter by postal code** Restrict results to addresses with a matching full postal code. Case, spaces and hyphens are ignored. For US addresses the full postal code is the nine digit ZIP+4 (`941021234`); filter on `postal_code_3` for a five digit ZIP. For UK addresses use `postcode`. |
| `postal_code_2` | `string` | no | **Filter by postal code prefix** Restrict results to addresses whose postal code starts with the given segment. For US addresses this is the three digit ZIP prefix (sectional center), e.g. `941` for San Francisco. |
| `postal_code_3` | `string` | no | **Filter by short postal code** Restrict results to addresses with a matching short postal code. For US addresses this is the five digit ZIP code. |
| `city` | `string` | no | **Filter by city** Restrict results to addresses in the named city, town or locality. Case, spaces and accents are ignored, so `San Francisco` and `sanfrancisco` match the same addresses. For UK addresses use `post_town`. |
| `state` | `string` | no | **Filter by state** Restrict results to addresses in the named state, province or region, e.g. `California`. Case and spaces are ignored. |
| `state_code` | `string` | no | **Filter by state code** Restrict results to addresses with a matching state or region code, e.g. the two letter USPS state abbreviation `CA`. Case is ignored. |
| `bias_postal_code` | `string` | no | **Bias by postal code** Boost addresses with a matching full postal code (nine digit ZIP+4 for US addresses). Unmatched addresses still appear, ranked lower. |
| `bias_postal_code_2` | `string` | no | **Bias by postal code prefix** Boost addresses whose postal code starts with the given segment (three digit ZIP prefix for US addresses). |
| `bias_postal_code_3` | `string` | no | **Bias by short postal code** Boost addresses with a matching short postal code (five digit ZIP for US addresses). |
| `bias_city` | `string` | no | **Bias by city** Boost addresses in the named city, town or locality. Case, spaces and accents are ignored. For UK addresses use `bias_posttown`. |
| `bias_state` | `string` | no | **Bias by state** Boost addresses in the named state, province or region. |
| `bias_state_code` | `string` | no | **Bias by state code** Boost addresses with a matching state or region code, e.g. `CA`. |
| `is_pobox` | `"true" \| "false"` | no | **Filter by PO Box** `true` restricts results to PO Box addresses; `false` excludes them. For US addresses this is derived from the USPS record type (`P`). |
| `is_business` | `"true" \| "false"` | no | **Filter by business address** `true` restricts results to business addresses; `false` excludes them. For US addresses this is derived from the USPS record type (`F`, a firm record). |

## Response Type

```ts
import type { FindAddressResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="find-address.ts"
import { createZenClient, findAddress } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({ apiKey: "ak_test" });
  const { data } = await findAddress({
    client,
    query: { query: "123 Main St" },
  });
  return data;
};
```
