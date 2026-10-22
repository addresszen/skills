# Create Config

**Endpoint:** `POST /keys/{key}/configs`

**Operation ID:** `CreateConfig`

**Tags:** Configs

Creates a named configuration on a key and returns it.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used to manage your account and API Keys. It was previously called the user token. |

## Request Body

Content-Type: `application/json` (required)

| Field | Required | Type | Description |
|---|---|---|---|
| `name` | yes | string | A unique name to identify the configuration payload |
| `payload` | yes | string | A serialized payload of up to `65536` characters |

## Request Samples

**curl**

```bash
curl -X POST 'https://api.addresszen.com/v1/keys/ak_test/configs?user_token=uk_secret' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "woocommerce",
    "payload": "{\"removeOrganisation\": false}"
  }'
```

**JavaScript**

```javascript
import { createZenClient, createConfig } from '@addresszen/sdk';

const client = createZenClient({ apiKey: 'ak_test', userToken: 'uk_secret' });

const { data } = await createConfig({
  client,
  path: { key: 'ak_test' },
  body: {
    name: 'woocommerce',
    payload: '{"removeOrganisation": false}',
  },
});
```

**Python**

```python
# pip install addresszen
import json

from addresszen import AddressZen

with AddressZen("ak_test") as client:
    result = client.create_config(
        "ak_test",
        user_token="uk_secret",
        name="woocommerce",
        payload=json.dumps({"removeOrganisation": False}),
    )
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/keys/ak_test/configs?user_token=uk_secret")
body = {
  name: "woocommerce",
  payload: '{"removeOrganisation": false}',
}
response = Net::HTTP.post(uri, body.to_json, "Content-Type" => "application/json")
result = JSON.parse(response.body)["result"]
```

**PHP**

```php
<?php
$ch = curl_init("https://api.addresszen.com/v1/keys/ak_test/configs?user_token=uk_secret");
curl_setopt_array($ch, [
  CURLOPT_POST => true,
  CURLOPT_HTTPHEADER => ["Content-Type: application/json"],
  CURLOPT_POSTFIELDS => json_encode([
    "name" => "woocommerce",
    "payload" => '{"removeOrganisation": false}',
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

## See also

- [Live docs](https://docs.addresszen.com/docs/api/create-config)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
