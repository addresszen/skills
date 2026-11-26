# `client.delete_config`

Delete

Permanently deletes a configuration object.

## Endpoint

`DELETE /keys/{key}/configs/{config}`

See the [API reference](https://docs.addresszen.com/docs/api/delete-config) for this endpoint.

This operation needs a Management Key. Pass it as `management_key:` to `AddressZen::Client.new`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/ruby/setup).

## Signature

```ruby
def delete_config(key, config)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `String` | yes | API Key |
| `config` | `String` | yes | Configuration Name |

## Query Parameters

_None._

## Response

`AddressZen::Responses::DeleteConfigResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="delete-config.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: "uk_test")

response = client.delete_config("ak_test", "woocommerce")

puts "Deleted: #{response.result.deleted}"
```
