# `client.update_key_details`

Update Details

Updates a key's settings and returns its private details. Only the fields you send change. A key on an unlimited plan ignores changes to `datasets`, `daily_limit` and `monthly_limit`. Datasets set by your plan cannot be changed here: sending one with a different value returns a 400.

## Endpoint

`PUT /keys/{key}/details`

See the [API reference](https://docs.addresszen.com/docs/api/update-key-details) for this endpoint.

This operation needs a Management Key. Pass it as `management_key:` to `AddressZen::Client.new`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/ruby/setup).

## Signature

```ruby
def update_key_details(
  key,
  name: nil,
  daily_limit: nil,
  monthly_limit: nil,
  individual_limit: nil,
  allowed_urls: nil,
  redact_days: nil,
  notifications: nil,
  ip_forwarding: nil,
  datasets: nil
)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `String` | yes | API Key |
| `keywords` | `keyword arguments` | no | One per [body field](#request-body), named as the API names them. A keyword left out or `nil` is not sent. |

## Query Parameters

_None._

## Request Body

Pass these as keyword arguments too; the SDK sends them as the JSON body.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `name` | `String` | no | A name for the key |
| `daily_limit` | `Hash` | no |  |
| `monthly_limit` | `Hash` | no |  |
| `individual_limit` | `Hash` | no |  |
| `allowed_urls` | `Array<String>` | no | A list of allowed URLs. An empty list disables the check. Up to 10 allowed. |
| `redact_days` | `Integer` | no | Number of days to preserve personal data stored in your key usage history. Set to 0 to prevent personal data storage |
| `notifications` | `Hash` | no |  |
| `ip_forwarding` | `Boolean` | no | Accept IP addresses forwarded in the `AZ-Source-IP` header |
| `datasets` | `Hash` | no | Datasets you can switch on or off for this key. Datasets set by your plan (`paf`, `mr`, `nyb`, `ecad`, `ecaf`) cannot be changed here: sending one with a different value returns a 400. |

## Response

`AddressZen::Responses::ApiKeyDetailsResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="update-key-details.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: "uk_test")

response = client.update_key_details(
  "ak_test",
  name: "Checkout",
  allowed_urls: ["https://www.example.com"]
)

puts response.result.name
```
