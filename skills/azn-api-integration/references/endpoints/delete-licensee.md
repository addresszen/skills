# Cancel Licensee

**Endpoint:** `DELETE /keys/{key}/licensees/{licensee}`

**Operation ID:** `DeleteLicensee`

**Tags:** Licensees

Cancels a licensee. Its key stops working and it drops out of the licensee list. Contact us to reverse it.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `licensee` | path | yes | string | Uniquely identifies a licensee. |
| `user_token` | query | no | string | A secret key used to manage your account and API Keys. It was previously called the user token. |

## Request Samples

**curl**

```bash
curl -X DELETE 'https://api.addresszen.com/v1/keys/ak_test/licensees/sl_ijoiqsxeQgXW2gkiE0X94?user_token=uk_secret'
```

**JavaScript**

```javascript
const response = await fetch('https://api.addresszen.com/v1/keys/ak_test/licensees/sl_ijoiqsxeQgXW2gkiE0X94?user_token=uk_secret', {
  method: 'DELETE',
});
```

**Python**

```python
import requests

response = requests.delete(
    "https://api.addresszen.com/v1/keys/ak_test/licensees/sl_ijoiqsxeQgXW2gkiE0X94",
    params={"user_token": "uk_secret"},
)
response.raise_for_status()
```

**Ruby**

```ruby
require "net/http"

uri = URI("https://api.addresszen.com/v1/keys/ak_test/licensees/sl_ijoiqsxeQgXW2gkiE0X94?user_token=uk_secret")
Net::HTTP.start(uri.host, use_ssl: true) do |http|
  http.delete(uri.request_uri)
end
```

**PHP**

```php
<?php
$ch = curl_init("https://api.addresszen.com/v1/keys/ak_test/licensees/sl_ijoiqsxeQgXW2gkiE0X94?user_token=uk_secret");
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

## See also

- [Live docs](https://docs.addresszen.com/docs/api/delete-licensee)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
