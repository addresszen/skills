# `client.key_details`

Details

Returns private data on a key: remaining lookups, licensed datasets, usage limits, notification settings and the search contexts the key can serve.

## Endpoint

`GET /keys/{key}/details`

See the [API reference](https://docs.addresszen.com/docs/api/key-details) for this endpoint.

This operation needs a Management Key. Pass it as `management_key:` to `AddressZen::Client.new`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/ruby/setup).

## Signature

```ruby
def key_details(key)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `String` | yes | API Key |

## Query Parameters

_None._

## Response

`AddressZen::Responses::ApiKeyDetailsResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="key-details.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: "uk_test")

response = client.key_details("ak_test")

puts "#{response.result.name}: #{response.result.lookups_remaining} lookups remaining"
```
