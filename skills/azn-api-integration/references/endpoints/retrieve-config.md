# Retrieve Configuration

**Endpoint:** `GET /keys/{key}/configs/{config}`

**Operation ID:** `RetrieveConfig`

**Tags:** Configurations

Retrieve configuration object by name

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `config` | path | yes | string | User provided configuration object name. |

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
| 404 |  | Not Found |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/retrieve-config)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
