# Availability

**Endpoint:** `GET /keys/{key}`

**Operation ID:** `KeyAvailability`

**Tags:** Keys

Returns public information on your API Key.

This endpoint can be used for the following:
 - Determine if the key is currently usable via the `available` property
 - Determine available contexts for an API Key
- Identify the currently likely context of a user given their location

You may pass both API Keys (beginning `ak_`) and Sub-licensed Keys (beginning `sl_`).

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | object |  |
| `message` | yes | string |  |
| `code` | yes | integer |  |

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 404 |  | Invalid Key |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/key-availability)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
