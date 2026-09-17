# Retrieve Address

**Endpoint:** `GET /autocomplete/addresses/{address}/usa`

**Operation ID:** `RetrieveAddress`

**Tags:** Address Search

Returns the full address for an autocomplete suggestion id.

This is the charged step of address autocomplete. A successful retrieval decrements your lookup balance. An id which resolves to no address returns `404`.

Every address comes back in one US-shaped format, whatever country or dataset it came from: up to two address lines and US field names such as `zip_code`, `state` and `city`.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `address` | path | yes | string | ID of address suggestion provided by the API to fully retrieve. |
| `licensee` | query | no | string | Uniquely identifies a licensee. |
| `filter` | query | no | string | Comma separated whitelist of address elements to return. |
| `tags` | query | no | string | A comma separated list of tags to query over. |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/autocomplete/addresses/usps_Z222446599|1||1101/usa' \
  -d 'api_key=ak_test'
```

**JavaScript**

```javascript
const response = await fetch(
  'https://api.addresszen.com/v1/autocomplete/addresses/usps_Z222446599%7C1%7C%7C1101/usa?' +
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
    "https://api.addresszen.com/v1/autocomplete/addresses/usps_Z222446599%7C1%7C%7C1101/usa",
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

uri = URI("https://api.addresszen.com/v1/autocomplete/addresses/usps_Z222446599%7C1%7C%7C1101/usa")
uri.query = URI.encode_www_form(api_key: "ak_test")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents(
  "https://api.addresszen.com/v1/autocomplete/addresses/usps_Z222446599%7C1%7C%7C1101/usa?" .
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
| `result` | yes | [Address](../data/address.md) | A single address. |

## Response Example

```json
{
  "code": 2000,
  "message": "Success",
  "result": {
    "id": "usps_V124884241|1040||0001",
    "dataset": "usps",
    "country": "United States",
    "country_iso": "USA",
    "country_iso_2": "US",
    "language": "en",
    "primary_number": "1040",
    "secondary_number": "",
    "plus_4_code": "0001",
    "line_1": "1040 Waverly Ave",
    "line_2": "",
    "last_line": "Holtsville NY 00501-0001",
    "zip_code": "00501",
    "zip_plus_4_code": "00501-0001",
    "update_key_number": "V124884241",
    "record_type_code": "S",
    "carrier_route_id": "C000",
    "street_pre_directional_abbreviation": "",
    "street_name": "Waverly",
    "street_suffix_abbreviation": "Ave",
    "street_post_directional_abbreviation": "",
    "building_or_firm_name": "",
    "address_secondary_abbreviation": "",
    "base_alternate_code": "B",
    "lacs_status_indicator": "",
    "government_building_indicator": "",
    "state_abbreviation": "NY",
    "state": "New York",
    "municipality_city_state_key": "",
    "urbanization_city_state_key": "",
    "preferred_last_line_city_state_key": "V13916",
    "county": "Suffolk",
    "city": "Holtsville",
    "city_abbreviation": "",
    "preferred_city": "Holtsville",
    "city_state_name_facility_code": "P",
    "zip_classification_code": "U",
    "city_state_mailing_name_indicator": "Y",
    "carrier_route_rate_sortation": "C",
    "finance_number": 353910,
    "congressional_district_number": 2,
    "county_number": 103
  }
}
```

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 404 |  | Resource not found |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/retrieve-address)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
