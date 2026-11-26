# `client.retrieve_config`

Retrieve

Returns a configuration by name. This request needs no `user_token`, so a browser integration can read its own configuration at runtime.

## Endpoint

`GET /keys/{key}/configs/{config}`

See the [API reference](https://docs.addresszen.com/docs/api/retrieve-config) for this endpoint.

## Signature

```ruby
def retrieve_config(key, config)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `String` | yes | API Key |
| `config` | `String` | yes | Configuration Name |

## Query Parameters

_None._

## Response

`AddressZen::Responses::ConfigResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="retrieve-config.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")

response = client.retrieve_config("ak_test", "woocommerce")

puts response.result.payload
```
