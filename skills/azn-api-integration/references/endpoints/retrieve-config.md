# Retrieve Config

**Endpoint:** `GET /keys/{key}/configs/{config}`

**Operation ID:** `RetrieveConfig`

**Tags:** Configs

Returns a configuration by name. This request needs no `user_token`, so a browser integration can read its own configuration at runtime.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `config` | path | yes | string | User-provided configuration object name. |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce' \
  -d 'user_token=uk_secret'
```

**JavaScript**

```javascript
const response = await fetch(
  'https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce?' +
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
    "https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce",
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

uri = URI("https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce")
uri.query = URI.encode_www_form(user_token: "uk_secret")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents(
  "https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce?" .
  http_build_query([
    "user_token" => "uk_secret",
  ])
);
$result = json_decode($response, true)["result"];
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | [Config](../data/config.md) |  |
| `code` | yes | `2000` |  |
| `message` | yes | `Success` |  |

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 404 |  | Not Found |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/retrieve-config)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
