# Logs (CSV)

**Endpoint:** `GET /keys/{key}/lookups`

**Operation ID:** `KeyLogs`

**Tags:** Keys

Reports lookup information on a key for paid lookups.

This method requires a `user_token`, which can be found on your [accounts page](https://addresszen.com/account).

A maximum interval of 90 days can be provided for analysis. If no start or end date is provided, the last 21 days will be used as the default interval.

## Download Usage History (CSV)

`GET /keys/:key/lookups`

Returns a CSV download of lookups performed and associated information.

Note that the Content-Type returned will be CSV (text/csv). For a non 200 response, the `Content-Type` will revert to JSON with the error code and message embedded.

## Data Redaction

Personally Identifiable Data (PII) caught in this your usage log (including IP, search term and URL data) will be redacted on a weekly basis.

By default, PII will be redacted if it is older than 21 days. This timeframe can be configured from your dashboard.

You may prevent PII collection altogether by setting the interval to `0` days.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `key` | path | yes | string | The API Key to retrieve. Begins `ak_`. |
| `user_token` | query | no | string | A secret key used for sensitive operations on your account and API Keys. |
| `start` | query | no | integer | A start date/time in the form of a UNIX Timestamp in milliseconds. E.g. `1418556452651` |
| `end` | query | no | integer | An end date/time in the form of a UNIX Timestamp in milliseconds. E.g.  `1418556477882` |
| `licensee` | query | no | string | Uniquely identifies a licensee. |

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 400 |  | Bad Request |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/key-logs)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
