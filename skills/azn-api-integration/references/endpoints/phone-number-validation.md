# Phone Number Validation

**Endpoint:** `GET /phone_numbers`

**Operation ID:** `PhoneNumberValidation`

**Tags:** Phone Numbers

Validates a phone number and returns its country, its national and international formats, and the network it was originally assigned to.

Requires an API Key licensed for phone validation.

Every query decrements your lookup balance, including a number that fails to parse and a number reported as invalid.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `query` | query | yes | string | Specifies the phone number to validate. Phone number must include a country code in an acceptable format. For instance, UK phone numbers should be prefixed with `+44`, `44` or `0044`. |
| `current_carrier` | query | no | `true` | When set to `true`, the API retrieves and populates the current network of the phone number. |
| `tags` | query | no | string | A comma separated list of tags to query over. |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/phone_numbers' \
  -d 'api_key=ak_test' \
  -d 'query=02071128019'
```

**JavaScript**

```javascript
const response = await fetch(
  'https://api.addresszen.com/v1/phone_numbers?' +
  new URLSearchParams({
    api_key: 'ak_test',
    query: '02071128019',
  })
);

const { result } = await response.json();
```

**Python**

```python
import requests

response = requests.get(
    "https://api.addresszen.com/v1/phone_numbers",
    params={
        "api_key": "ak_test",
        "query": "02071128019",
    },
)
result = response.json()["result"]
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/phone_numbers")
uri.query = URI.encode_www_form(api_key: "ak_test", query: "02071128019")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents(
  "https://api.addresszen.com/v1/phone_numbers?" .
  http_build_query([
    "api_key" => "ak_test",
    "query" => "02071128019",
  ])
);
$result = json_decode($response, true)["result"];
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `code` | yes | `2000` |  |
| `message` | yes | `Success` |  |
| `result` | yes | PhoneNumber \| InvalidPhoneNumber |  |

## Response Example

```json
{
  "result": {
    "valid": true,
    "national_format": "020 7112 8019",
    "international_format": "+44 20 7112 8019",
    "iso_country": "GBR",
    "iso_country_2": "GB",
    "country": "United Kingdom",
    "current_carrier": {
      "network_code": null,
      "name": "Invomo Ltd",
      "country": "GB",
      "network_type": "landline"
    },
    "original_carrier": {
      "network_code": null,
      "name": "Invomo Ltd",
      "country": "GB",
      "network_type": "landline"
    }
  },
  "code": 2000,
  "message": "Success"
}
```

## See also

- [Live docs](https://docs.addresszen.com/docs/api/phone-number-validation)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
