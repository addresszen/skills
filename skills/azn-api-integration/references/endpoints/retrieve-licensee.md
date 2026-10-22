# Retrieve Licensee

**Endpoint:** `GET /keys/{key}/licensees/{licensee}`

**Operation ID:** `RetrieveLicensee`

**Tags:** Licensees

Returns a licensee by its `sl_` key. A canceled or unknown licensee returns `404`.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key. Begins `ak_`. |
| `licensee` | path | yes | string | Uniquely identifies a licensee. |
| `user_token` | query | no | string | A secret key used to manage your account and API Keys. It was previously called the user token. |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/keys/ak_test/licensees/sl_ijoiqsxeQgXW2gkiE0X94' \
  -d 'user_token=uk_secret'
```

**JavaScript**

```javascript
import { createZenClient, retrieveLicensee } from '@addresszen/sdk';

const client = createZenClient({ apiKey: 'ak_test', userToken: 'uk_secret' });

const { data } = await retrieveLicensee({
  client,
  path: { key: 'ak_test', licensee: 'sl_ijoiqsxeQgXW2gkiE0X94' },
});
```

**Python**

```python
# pip install addresszen
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    result = client.retrieve_licensee("ak_test", "sl_ijoiqsxeQgXW2gkiE0X94", user_token="uk_secret")
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/keys/ak_test/licensees/sl_ijoiqsxeQgXW2gkiE0X94")
uri.query = URI.encode_www_form(user_token: "uk_secret")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents(
  "https://api.addresszen.com/v1/keys/ak_test/licensees/sl_ijoiqsxeQgXW2gkiE0X94?" .
  http_build_query([
    "user_token" => "uk_secret",
  ])
);
$result = json_decode($response, true)["result"];
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | [Licensee](../data/licensee.md) |  |
| `code` | yes | `2000` |  |
| `message` | yes | `Success` |  |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/retrieve-licensee)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
