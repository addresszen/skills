# Email Validation

**Endpoint:** `GET /emails`

**Operation ID:** `EmailValidation`

**Tags:** Emails

Validates an email address and reports whether it is deliverable.

Requires an API Key licensed for email validation. A query over 320 characters is rejected.

A validated address decrements your lookup balance. An address the API cannot check returns `unknown` and costs no lookup. An address whose domain does not resolve, or publishes no MX records, returns `not_deliverable` and also costs no lookup. Only those two domain failures populate `suggestions`. Every other response returns an empty list.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `query` | query | yes | string | Specifies the email address to validate |
| `tags` | query | no | string | A comma separated list of tags to query over. |

## Request Samples

**curl**

```bash
curl -G 'https://api.addresszen.com/v1/emails' \
  -d 'api_key=ak_test' \
  --data-urlencode 'query=foo@domain.com'
```

**JavaScript**

```javascript
const response = await fetch(
  'https://api.addresszen.com/v1/emails?' +
  new URLSearchParams({
    api_key: 'ak_test',
    query: 'foo@domain.com',
  })
);

const { result } = await response.json();
```

**Python**

```python
import requests

response = requests.get(
    "https://api.addresszen.com/v1/emails",
    params={
        "api_key": "ak_test",
        "query": "foo@domain.com",
    },
)
result = response.json()["result"]
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/emails")
uri.query = URI.encode_www_form(api_key: "ak_test", query: "foo@domain.com")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents(
  "https://api.addresszen.com/v1/emails?" .
  http_build_query([
    "api_key" => "ak_test",
    "query" => "foo@domain.com",
  ])
);
$result = json_decode($response, true)["result"];
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `code` | yes | `2000` |  |
| `message` | yes | `Success` |  |
| `result` | yes | Email \| UnknownEmail |  |

## Response Example

```json
{
  "result": {
    "result": "deliverable",
    "deliverable": true,
    "catchall": false,
    "free": false,
    "role": true,
    "disposable": false,
    "suggestions": []
  },
  "code": 2000,
  "message": "Success"
}
```

## See also

- [Live docs](https://docs.addresszen.com/docs/api/email-validation)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
