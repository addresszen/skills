# `client.phone_number_validation`

Phone Number Validation

Validates a phone number and returns its country, its national and international formats, and the network it was originally assigned to.

Requires an API Key licensed for phone validation.

Every query decrements your lookup balance, including a number that fails to parse and a number reported as invalid.

## Endpoint

`GET /phone_numbers`

See the [API reference](https://docs.addresszen.com/docs/api/phone-number-validation) for this endpoint.

## Signature

```ruby
def phone_number_validation(query:, current_carrier: nil, tags: nil)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `keywords` | `keyword arguments` | yes | One per [query parameter](#query-parameters), named as the API names them. A keyword left out or `nil` is not sent. |

## Query Parameters

Pass these as keyword arguments.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `query` | `String` | yes | Specifies the phone number to validate. Phone number must include a country code in an acceptable format. For instance, UK phone numbers should be prefixed with `+44`, `44` or `0044`. |
| `current_carrier` | `String` | no | When set to `true`, the API retrieves and populates the current network of the phone number. |
| `tags` | `String, Array<String>` | no | Tags |

## Response

`AddressZen::Responses::PhoneNumberResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="phone-number-validation.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")

response = client.phone_number_validation(query: "+1 202 555 0123")

result = response.result

if result.is_a?(AddressZen::Types::PhoneNumber)
  puts "#{result.international_format} (#{result.country})"
else
  puts "Invalid phone number"
end
```
