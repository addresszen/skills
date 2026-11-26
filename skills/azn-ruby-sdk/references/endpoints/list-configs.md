# `client.list_configs`

List

Returns every configuration stored against a key, oldest first.

## Endpoint

`GET /keys/{key}/configs`

See the [API reference](https://docs.addresszen.com/docs/api/list-configs) for this endpoint.

This operation needs a Management Key. Pass it as `management_key:` to `AddressZen::Client.new`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/ruby/setup).

## Signature

```ruby
def list_configs(key)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `String` | yes | API Key |

## Query Parameters

_None._

## Response

`AddressZen::Responses::ConfigsResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="list-configs.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: "uk_test")

response = client.list_configs("ak_test")

response.result.configs.each do |config|
  puts "#{config.name} updated #{config.updated_at}"
end
```
