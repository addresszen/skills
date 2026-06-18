# Update Details

**Endpoint:** `PUT /keys/{key}/details`

**Operation ID:** `UpdateKeyDetails`

**Tags:** Keys

Update API Key Details

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used for sensitive operations on your account and API Keys. |

## Request Body

Content-Type: `application/json` (required)

| Field | Required | Type | Description |
|---|---|---|---|
| `name` | no | string | A name for the key |
| `daily_limit` | no | object |  |
| `monthly_limit` | no | object |  |
| `individual_limit` | no | object |  |
| `allowed_urls` | no | array | A list of allowed URLs. An empty list means that allowed URLs are disabled. Up to 10 allowed. |
| `redact_days` | no | integer | Number of days to preserve personal data stored in your key usage history. Set to 0 to prevent personal data storage |
| `notifications` | no | object |  |
| `ip_forwarding` | no | boolean | Accept IP addresses forwarded in the `AZ-Source-IP` header |
| `datasets` | no | object | Indicates which datasets are available and added by default to the address responses |

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | object |  |
| `code` | yes | integer |  |
| `message` | yes | string |  |

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 400 |  | Bad Request |
| 401 |  | Unauthorised |
| 404 |  | Resource not found |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/update-key-details)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
