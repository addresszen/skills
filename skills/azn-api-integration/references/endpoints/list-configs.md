# List Configuration

**Endpoint:** `GET /keys/{key}/configs`

**Operation ID:** `ListConfigs`

**Tags:** Configurations

Lists configurations associated with a key

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used for sensitive operations on your account and API Keys. |

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | object | List of configurations |
| `message` | yes | string |  |
| `code` | yes | integer |  |

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 400 |  | Bad Request |
| 401 |  | Unauthorized Request |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/list-configs)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
