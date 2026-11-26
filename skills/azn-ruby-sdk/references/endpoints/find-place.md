# `client.find_place`

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

## Signature

```ruby
def find_place(query: nil, country_iso: nil, bias_country_iso: nil, bias_lonlat: nil, bias_ip: nil)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `keywords` | `keyword arguments` | no | One per [query parameter](#query-parameters), named as the API names them. A keyword left out or `nil` is not sent. |

## Query Parameters

Pass these as keyword arguments.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `query` | `String` | no | Specifies the place to query. Can be shortened to `q=` |
| `country_iso` | `String, Array<String>` | no | Filter by Country |
| `bias_country_iso` | `String, Array<String>` | no | Bias by Country Bias by country ISO code. Uses 3 letter country code (ISO 3166-1) standard. Bias by multiple countries with a comma separated list. E.g. `GBR,IRL` |
| `bias_lonlat` | `String` | no | Bias by Geolocation |
| `bias_ip` | `String` | no | Bias by Geolocation of IP |

## Response

`AddressZen::Responses::PlaceResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="find-place.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")

response = client.find_place(query: "Springfield", country_iso: "USA")

response.result.hits.each do |place|
  puts "#{place.id}: #{place.descriptive_name}"
end
```
