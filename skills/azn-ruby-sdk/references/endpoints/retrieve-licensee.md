# `client.retrieve_licensee`

Retrieve

Returns a licensee by its `sl_` key. A canceled or unknown licensee returns `404`.

## Endpoint

`GET /keys/{key}/licensees/{licensee}`

See the [API reference](https://docs.addresszen.com/docs/api/retrieve-licensee) for this endpoint.

This operation needs a Management Key. Pass it as `management_key:` to `AddressZen::Client.new`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/ruby/setup).

## Signature

```ruby
def retrieve_licensee(key, licensee)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `String` | yes | API Key |
| `licensee` | `String` | yes | Licensee Key |

## Query Parameters

_None._

## Response

`AddressZen::Responses::LicenseeResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="retrieve-licensee.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: "uk_test")

response = client.retrieve_licensee("ak_test", "sl_hk71kco54zGSGvF9eXXrvvnMOLLNh")

puts "#{response.result.name}: #{response.result.key}"
```
