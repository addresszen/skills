# Usage Stats

**Endpoint:** `GET /keys/{key}/usage`

**Operation ID:** `KeyUsage`

**Tags:** Keys

Reports the number of lookups consumed on a key for a range of days.

A maximum interval of 90 days can be provided for analysis. If no start or end date is provided, the last 21 days will be used as the default interval.

If no `start` time is provided, the start time will be set to 21 days prior to the current time.

If no `end` time is provided, the current time will be used.

Append `tags` to scope the number of lookups to those with matching tag values. E.g. `tags=foo,bar` will only count transactions that match `foo` and `bar`.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used for sensitive operations on your account and API Keys. |
| `start` | query | no | integer | A start date/time in the form of a UNIX Timestamp in milliseconds. E.g. `1418556452651` |
| `end` | query | no | integer | An end date/time in the form of a UNIX Timestamp in milliseconds. E.g.  `1418556477882` |
| `tags` | query | no | string | A comma separated list of tags to query over. |
| `licensee` | query | no | string | Uniquely identifies a licensee. |

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

- [Live docs](https://docs.addresszen.com/docs/api/key-usage)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
