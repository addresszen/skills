# `find_place`

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

```python
from addresszen import AddressZen
```

Call `find_place` on the `AddressZen` client. Path parameters are positional; query and body parameters are keyword-only.

## Path Parameters

_None._

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `query` | `str` | yes | Specifies the place to query. Can be shortened to `q=` |
| `country_iso` | `str` | no | **Filter by Country** Filter by country ISO code. Uses 3 letter country code (ISO 3166-1) standard. Filter by multiple countries with a comma separated list. E.g. `GBR,IRL` |
| `bias_country_iso` | `str` | no | **Bias by Country** Bias by country ISO code. Uses 3 letter country code (ISO 3166-1) standard. Bias by multiple countries with a comma separated list. E.g. `GBR,IRL` |
| `bias_lonlat` | `str` | no | **Bias by Geolocation** Bias search to a geospatial circle determined by an origin and radius in meters. Max radius is `50000`. Uses the format bias_lonlat=[longitude],[latitude],[radius in meters]. Only one geospatial bias may be provided. |
| `bias_ip` | `Literal['true'] \| str` | no | **Bias by Geolocation of IP** Biases search based on approximate geolocation of IP address. Set `bias_ip=true` to enable. |

## Response Type

```python
from addresszen.types import FindPlaceResult
```

## Errors

Unsuccessful HTTP responses raise `APIError` or a subclass, with the HTTP `status` and the API error `code` and `message`. Connection failures and timeouts raise `TransportError`. Unexpected responses raise `ProtocolError`. All derive from `ClientError`. See [error handling](https://docs.addresszen.com/docs/sdks/python/errors).

## Example

```python title="find_place.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    places = client.find_place(query="Springfield")
```
