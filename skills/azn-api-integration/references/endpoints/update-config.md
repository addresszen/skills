# Update Config

**Endpoint:** `POST /keys/{key}/configs/{config}`

**Operation ID:** `UpdateConfig`

**Tags:** Configs

Replaces a configuration's payload and returns the updated configuration. The name is fixed at creation.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `config` | path | yes | string | User-provided configuration object name. |
| `user_token` | query | no | string | A secret key used to manage your account and API Keys. It was previously called the user token. |

## Request Body

Content-Type: `application/json` (required)

| Field | Required | Type | Description |
|---|---|---|---|
| `payload` | no | string | A serialized payload of up to `65536` characters |

## Request Samples

**curl**

```bash
curl -X POST 'https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce?user_token=uk_secret' \
  -H 'Content-Type: application/json' \
  -d '{
    "payload": "{\"removeOrganisation\": true}"
  }'
```

**JavaScript**

```javascript
const response = await fetch('https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce?user_token=uk_secret', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    payload: '{"removeOrganisation": true}',
  }),
});

const { result } = await response.json();
```

**Python**

```python
import requests

response = requests.post(
    "https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce",
    params={"user_token": "uk_secret"},
    json={
        "payload": "{\"removeOrganisation\": true}",
    },
)
result = response.json()["result"]
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce?user_token=uk_secret")
body = {
  payload: '{"removeOrganisation": true}',
}
response = Net::HTTP.post(uri, body.to_json, "Content-Type" => "application/json")
result = JSON.parse(response.body)["result"]
```

**PHP**

```php
<?php
$ch = curl_init("https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce?user_token=uk_secret");
curl_setopt_array($ch, [
  CURLOPT_POST => true,
  CURLOPT_HTTPHEADER => ["Content-Type: application/json"],
  CURLOPT_POSTFIELDS => json_encode([
    "payload" => '{"removeOrganisation": true}',
  ]),
  CURLOPT_RETURNTRANSFER => true,
]);
$result = json_decode(curl_exec($ch), true)["result"];
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

- [Live docs](https://docs.addresszen.com/docs/api/update-config)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
