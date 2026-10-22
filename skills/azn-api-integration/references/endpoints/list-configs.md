# List Config

**Endpoint:** `GET /keys/{key}/configs`

**Operation ID:** `ListConfigs`

**Tags:** Configs

Returns every configuration stored against a key, oldest first.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used to manage your account and API Keys. It was previously called the user token. |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/keys/ak_test/configs' \
  -d 'user_token=uk_secret'
```

**JavaScript**

```javascript
import { createZenClient, listConfigs } from '@addresszen/sdk';

const client = createZenClient({ apiKey: 'ak_test', userToken: 'uk_secret' });

const { data } = await listConfigs({
  client,
  path: { key: 'ak_test' },
});
```

**Python**

```python
# pip install addresszen
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    result = client.list_configs("ak_test", user_token="uk_secret")
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
