# Retrieve Licensee

**Endpoint:** `GET /keys/{key}/licensees/{licensee}`

**Operation ID:** `RetrieveLicensee`

**Tags:** Licensees

Returns licensee information as identified by the licensee key.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `licensee` | path | yes | string | Uniquely identifies a licensee. |
| `user_token` | query | no | string | A secret key used for sensitive operations on your account and API Keys. |

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes |  |  |
| `code` | yes | integer |  |
| `message` | yes | string |  |

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 400 |  | Bad Request |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/retrieve-licensee)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
