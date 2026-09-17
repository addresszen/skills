# Logs (CSV)

**Endpoint:** `GET /keys/{key}/lookups`

**Operation ID:** `KeyLogs`

**Tags:** Keys

Returns a CSV of the charged lookups made on a key, one row per request.

Requires the `user_token` for the account. The maximum interval is 90 days. Without a start or end date the interval is the last 21 days.

The response is `text/csv` and downloads as an attachment. A non-200 response reverts to JSON, with the error code and message in the body.

## CSV format

The CSV has no header row. Columns, in order:

1. Timestamp (ISO 8601)
2. IP address the request was received from
3. Search term
4. URL the request originated from
5. Lookup type
6. Tags
7. Lookups consumed
8. Licensee name (sublicensing keys only)
9. Source IP address

The source IP column carries the address forwarded in the `AZ-Source-IP` header. We record it only for keys with IP address forwarding enabled, and only when the header holds a valid IP address. It is empty otherwise.

## Data redaction

We redact personally identifiable data (PII) in your usage log weekly, covering the IP, source IP, search term and URL columns.

The default retention is 28 days. Change the period from your dashboard. Set it to `0` days to stop collecting PII altogether.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used for sensitive operations on your account and API Keys. |
| `start` | query | no | integer | A start date/time in the form of a UNIX Timestamp in milliseconds. E.g. `1418556452651` |
| `end` | query | no | integer | An end date/time in the form of a UNIX Timestamp in milliseconds. E.g.  `1418556477882` |
| `licensee` | query | no | string | Uniquely identifies a licensee. |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/keys/ak_test/lookups' \
  -d 'user_token=uk_secret'
```

**JavaScript**

```javascript
const response = await fetch(
  'https://api.addresszen.com/v1/keys/ak_test/lookups?' +
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
    "https://api.addresszen.com/v1/keys/ak_test/lookups",
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

uri = URI("https://api.addresszen.com/v1/keys/ak_test/lookups")
uri.query = URI.encode_www_form(user_token: "uk_secret")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents(
  "https://api.addresszen.com/v1/keys/ak_test/lookups?" .
  http_build_query([
    "user_token" => "uk_secret",
  ])
);
$result = json_decode($response, true)["result"];
```

## See also

- [Live docs](https://docs.addresszen.com/docs/api/key-logs)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
