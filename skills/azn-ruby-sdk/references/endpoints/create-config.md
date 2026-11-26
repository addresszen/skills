# `client.create_config`

Create

Creates a named configuration on a key and returns it.

## Endpoint

`POST /keys/{key}/configs`

See the [API reference](https://docs.addresszen.com/docs/api/create-config) for this endpoint.

This operation needs a Management Key. Pass it as `management_key:` to `AddressZen::Client.new`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/ruby/setup).

## Signature

```ruby
def create_config(key, name:, payload:)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `String` | yes | API Key |
| `keywords` | `keyword arguments` | yes | One per [body field](#request-body), named as the API names them. A keyword left out or `nil` is not sent. |

## Query Parameters

_None._

## Request Body

Pass these as keyword arguments too; the SDK sends them as the JSON body.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `name` | `String` | yes | A unique name to identify the configuration payload |
| `payload` | `String` | yes | A serialized payload of up to `65536` characters |

## Response

`AddressZen::Responses::ConfigResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="create-config.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: "uk_test")

payload = JSON.generate(removeOrganisation: false)
response = client.create_config("ak_test", name: "woocommerce", payload: payload)

puts "#{response.result.name} created #{response.result.created_at}"
```
