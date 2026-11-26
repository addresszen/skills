# `client.key_availability`

Availability

Returns public information on an API Key: whether it can be used right now (`available`), the search contexts the key is licensed for (`contexts`) and the context that best matches the caller's IP address (`context`).

The endpoint accepts API Keys (beginning `ak_`) and sub-licensed keys (beginning `sl_`), and needs no Management Key.

A key that exists but cannot be used, because it has no lookups left or has breached a limit, returns `200` with `"available": false`. An unknown or malformed key returns an error.

Supply a valid Management Key and the endpoint returns the key's private details instead, as `GET /keys/{key}/details` does. A Management Key that does not own the key is rejected.

## Endpoint

`GET /keys/{key}`

See the [API reference](https://docs.addresszen.com/docs/api/key-availability) for this endpoint.

## Signature

```ruby
def key_availability(key)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `String` | yes | API Key |

## Query Parameters

_None._

## Response

`AddressZen::Responses::ApiKeyResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="key-availability.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")

response = client.key_availability("ak_test")

puts "Available: #{response.result.available}"
puts "Context: #{response.result.context}"
```
