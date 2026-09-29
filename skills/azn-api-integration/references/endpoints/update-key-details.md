# Update Details

**Endpoint:** `PUT /keys/{key}/details`

**Operation ID:** `UpdateKeyDetails`

**Tags:** Keys

Updates a key's settings and returns its private details. Only the fields you send change. A key on an unlimited plan ignores changes to `datasets`, `daily_limit` and `monthly_limit`.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used to manage your account and API Keys. It was previously called the user token. |

## Request Body

Content-Type: `application/json` (required)

| Field | Required | Type | Description |
|---|---|---|---|
| `name` | no | string | A name for the key |
| `daily_limit` | no | object |  |
| `monthly_limit` | no | object |  |
| `individual_limit` | no | object |  |
| `allowed_urls` | no | array<string> | A list of allowed URLs. An empty list disables the check. Up to 10 allowed. |
| `redact_days` | no | integer | Number of days to preserve personal data stored in your key usage history. Set to 0 to prevent personal data storage |
| `notifications` | no | object |  |
| `ip_forwarding` | no | boolean | Accept IP addresses forwarded in the `AZ-Source-IP` header |
| `datasets` | no | object | Indicates which datasets are available and added by default to the address responses |

## Request Samples

**curl**

```bash
curl -X PUT 'https://api.addresszen.com/v1/keys/ak_test/details?user_token=uk_secret' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "My Updated Key",
    "daily_limit": 1000,
    "notifications": {
      "enabled": true
    }
  }'
```

**JavaScript**

```javascript
const response = await fetch('https://api.addresszen.com/v1/keys/ak_test/details?user_token=uk_secret', {
  method: 'PUT',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    name: 'My Updated Key',
    daily_limit: 1000,
    notifications: {
      enabled: true,
    },
  }),
});

const { result } = await response.json();
```

**Python**

```python
import requests

response = requests.put(
    "https://api.addresszen.com/v1/keys/ak_test/details",
    params={"user_token": "uk_secret"},
    json={
        "name": "My Updated Key",
        "daily_limit": 1000,
        "notifications": {
            "enabled": True,
        },
    },
)
result = response.json()["result"]
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/keys/ak_test/details?user_token=uk_secret")
body = {
  name: "My Updated Key",
  daily_limit: 1000,
  notifications: {
    enabled: true,
  },
}
response = Net::HTTP.put(uri, body.to_json, "Content-Type" => "application/json")
result = JSON.parse(response.body)["result"]
```

**PHP**

```php
<?php
$ch = curl_init("https://api.addresszen.com/v1/keys/ak_test/details?user_token=uk_secret");
curl_setopt_array($ch, [
  CURLOPT_CUSTOMREQUEST => "PUT",
  CURLOPT_HTTPHEADER => ["Content-Type: application/json"],
  CURLOPT_POSTFIELDS => json_encode([
    "name" => "My Updated Key",
    "daily_limit" => 1000,
    "notifications" => [
      "enabled" => true,
    ],
  ]),
  CURLOPT_RETURNTRANSFER => true,
]);
$result = json_decode(curl_exec($ch), true)["result"];
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

- [Live docs](https://docs.addresszen.com/docs/api/update-key-details)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
