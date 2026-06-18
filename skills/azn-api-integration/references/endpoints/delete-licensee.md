# Cancel Licensee

**Endpoint:** `DELETE /keys/{key}/licensees/{licensee}`

**Operation ID:** `DeleteLicensee`

**Tags:** Licensees

Cancels a licensee key. This renders a licensee unusable. This action can be reversed if you get in contact with us.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `licensee` | path | yes | string | Uniquely identifies a licensee. |
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
| 400 |  | Bad Request |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/delete-licensee)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
