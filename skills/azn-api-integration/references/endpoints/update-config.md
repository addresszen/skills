# Update Config

**Endpoint:** `POST /keys/{key}/configs/{config}`

**Operation ID:** `UpdateConfig`

**Tags:** Configs

Replaces a configuration's payload and returns the updated configuration. The name is fixed at creation.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key. Begins `ak_`. |
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
import { createZenClient, updateConfig } from '@addresszen/sdk';

const client = createZenClient({ apiKey: 'ak_test', userToken: 'uk_secret' });

const { data } = await updateConfig({
  client,
  path: { key: 'ak_test', config: 'woocommerce' },
  body: {
    payload: '{"removeOrganisation": true}',
  },
});
```

**Python**

```python
# pip install addresszen
import json

from addresszen import AddressZen

with AddressZen("ak_test") as client:
    result = client.update_config(
        "ak_test",
        "woocommerce",
        user_token="uk_secret",
        payload=json.dumps({"removeOrganisation": True}),
    )
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
