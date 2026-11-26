# `client.resolve_place`

Resolve Place

Returns the full place for a place ID taken from a `/places` suggestion.

On top of the fields carried by the suggestion, the response adds coordinates, language and the underlying dataset record.

Each request decrements your lookup balance. An unknown ID returns `404`.

## Endpoint

`GET /places/{place}`

See the [API reference](https://docs.addresszen.com/docs/api/resolve-place) for this endpoint.

## Signature

```ruby
def resolve_place(place, tags: nil)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `place` | `String` | yes | ID of place suggestion |
| `keywords` | `keyword arguments` | no | One per [query parameter](#query-parameters), named as the API names them. A keyword left out or `nil` is not sent. |

## Query Parameters

Pass these as keyword arguments.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `tags` | `String, Array<String>` | no | Tags |

## Response

`AddressZen::Responses::ResolvePlaceResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="resolve-place.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")

response = client.resolve_place("geonames_5128581")

place = response.result

puts "#{place.descriptive_name} (#{place.country_iso})"
puts "#{place.latitude}, #{place.longitude}"
```
