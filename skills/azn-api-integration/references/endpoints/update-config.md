# Update Configuration

**Endpoint:** `POST /keys/{key}/configs/{config}`

**Operation ID:** `UpdateConfig`

**Tags:** Configurations

Updates configuration object

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `config` | path | yes | string | User provided configuration object name. |
| `user_token` | query | no | string | A secret key used for sensitive operations on your account and API Keys. |

## Request Body

Content-Type: `application/json` (required)

| Field | Required | Type | Description |
|---|---|---|---|
| `payload` | no | string | A serialised payload of up to `4096` characters |

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
| 401 |  | Unauthorized Request |
| 404 |  | Not Found |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/update-config)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
