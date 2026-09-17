# List Config

**Endpoint:** `GET /keys/{key}/configs`

**Operation ID:** `ListConfigs`

**Tags:** Configs

Returns every configuration stored against a key, oldest first.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used for sensitive operations on your account and API Keys. |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/keys/ak_test/configs' \
  -d 'user_token=uk_secret'
```

**JavaScript**

```javascript
const response = await fetch(
  'https://api.addresszen.com/v1/keys/ak_test/configs?' +
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
    "https://api.addresszen.com/v1/keys/ak_test/configs",
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

uri = URI("https://api.addresszen.com/v1/keys/ak_test/configs")
uri.query = URI.encode_www_form(user_token: "uk_secret")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents(
  "https://api.addresszen.com/v1/keys/ak_test/configs?" .
  http_build_query([
    "user_token" => "uk_secret",
  ])
);
$result = json_decode($response, true)["result"];
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | object | List of configurations |
| `message` | yes | `Success` |  |
| `code` | yes | `2000` |  |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/list-configs)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
