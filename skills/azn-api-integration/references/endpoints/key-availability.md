# Availability

**Endpoint:** `GET /keys/{key}`

**Operation ID:** `KeyAvailability`

**Tags:** Keys

Returns public information on an API Key: whether it can be used right now (`available`), the search contexts the key is licensed for (`contexts`) and the context that best matches the caller's IP address (`context`).

The endpoint accepts API Keys (beginning `ak_`) and sub-licensed keys (beginning `sl_`), and needs no `user_token`.

A key that exists but cannot be used, because it has no lookups left or has breached a limit, returns `200` with `"available": false`. An unknown or malformed key returns an error.

Supply a valid `user_token` and the endpoint returns the key's private details instead, as `GET /keys/{key}/details` does. A `user_token` that does not own the key is rejected.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |

## Request Samples

**curl**

```bash
curl 'https://api.addresszen.com/v1/keys/ak_test'
```

**JavaScript**

```javascript
const response = await fetch('https://api.addresszen.com/v1/keys/ak_test');

const { result } = await response.json();
```

**Python**

```python
import requests

response = requests.get("https://api.addresszen.com/v1/keys/ak_test")
result = response.json()["result"]
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/keys/ak_test")
result = JSON.parse(Net::HTTP.get(uri))["result"]
```

**PHP**

```php
<?php
$response = file_get_contents("https://api.addresszen.com/v1/keys/ak_test");
$result = json_decode($response, true)["result"];
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | [ApiKey](../data/api-key.md) |  |
| `message` | yes | `Success` |  |
| `code` | yes | `2000` |  |

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 404 |  | Invalid Key |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/key-availability)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
