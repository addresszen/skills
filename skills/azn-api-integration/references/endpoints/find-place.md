# Find Place

**Endpoint:** `GET /places`

**Operation ID:** `FindPlace`

**Tags:** Place Search

Returns place suggestions for a query, ranked by relevance. Places cover countries, administrative areas, capitals and other administrative seats.

## Implementing Place Autocomplete

Retrieving a full place takes two requests:

1. Fetch suggestions from `/places`
2. Fetch the place using the `id` on a suggestion

A query returns at most 10 suggestions. An empty query returns an empty result set. Show users the `descriptive_name`. The API drops suggestions that share one, so each name in a response identifies a single place.

## Rate Limiting and Cost

The rate limit is 3,000 requests per 5 minutes.

`/places` does not decrement your lookup balance, but resolving a suggestion to a full place does. We rate limit and then suspend integrations that repeatedly call `/places` without resolving.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `query` | query | no | string | Specifies the place to query. Can be shortened to `q=` |
| `country_iso` | query | no | string | Filter by country ISO code. Uses 3 letter country code (ISO 3166-1) standard. |
| `bias_country_iso` | query | no | string | Bias by country ISO code. Uses 3 letter country code (ISO 3166-1) standard. |
| `bias_lonlat` | query | no | string | Bias search to a geospatial circle determined by an origin and radius in meters. Max radius is `50000`. |
| `bias_ip` | query | no | `true` | Biases search based on approximate geolocation of IP address. |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/places' \
  -d 'api_key=ak_test' \
  -d 'query=london'
```

**JavaScript**

```javascript
const response = await fetch(
  'https://api.addresszen.com/v1/places?' +
  new URLSearchParams({
    api_key: 'ak_test',
    query: 'london',
  })
);

const { result } = await response.json();
```

**Python**

```python
import requests

response = requests.get(
    "https://api.addresszen.com/v1/places",
    params={
        "api_key": "ak_test",
        "query": "london",
    },
)
result = response.json()["result"]
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/places")
uri.query = URI.encode_www_form(api_key: "ak_test", query: "london")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents(
  "https://api.addresszen.com/v1/places?" .
  http_build_query([
    "api_key" => "ak_test",
    "query" => "london",
  ])
);
$result = json_decode($response, true)["result"];
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `code` | yes | `2000` |  |
| `message` | yes | `Success` |  |
| `result` | yes | object |  |

## Response Example

```json
{
  "result": {
    "hits": [
      {
        "id": "geonames_2643743",
        "name": "London",
        "descriptive_name": "London, Greater London, England",
        "country_iso": "GBR"
      },
      "… 2 more items …"
    ]
  },
  "code": 2000,
  "message": "Success"
}
```

## See also

- [Live docs](https://docs.addresszen.com/docs/api/find-place)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
