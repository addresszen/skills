# `client.key_usage`

Usage Stats

Reports the number of lookups a key consumed over a date range, as a total and a daily breakdown.

The range defaults to the last 21 days. `start` and `end` take UNIX timestamps in milliseconds, and `end` defaults to the current time. The maximum range is 90 days.

Query at most three tags at once.

## Endpoint

`GET /keys/{key}/usage`

See the [API reference](https://docs.addresszen.com/docs/api/key-usage) for this endpoint.

This operation needs a Management Key. Pass it as `management_key:` to `AddressZen::Client.new`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/ruby/setup).

## Signature

```ruby
def key_usage(key, start: nil, end: nil, tags: nil, licensee: nil)
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
| `tags` | `String, Array<String>` | no | Tags |
| `licensee` | `String` | no | Licensee Key |

## Response

`AddressZen::Responses::ApiKeyUsageResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="key-usage.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: "uk_test")

now = (Time.now.to_f * 1000).to_i
week = 7 * 24 * 60 * 60 * 1000

response = client.key_usage("ak_test", start: now - week, end: now)

response.result.daily_count.each do |day|
  puts "#{day.date}: #{day.count}"
end

puts "Total: #{response.result.total}"
```
