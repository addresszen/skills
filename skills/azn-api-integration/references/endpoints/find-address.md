# Find Address

**Endpoint:** `GET /autocomplete/addresses`

**Operation ID:** `FindAddress`

**Tags:** Address Search

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

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `query` | query | no | string | The partial address string entered by the user to autocomplete. |
| `dataset` | query | no | array | Comma-separated list of datasets to search within. |
| `context` | query | no | string | Limits search results, typically within a country. |
| `limit` | query | no | integer | Specifies the maximum number of records to retrieve. |
| `bias_lonlat` | query | no | string | Bias search to a geospatial circle determined by an origin and radius in metres. Max radius is `50000`. |
| `bias_ip` | query | no | `true` | Biases search based on approximate geolocation of IP address. |
| `box` | query | no | string | Restrict search to a geospatial box determined by the "top-left" and "bottom-right" geolocations. |
| `postal_code` | query | no | string | Restrict results to addresses with a matching full postal code. Case, spaces and hyphens are ignored. For US addresses the full postal code is the nine digit ZIP+4 (`941021234`); filter on `postal_code_3` for a five digit ZIP. For UK addresses use `postcode`. |
| `postal_code_2` | query | no | string | Restrict results to addresses whose postal code starts with the given segment. For US addresses this is the three digit ZIP prefix (sectional center), e.g. `941` for San Francisco. |
| `postal_code_3` | query | no | string | Restrict results to addresses with a matching short postal code. For US addresses this is the five digit ZIP code. |
| `city` | query | no | string | Restrict results to addresses in the named city, town or locality. Case, spaces and accents are ignored, so `San Francisco` and `sanfrancisco` match the same addresses. For UK addresses use `post_town`. |
| `state` | query | no | string | Restrict results to addresses in the named state, province or region, e.g. `California`. Case and spaces are ignored. |
| `state_code` | query | no | string | Restrict results to addresses with a matching state or region code, e.g. the two letter USPS state abbreviation `CA`. Case is ignored. |
| `bias_postal_code` | query | no | string | Boost addresses with a matching full postal code (nine digit ZIP+4 for US addresses). Unmatched addresses still appear, ranked lower. |
| `bias_postal_code_2` | query | no | string | Boost addresses whose postal code starts with the given segment (three digit ZIP prefix for US addresses). |
| `bias_postal_code_3` | query | no | string | Boost addresses with a matching short postal code (five digit ZIP for US addresses). |
| `bias_city` | query | no | string | Boost addresses in the named city, town or locality. Case, spaces and accents are ignored. For UK addresses use `bias_posttown`. |
| `bias_state` | query | no | string | Boost addresses in the named state, province or region. |
| `bias_state_code` | query | no | string | Boost addresses with a matching state or region code, e.g. `CA`. |
| `is_pobox` | query | no | `true` \| `false` | `true` restricts results to PO Box addresses; `false` excludes them. For US addresses this is derived from the USPS record type (`P`). |
| `is_business` | query | no | `true` \| `false` | `true` restricts results to business addresses; `false` excludes them. For US addresses this is derived from the USPS record type (`F`, a firm record). |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/autocomplete/addresses' \
  -d 'api_key=ak_test' \
  --data-urlencode 'query=1600 Pennsylvania'
```

**JavaScript**

```javascript
const response = await fetch(
  'https://api.addresszen.com/v1/autocomplete/addresses?' +
  new URLSearchParams({
    api_key: 'ak_test',
    query: '1600 Pennsylvania',
  })
);

const { result } = await response.json();
```

**Python**

```python
import requests

response = requests.get(
    "https://api.addresszen.com/v1/autocomplete/addresses",
    params={
        "api_key": "ak_test",
        "query": "1600 Pennsylvania",
    },
)
result = response.json()["result"]
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/autocomplete/addresses")
uri.query = URI.encode_www_form(api_key: "ak_test", query: "1600 Pennsylvania")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents(
  "https://api.addresszen.com/v1/autocomplete/addresses?" .
  http_build_query([
    "api_key" => "ak_test",
    "query" => "1600 Pennsylvania",
  ])
);
$result = json_decode($response, true)["result"];
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | object |  |
| `code` | yes | `2000` |  |
| `message` | yes | `Success` |  |

## Response Example

```json
{
  "result": {
    "hits": [
      {
        "suggestion": "10 Downing St, Montpelier, VT, 05602",
        "urls": {},
        "id": "usps_V210079628|10||3797"
      },
      "… 9 more items …"
    ]
  },
  "code": 2000,
  "message": "Success"
}
```

## See also

- [Live docs](https://docs.addresszen.com/docs/api/find-address)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
