# `client.delete_licensee`

Cancel

Cancels a licensee. Its key stops working and it drops out of the licensee list. Contact us to reverse it.

## Endpoint

`DELETE /keys/{key}/licensees/{licensee}`

See the [API reference](https://docs.addresszen.com/docs/api/delete-licensee) for this endpoint.

This operation needs a Management Key. Pass it as `management_key:` to `AddressZen::Client.new`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/ruby/setup).

## Signature

```ruby
def delete_licensee(key, licensee)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `String` | yes | API Key |
| `licensee` | `String` | yes | Licensee Key |

## Query Parameters

_None._

## Response

`AddressZen::Responses::DeleteLicenseeResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="delete-licensee.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: "uk_test")

response = client.delete_licensee("ak_test", "sl_hk71kco54zGSGvF9eXXrvvnMOLLNh")

puts "Deleted: #{response.result.deleted}"
```
