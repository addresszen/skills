# Create Licensee

**Endpoint:** `POST /keys/{key}/licensees`

**Operation ID:** `CreateLicensee`

**Tags:** Licensees

Create a licensee for the specified API Key.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used for sensitive operations on your account and API Keys. |

## Request Body

Content-Type: `application/json` (required)

| Field | Required | Type | Description |
|---|---|---|---|
| `name` | no | string | Licensee individual or organization name |
| `address` | no | string | Licensee's first, second and third line address as well as post town concatenated by commas |
| `postcode` | no | string | Licensee's postcode |
| `whitelist` | no | array | A list of allowed URLs. An empty list means that whitelisting is disabled |
| `daily` | no | object |  |

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

- [Live docs](https://docs.addresszen.com/docs/api/create-licensee)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
