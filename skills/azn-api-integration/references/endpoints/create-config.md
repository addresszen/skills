# Create Configuration

**Endpoint:** `POST /keys/{key}/configs`

**Operation ID:** `CreateConfig`

**Tags:** Configurations

Create a configuration

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used for sensitive operations on your account and API Keys. |

## Request Body

Content-Type: `application/json` (required)

| Field | Required | Type | Description |
|---|---|---|---|
| `name` | yes | string | A unique name to identify the configuration payload |
| `payload` | yes | string | A serialised payload of up to `4096` characters |

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

## See also

- [Live docs](https://docs.addresszen.com/docs/api/create-config)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
