# List Licensee

**Endpoint:** `GET /keys/{key}/licensees`

**Operation ID:** `ListLicensees`

**Tags:** Licensees

Returns a key's licensees, oldest first, up to 100 per request. The list omits canceled licensees. The key must be enabled for sub-licensing.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `starting_after` | query | no | integer | ID of the licensee after which to list results |
| `user_token` | query | no | string | A secret key used to manage your account and API Keys. It was previously called the user token. |
| `limit` | query | no | integer | Specifies the maximum number of records to retrieve. |
| `query` | query | no | string | Filter results by licensee name. Can be shortened to `q=` |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/keys/ak_test/licensees' \
  -d 'user_token=uk_secret'
```

**JavaScript**

```javascript
const response = await fetch(
  'https://api.addresszen.com/v1/keys/ak_test/licensees?' +
  new URLSearchParams({
    user_token: 'uk_secret',
  })
);

const { result } = await response.json();
```

**Python**

```python
import requests

response = requests.get(
    "https://api.addresszen.com/v1/keys/ak_test/licensees",
    params={
        "user_token": "uk_secret",
    },
)
result = response.json()["result"]
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/keys/ak_test/licensees")
uri.query = URI.encode_www_form(user_token: "uk_secret")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents(
  "https://api.addresszen.com/v1/keys/ak_test/licensees?" .
  http_build_query([
    "user_token" => "uk_secret",
  ])
);
$result = json_decode($response, true)["result"];
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | object | List of licensees |
| `message` | yes | `Success` |  |
| `code` | yes | `2000` |  |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/list-licensees)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
