# `client.find_address`

Find Address

Returns address suggestions for a partial address, ranked by relevance. Use it to autofill an address form as the user types.

A suggestion is a display label and an `id`, not a full address. Retrieve the address with a second request to `/autocomplete/addresses/{id}/usa`. That second request is the one which decrements your lookup balance.

Autocomplete is not a free standalone resource. We rate limit, then suspend, keys that autocomplete without resolving suggestions.

Our address autocomplete JavaScript libraries add this to a form without calling the API directly.

## Coverage

Each search runs in one country, selected with `context`. A missing or unrecognized `context` falls back to your account default. Results come from the datasets enabled on your key: USPS ZIP+4 for the US and its territories, and the country datasets you license elsewhere. Where a key has more than one dataset for a country, `dataset` narrows the search.

## Filters

Filters restrict results, e.g. `state_code=NY` searches New York only. A filter which matches no address returns an empty set. An unrecognized filter name is ignored. Neither affects your lookup balance.

Filters combine with `AND` logic, so `state_code=CA&city=San Francisco` requires both. A comma-separated value combines terms for one filter, e.g. `postal_code_3=11225,11226,11238` accepts any of the three ZIP codes. Unless a parameter states otherwise, every filter takes multiple terms. The maximum is 10 filter terms.

## Address bias

Bias terms carry the `bias_` prefix and promote addresses rather than restricting the set, so unmatched addresses still appear, lower down. For example, `bias_state_code=NY,NJ` favors addresses in New York and New Jersey, and `bias_lonlat` favors addresses near a point. Invalid bias terms have no effect. Multiple bias terms are allowed unless stated otherwise, with a combined maximum of 5.

## Suggestion format

The suggestion string is subject to change. Present it to the user as it arrives rather than parsing it.

## Rate limiting and cost

The default rate limit is 3,000 requests per 5 minutes, counted per API key and IP address. The `X-RateLimit-Limit`, `X-RateLimit-Remaining` and `X-RateLimit-Reset` headers report the current window.

Autocomplete requests do not draw on your balance. Resolving a suggestion to a full address does.

## Endpoint

`GET /autocomplete/addresses`

See the [API reference](https://docs.addresszen.com/docs/api/find-address) for this endpoint.

## Signature

```ruby
def find_address(
  query: nil,
  dataset: nil,
  context: nil,
  limit: nil,
  bias_lonlat: nil,
  bias_ip: nil,
  box: nil,
  postal_code: nil,
  postal_code_2: nil,
  postal_code_3: nil,
  city: nil,
  state: nil,
  state_code: nil,
  bias_postal_code: nil,
  bias_postal_code_2: nil,
  bias_postal_code_3: nil,
  bias_city: nil,
  bias_state: nil,
  bias_state_code: nil,
  is_pobox: nil,
  is_business: nil
)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `keywords` | `keyword arguments` | no | One per [query parameter](#query-parameters), named as the API names them. A keyword left out or `nil` is not sent. |

## Query Parameters

Pass these as keyword arguments.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `query` | `String` | no | Address Query |
| `dataset` | `Array<String>` | no | Filter by Dataset |
| `context` | `String` | no | Context |
| `limit` | `Integer` | no | Limit |
| `bias_lonlat` | `String` | no | Bias by Geolocation |
| `bias_ip` | `String` | no | Bias by Geolocation of IP |
| `box` | `String, Array<String>` | no | Filter by Bounding Box |
| `postal_code` | `String` | no | Filter by postal code |
| `postal_code_2` | `String` | no | Filter by postal code prefix |
| `postal_code_3` | `String` | no | Filter by short postal code |
| `city` | `String` | no | Filter by city |
| `state` | `String` | no | Filter by state |
| `state_code` | `String` | no | Filter by state code |
| `bias_postal_code` | `String` | no | Bias by postal code |
| `bias_postal_code_2` | `String` | no | Bias by postal code prefix |
| `bias_postal_code_3` | `String` | no | Bias by short postal code |
| `bias_city` | `String` | no | Bias by city |
| `bias_state` | `String` | no | Bias by state |
| `bias_state_code` | `String` | no | Bias by state code |
| `is_pobox` | `String` | no | Filter by PO Box |
| `is_business` | `String` | no | Filter by business address |

## Response

`AddressZen::Responses::AutocompleteResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="find-address.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")

response = client.find_address(query: "1010 Cauthen Ln", limit: 5)

response.result.hits.each do |hit|
  puts "#{hit.id}: #{hit.suggestion}"
end
```
