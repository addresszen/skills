# `client.email_validation`

Email Validation

Validates an email address and reports whether it is deliverable.

Requires an API Key licensed for email validation. A query over 320 characters is rejected.

A validated address decrements your lookup balance. An address the API cannot check returns `unknown` and costs no lookup. An address whose domain does not resolve, or publishes no MX records, returns `not_deliverable` and also costs no lookup. Only those two domain failures populate `suggestions`. Every other response returns an empty list.

## Endpoint

`GET /emails`

See the [API reference](https://docs.addresszen.com/docs/api/email-validation) for this endpoint.

## Signature

```ruby
def email_validation(query:, tags: nil)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `keywords` | `keyword arguments` | yes | One per [query parameter](#query-parameters), named as the API names them. A keyword left out or `nil` is not sent. |

## Query Parameters

Pass these as keyword arguments.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `query` | `String` | yes | Specifies the email address to validate |
| `tags` | `String, Array<String>` | no | Tags |

## Response

`AddressZen::Responses::EmailResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="email-validation.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")

response = client.email_validation(query: "support@addresszen.com")

result = response.result

if result.is_a?(AddressZen::Types::Email)
  puts result.result
  puts "Deliverable: #{result.deliverable}"
  puts "Disposable: #{result.disposable}"
else
  puts "Deliverability unknown"
end
```
