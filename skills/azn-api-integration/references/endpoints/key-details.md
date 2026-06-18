# Details

**Endpoint:** `GET /keys/{key}/details`

**Operation ID:** `KeyDetails`

**Tags:** Keys

Returns private data on the key including remaining lookups, available datasets and usage limits.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used for sensitive operations on your account and API Keys. |

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | object |  |
| `code` | yes | integer |  |
| `message` | yes | string |  |

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 401 |  | Unauthorised |
| 404 |  | Resource not found |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/key-details)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
