# Usage Stats

**Endpoint:** `GET /keys/{key}/usage`

**Operation ID:** `KeyUsage`

**Tags:** Keys

Reports the number of lookups a key consumed over a date range, as a total and a daily breakdown.

The range defaults to the last 21 days. `start` and `end` take UNIX timestamps in milliseconds, and `end` defaults to the current time. The maximum range is 90 days.

Query at most three tags at once.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used to manage your account and API Keys. It was previously called the user token. |
| `start` | query | no | integer | A start date/time in the form of a UNIX Timestamp in milliseconds. E.g. `1418556452651` |
| `end` | query | no | integer | An end date/time in the form of a UNIX Timestamp in milliseconds. E.g.  `1418556477882` |
| `tags` | query | no | string | A comma separated list of tags to query over. |
| `licensee` | query | no | string | Uniquely identifies a licensee. |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/keys/ak_test/usage' \
  -d 'user_token=uk_secret'
```

**JavaScript**

```javascript
const response = await fetch(
  'https://api.addresszen.com/v1/keys/ak_test/usage?' +
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
    "https://api.addresszen.com/v1/keys/ak_test/usage",
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

uri = URI("https://api.addresszen.com/v1/keys/ak_test/usage")
uri.query = URI.encode_www_form(user_token: "uk_secret")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents(
  "https://api.addresszen.com/v1/keys/ak_test/usage?" .
  http_build_query([
    "user_token" => "uk_secret",
  ])
);
$result = json_decode($response, true)["result"];
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | KeyUsageResult |  |
| `code` | yes | `2000` |  |
| `message` | yes | `Success` |  |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/key-usage)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
