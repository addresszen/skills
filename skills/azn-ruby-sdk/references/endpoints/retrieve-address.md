# `client.retrieve_address`

Retrieve Address

Returns the full address for an autocomplete suggestion id.

This is the charged step of address autocomplete. A successful retrieval decrements your lookup balance. An id which resolves to no address returns `404`.

Every address comes back in one US-shaped format, whatever country or dataset it came from: up to two address lines and US field names such as `zip_code`, `state` and `city`.

## Endpoint

`GET /autocomplete/addresses/{address}/usa`

See the [API reference](https://docs.addresszen.com/docs/api/retrieve-address) for this endpoint.

## Signature

```ruby
def retrieve_address(address, licensee: nil, filter: nil, tags: nil, remove_firm: nil)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `address` | `String` | yes | ID of address suggestion |
| `keywords` | `keyword arguments` | no | One per [query parameter](#query-parameters), named as the API names them. A keyword left out or `nil` is not sent. |

## Query Parameters

Pass these as keyword arguments.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `licensee` | `String` | no | Licensee Key |
| `filter` | `String, Array<String>` | no | Restrict Result Fields |
| `tags` | `String, Array<String>` | no | Tags |
| `remove_firm` | `String` | no | Remove Firm |

## Response

`AddressZen::Responses::UsaResolveAddressResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="retrieve-address.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")

response = client.retrieve_address("usps_Z108703633|123||1119")

address = response.result

puts address.line_1
puts address.last_line
```
