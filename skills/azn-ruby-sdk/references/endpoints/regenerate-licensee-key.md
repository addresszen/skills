# `client.regenerate_licensee_key`

Regenerate Key

Regenerates a licensee's key and returns the licensee with the new key. The previous key stops working immediately, so update any integration that uses it.

## Endpoint

`POST /keys/{key}/licensees/{licensee}/regenerate-key`

This operation needs a Management Key. Pass it as `management_key:` to `AddressZen::Client.new`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/ruby/setup).

## Signature

```ruby
def regenerate_licensee_key(key, licensee)
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

```ruby title="regenerate-licensee-key.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: "uk_test")

response = client.regenerate_licensee_key("ak_test", "sl_hk71kco54zGSGvF9eXXrvvnMOLLNh")

puts "New licensee key: #{response.result.key}"
```
