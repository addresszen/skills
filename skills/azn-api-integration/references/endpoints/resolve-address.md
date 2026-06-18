# Resolve Address

**Endpoint:** `GET /autocomplete/addresses/{address}/gbr`

**Operation ID:** `ResolveAddress`

**Tags:** Address Search

Resolves an address autocompletion by its address ID.

Resolved addresses (including global addresses) are returned in a UK format (up to 3 address lines) using UK nomenclature (like postcode and county).

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `address` | path | yes | string | ID of address suggestion provided by the API to fully resolve. |
| `tags` | query | no | string | A comma separated list of tags to query over. |

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `code` | yes | integer |  |
| `message` | yes | string |  |
| `result` | yes |  |  |

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 404 |  | Resource not found |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/resolve-address)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
