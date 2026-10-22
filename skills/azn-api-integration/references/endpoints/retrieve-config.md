# Retrieve Config

**Endpoint:** `GET /keys/{key}/configs/{config}`

**Operation ID:** `RetrieveConfig`

**Tags:** Configs

Returns a configuration by name. This request needs no `user_token`, so a browser integration can read its own configuration at runtime.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key. Begins `ak_`. |
| `config` | path | yes | string | User-provided configuration object name. |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce' \
  -d 'user_token=uk_secret'
```

**JavaScript**

```javascript
import { createZenClient, retrieveConfig } from '@addresszen/sdk';

const client = createZenClient({ apiKey: 'ak_test' });

const { data } = await retrieveConfig({
  client,
  path: { key: 'ak_test', config: 'woocommerce' },
});
```

**Python**

```python
# pip install addresszen
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    result = client.retrieve_config("ak_test", "woocommerce")
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
