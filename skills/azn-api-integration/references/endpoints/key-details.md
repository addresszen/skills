# Details

**Endpoint:** `GET /keys/{key}/details`

**Operation ID:** `KeyDetails`

**Tags:** Keys

Returns private data on a key: remaining lookups, licensed datasets, usage limits, notification settings and the search contexts the key can serve.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used for sensitive operations on your account and API Keys. |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/keys/ak_test/details' \
  -d 'user_token=uk_secret'
```

**JavaScript**

```javascript
const response = await fetch(
  'https://api.addresszen.com/v1/keys/ak_test/details?' +
  new URLSearchParams({
    user_token: 'uk_secret',
  })
);

const { result } = await response.json();
```

**Python**

```python
import requests

response = requests.get(
    "https://api.addresszen.com/v1/keys/ak_test/details",
    params={
        "user_token": "uk_secret",
    },
)
result = response.json()["result"]
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/keys/ak_test/details")
uri.query = URI.encode_www_form(user_token: "uk_secret")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents(
  "https://api.addresszen.com/v1/keys/ak_test/details?" .
  http_build_query([
    "user_token" => "uk_secret",
  ])
);
$result = json_decode($response, true)["result"];
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | ApiKeyDetails |  |
| `code` | yes | `2000` |  |
| `message` | yes | `Success` |  |

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 404 |  | Resource not found |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/key-details)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
