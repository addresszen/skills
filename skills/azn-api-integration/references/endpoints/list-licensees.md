# List Licensee

**Endpoint:** `GET /keys/{key}/licensees`

**Operation ID:** `ListLicensees`

**Tags:** Licensees

Returns a list of licensees for a key.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `starting_after` | query | no | integer | Specify ID of the licensee after which you would like to list results |
| `user_token` | query | no | string | A secret key used for sensitive operations on your account and API Keys. |
| `limit` | query | no | integer | Specifies the maximum number of records to retrieve. |
| `query` | query | no | string | Filter result by licensee name. Query can be shortened to `q=` |

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | object | List of licensees |
| `message` | yes | string |  |
| `code` | yes | integer |  |

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 400 |  | Bad Request |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/list-licensees)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
