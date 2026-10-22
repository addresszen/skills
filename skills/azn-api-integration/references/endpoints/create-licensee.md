# Create Licensee

**Endpoint:** `POST /keys/{key}/licensees`

**Operation ID:** `CreateLicensee`

**Tags:** Licensees

Creates a licensee on a key and returns it with its generated `sl_` key. The key must be enabled for sub-licensing.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key. Begins `ak_`. |
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
curl -X POST 'https://api.addresszen.com/v1/keys/ak_test/licensees?user_token=uk_secret' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Qwerty Widgets Limited",
    "address": "12 High Street, Manchester",
    "postcode": "BR8 7RE",
    "whitelist": [],
    "daily": {
      "limit": 10000
    }
  }'
```

**JavaScript**

```javascript
import { createZenClient, createLicensee } from '@addresszen/sdk';

const client = createZenClient({ apiKey: 'ak_test', userToken: 'uk_secret' });

const { data } = await createLicensee({
  client,
  path: { key: 'ak_test' },
  body: {
    name: 'Qwerty Widgets Limited',
    address: '12 High Street, Manchester',
    postcode: 'BR8 7RE',
    whitelist: [],
    daily: {
      limit: 10000,
    },
  },
});
```

**Python**

```python
# pip install addresszen
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    result = client.create_licensee(
        "ak_test",
        user_token="uk_secret",
        name="Qwerty Widgets Limited",
        address="12 High Street, Manchester",
        postcode="BR8 7RE",
        whitelist=[],
        daily={"limit": 10000},
    )
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/keys/ak_test/licensees?user_token=uk_secret")
body = {
  name: "Qwerty Widgets Limited",
  address: "12 High Street, Manchester",
  postcode: "BR8 7RE",
  whitelist: [],
  daily: {
    limit: 10000,
  },
}
response = Net::HTTP.post(uri, body.to_json, "Content-Type" => "application/json")
result = JSON.parse(response.body)["result"]
```

**PHP**

```php
<?php
$ch = curl_init("https://api.addresszen.com/v1/keys/ak_test/licensees?user_token=uk_secret");
curl_setopt_array($ch, [
  CURLOPT_POST => true,
  CURLOPT_HTTPHEADER => ["Content-Type: application/json"],
  CURLOPT_POSTFIELDS => json_encode([
    "name" => "Qwerty Widgets Limited",
    "address" => "12 High Street, Manchester",
    "postcode" => "BR8 7RE",
    "whitelist" => [],
    "daily" => [
      "limit" => 10000,
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

- [Live docs](https://docs.addresszen.com/docs/api/create-licensee)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
