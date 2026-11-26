# `client.key_logs`

Logs (CSV)

Returns a CSV of the charged lookups made on a key, one row per request.

Requires the account Management Key. The maximum interval is 90 days. Without a start or end date the interval is the last 21 days.

The response is `text/csv` and downloads as an attachment. A non-200 response reverts to JSON, with the error code and message in the body.

## CSV format

The CSV has no header row. Columns, in order:

1. Timestamp (ISO 8601)
2. IP address the request was received from
3. Search term
4. URL the request originated from
5. Lookup type
6. Tags
7. Lookups consumed
8. Licensee name (sublicensing keys only)
9. Source IP address

The source IP column carries the address forwarded in the `AZ-Source-IP` header. We record it only for keys with IP address forwarding enabled, and only when the header holds a valid IP address. It is empty otherwise.

## Data redaction

We redact personally identifiable information (PII) in your usage log weekly, covering the IP, source IP, search term and URL columns.

The default retention is 28 days. Change the period from your dashboard. Set it to `0` days to stop collecting PII altogether.

## Endpoint

`GET /keys/{key}/lookups`

See the [API reference](https://docs.addresszen.com/docs/api/key-logs) for this endpoint.

This operation needs a Management Key. Pass it as `management_key:` to `AddressZen::Client.new`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/ruby/setup).

## Signature

```ruby
def key_logs(key, start: nil, end: nil, licensee: nil)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `String` | yes | API Key |
| `keywords` | `keyword arguments` | no | One per [query parameter](#query-parameters), named as the API names them. A keyword left out or `nil` is not sent. |

## Query Parameters

Pass these as keyword arguments.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `start` | `Integer` | no | Start Timestamp |
| `end` | `Integer` | no | End Timestamp |
| `licensee` | `String` | no | Licensee Key |

## Response

The CSV text, as a `String`.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="key-logs.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: "uk_test")

now = (Time.now.to_f * 1000).to_i
week = 7 * 24 * 60 * 60 * 1000

puts client.key_logs("ak_test", start: now - week, end: now)
```
