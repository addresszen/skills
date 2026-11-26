# `client.list_licensees`

List

Returns a key's licensees, oldest first, up to 100 per request. The list omits canceled licensees. The key must be enabled for sub-licensing.

## Endpoint

`GET /keys/{key}/licensees`

See the [API reference](https://docs.addresszen.com/docs/api/list-licensees) for this endpoint.

This operation needs a Management Key. Pass it as `management_key:` to `AddressZen::Client.new`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/ruby/setup).

## Signature

```ruby
def list_licensees(key, starting_after: nil, limit: nil, query: nil)
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
| `starting_after` | `String` | no | ID of the licensee after which to list results. Pass the `id` of the last licensee on the previous page. |
| `limit` | `Integer` | no | Limit |
| `query` | `String` | no | Filter results by licensee name. Can be shortened to `q=` |

## Response

`AddressZen::Responses::LicenseesResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="list-licensees.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: "uk_test")

response = client.list_licensees("ak_test", limit: 10)

response.result.licensees.each do |licensee|
  puts "#{licensee.id}: #{licensee.name} (#{licensee.key})"
end

puts "More pages: #{response.result.has_more}"
```
