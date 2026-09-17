# Resolve Place

**Endpoint:** `GET /places/{place}`

**Operation ID:** `ResolvePlace`

**Tags:** Place Search

Returns the full place for a place ID taken from a `/places` suggestion.

On top of the fields carried by the suggestion, the response adds coordinates, language and the underlying dataset record.

Each request decrements your lookup balance. An unknown ID returns `404`.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `place` | path | yes | string | ID of place suggestion |
| `tags` | query | no | string | A comma separated list of tags to query over. |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/places/geonames_5353' \
  -d 'api_key=ak_test'
```

**JavaScript**

```javascript
const response = await fetch(
  'https://api.addresszen.com/v1/places/geonames_5353?' +
  new URLSearchParams({
    api_key: 'ak_test',
  })
);

const { result } = await response.json();
```

**Python**

```python
import requests

response = requests.get(
    "https://api.addresszen.com/v1/places/geonames_5353",
    params={
        "api_key": "ak_test",
    },
)
result = response.json()["result"]
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/places/geonames_5353")
uri.query = URI.encode_www_form(api_key: "ak_test")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents(
  "https://api.addresszen.com/v1/places/geonames_5353?" .
  http_build_query([
    "api_key" => "ak_test",
  ])
);
$result = json_decode($response, true)["result"];
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `code` | yes | `2000` |  |
| `message` | yes | `Success` |  |
| `result` | yes | Place | A geographical place: an administrative division, capital or seat of administration city drawn from GeoNames. `GET /places` returns a suggestion for each match and `GET /places/{place}` resolves a suggestion id to the full place. `native` holds the underlying GeoNames record. |

## Response Example

```json
{
  "result": {
    "id": "geonames_2643743",
    "dataset": "geonames",
    "name": "London",
    "descriptive_name": "London, Greater London, England",
    "language": "en",
    "longitude": -0.12574,
    "latitude": 51.50853,
    "country_iso": "GBR",
    "native": {
      "admin1_code": "ENG",
      "admin2_name": "Greater London",
      "geonameid": 2643743,
      "timezone": "Europe/London",
      "latitude": 51.50853,
      "language": "en",
      "dem": 25,
      "admin4_code": "",
      "admin1_geonameid": 6269131,
      "alternatenames": [
        "ILondon",
        "… 108 more items …"
      ],
      "cc2": [],
      "admin2_code": "GLA",
      "modification_date": "2022-03-09T00:00:00.000Z",
      "asciiname": "London",
      "id": "geonames_2643743",
      "feature_code": "PPLC",
      "country_iso": "GBR",
      "longitude": -0.12574,
      "elevation": null,
      "admin2_geonameid": 2648110,
      "admin1_name": "England",
      "population": "8961989",
      "country_code": "GB",
      "feature_class": "P",
      "name": "London",
      "admin3_code": "",
      "dataset": "geonames"
    }
  },
  "code": 2000,
  "message": "Success"
}
```

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 404 |  | Resource not found |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/resolve-place)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
