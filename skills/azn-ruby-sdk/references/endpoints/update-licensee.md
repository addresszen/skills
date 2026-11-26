# `client.update_licensee`

Update

Updates a licensee's address, postcode, allowed URLs and daily limit. Returns the updated licensee. The name is fixed at creation.

## Endpoint

`POST /keys/{key}/licensees/{licensee}`

See the [API reference](https://docs.addresszen.com/docs/api/update-licensee) for this endpoint.

This operation needs a Management Key. Pass it as `management_key:` to `AddressZen::Client.new`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/ruby/setup).

## Signature

```ruby
def update_licensee(
  key,
  licensee,
  name: nil,
  address: nil,
  postcode: nil,
  whitelist: nil,
  daily: nil
)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `String` | yes | API Key |
| `licensee` | `String` | yes | Licensee Key |
| `keywords` | `keyword arguments` | no | One per [body field](#request-body), named as the API names them. A keyword left out or `nil` is not sent. |

## Query Parameters

_None._

## Request Body

Pass these as keyword arguments too; the SDK sends them as the JSON body.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `name` | `String` | no | Licensee individual or organisation name |
| `address` | `String` | no | Licensee's first, second and third line address as well as post town concatenated by commas |
| `postcode` | `String` | no | Licensee's postcode |
| `whitelist` | `Array<String>` | no | A list of allowed URLs. An empty list disables the check. |
| `daily` | `Hash` | no |  |

## Response

`AddressZen::Responses::LicenseeResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="update-licensee.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: "uk_test")

response = client.update_licensee("ak_test", "sl_hk71kco54zGSGvF9eXXrvvnMOLLNh", name: "Acme Inc")

puts response.result.name
```
