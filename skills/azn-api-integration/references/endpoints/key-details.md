# Details

**Endpoint:** `GET /keys/{key}/details`

**Operation ID:** `KeyDetails`

**Tags:** Keys

Returns private data on a key: remaining lookups, licensed datasets, usage limits, notification settings and the search contexts the key can serve.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used to manage your account and API Keys. It was previously called the user token. |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/keys/ak_test/details' \
  -d 'user_token=uk_secret'
```

**JavaScript**

```javascript
import { createZenClient, keyDetails } from '@addresszen/sdk';

const client = createZenClient({ apiKey: 'ak_test', userToken: 'uk_secret' });

const { data } = await keyDetails({
  client,
  path: { key: 'ak_test' },
});
```

**Python**

```python
# pip install addresszen
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    result = client.key_details("ak_test", user_token="uk_secret")
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/keys/ak_test/details")
uri.query = URI.encode_www_form(user_token: "uk_secret")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents(
  "https://api.addresszen.com/v1/keys/ak_test/details?" .
  http_build_query([
    "user_token" => "uk_secret",
  ])
);
$result = json_decode($response, true)["result"];
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

- [Live docs](https://docs.addresszen.com/docs/api/key-details)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
