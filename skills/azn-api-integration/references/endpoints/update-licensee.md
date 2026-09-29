# Update Licensee

**Endpoint:** `POST /keys/{key}/licensees/{licensee}`

**Operation ID:** `UpdateLicensee`

**Tags:** Licensees

Updates a licensee's address, postcode, allowed URLs and daily limit. Returns the updated licensee. The name is fixed at creation.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `licensee` | path | yes | string | Uniquely identifies a licensee. |
| `user_token` | query | no | string | A secret key used to manage your account and API Keys. It was previously called the user token. |

## Request Body

Content-Type: `application/json` (required)

| Field | Required | Type | Description |
|---|---|---|---|
| `name` | no | string | Licensee individual or organisation name |
| `address` | no | string | Licensee's first, second and third line address as well as post town concatenated by commas |
| `postcode` | no | string | Licensee's postcode |
| `whitelist` | no | array<string> | A list of allowed URLs. An empty list disables the check. |
| `daily` | no | object |  |

## Request Samples

**curl**

```bash
curl -X POST 'https://api.addresszen.com/v1/keys/ak_test/licensees/sl_ijoiqsxeQgXW2gkiE0X94?user_token=uk_secret' \
  -H 'Content-Type: application/json' \
  -d '{
    "daily": {
      "limit": 20000
    }
  }'
```

**JavaScript**

```javascript
const response = await fetch('https://api.addresszen.com/v1/keys/ak_test/licensees/sl_ijoiqsxeQgXW2gkiE0X94?user_token=uk_secret', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    daily: {
      limit: 20000,
    },
  }),
});

const { result } = await response.json();
```

**Python**

```python
import requests

response = requests.post(
    "https://api.addresszen.com/v1/keys/ak_test/licensees/sl_ijoiqsxeQgXW2gkiE0X94",
    params={"user_token": "uk_secret"},
    json={
        "daily": {
            "limit": 20000,
        },
    },
)
result = response.json()["result"]
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/keys/ak_test/licensees/sl_ijoiqsxeQgXW2gkiE0X94?user_token=uk_secret")
body = {
  daily: {
    limit: 20000,
  },
}
response = Net::HTTP.post(uri, body.to_json, "Content-Type" => "application/json")
result = JSON.parse(response.body)["result"]
```

**PHP**

```php
<?php
$ch = curl_init("https://api.addresszen.com/v1/keys/ak_test/licensees/sl_ijoiqsxeQgXW2gkiE0X94?user_token=uk_secret");
curl_setopt_array($ch, [
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_HTTPHEADER => ["Content-Type: application/json"],
  CURLOPT_POSTFIELDS => json_encode([
    "daily" => [
      "limit" => 20000,
    ],
  ]),
  CURLOPT_RETURNTRANSFER => true,
]);
$result = json_decode(curl_exec($ch), true)["result"];
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | [Licensee](../data/licensee.md) |  |
| `code` | yes | `2000` |  |
| `message` | yes | `Success` |  |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/update-licensee)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
