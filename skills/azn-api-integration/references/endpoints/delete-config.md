# Delete Config

**Endpoint:** `DELETE /keys/{key}/configs/{config}`

**Operation ID:** `DeleteConfig`

**Tags:** Configs

Permanently deletes a configuration object.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `config` | path | yes | string | User-provided configuration object name. |
| `user_token` | query | no | string | A secret key used to manage your account and API Keys. It was previously called the user token. |

## Request Samples

**curl**

```bash
curl -X DELETE 'https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce?user_token=uk_secret'
```

**JavaScript**

```javascript
const response = await fetch('https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce?user_token=uk_secret', {
  method: 'DELETE',
});
```

**Python**

```python
import requests

response = requests.delete(
    "https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce",
    params={"user_token": "uk_secret"},
)
response.raise_for_status()
```

**Ruby**

```ruby
require "net/http"

uri = URI("https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce?user_token=uk_secret")
Net::HTTP.start(uri.host, use_ssl: true) do |http|
  http.delete(uri.request_uri)
end
```

**PHP**

```php
<?php
$ch = curl_init("https://api.addresszen.com/v1/keys/ak_test/configs/woocommerce?user_token=uk_secret");
curl_setopt_array($ch, [
  CURLOPT_CUSTOMREQUEST => "DELETE",
  CURLOPT_RETURNTRANSFER => true,
]);
curl_exec($ch);
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | object |  |
| `code` | yes | `2000` |  |
| `message` | yes | `Success` |  |

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 404 |  | Not Found |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/delete-config)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
