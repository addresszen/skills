# `client.address_verify`

Verify Address

Verifies an address against the USPS Coding Accuracy Support System (CASS) and returns it standardized and corrected.

Submit the whole address in `query`, or the first address line in `query` with either `zip_code`, or `city` and `state`. A freeform `query` is parsed into those components before the search runs.

A match returns the standardized address lines, city, state and ZIP+4, scored by `fit` and `confidence`. It also carries the CASS record behind the match: delivery point, DPV flags, carrier route, eLOT, county, congressional district, RDI, time zone and coordinates. CASS corrects what it can, so an address with the wrong city or state for its ZIP code still verifies, with the corrected values.

An address that cannot be verified returns `200` with a `count` of `0`, a `null` `match` and empty address fields. `match_information` says why, e.g. `Address not found` or `House number not valid for this street`. It is for people to read and its wording may change, so test `match` for `null` rather than parsing it.

In the United States every verification the CASS engine answers draws on your balance, matched or not. A query that cannot be parsed into an address does not. Elsewhere only a match draws on your balance. A key without address verification enabled returns `401`. A verification still running after 9.5 seconds aborts with `429`.

## Countries

Verify defaults to the United States, where it is CASS certified. Pass `context` with an ISO 3166-1 alpha-3 country code to verify an address elsewhere, e.g. `context=GBR` or `context=FRA`. The address datasets your key is licensed for decide which countries it can verify.

Outside the United States there is no CASS record, so `match` is the address in the same format Retrieve Address returns: USPS-style field names, empty strings where the country has no equivalent, and the raw dataset record in `native`. Check `dataset` to tell the two apart: it is present on every non-US match and absent from a CASS match.

The top-level fields (`address_line_one`, `address_line_two`, `city`, `state`, `zip_code`, `country_iso_2`) are populated for every country, along with `confidence` and `fit`.

## Endpoint

`POST /verify/addresses`

See the [API reference](https://docs.addresszen.com/docs/api/address-verify) for this endpoint.

## Signature

```ruby
def address_verify(
  query:,
  tags: nil,
  remove_firm: nil,
  context: nil,
  zip_code: nil,
  city: nil,
  state: nil
)
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `keywords` | `keyword arguments` | yes | One per [query parameter](#query-parameters) and [body field](#request-body), named as the API names them. A keyword left out or `nil` is not sent. |

## Query Parameters

Pass these as keyword arguments.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `tags` | `String, Array<String>` | no | Tags |
| `remove_firm` | `String` | no | Remove Firm |
| `context` | `String` | no | Identify the country of the address to verify. Defaults to United States (USA) |

## Request Body

Pass these as keyword arguments too; the SDK sends them as the JSON body.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `query` | `String` | yes | Address input to verify. |
| `zip_code` | `String` | no | Specify the ZIP code of an address. The following formats are accepted: `81073-1119`, `810731119`, `81073`. |
| `city` | `String` | no | City of an address. |
| `state` | `String` | no | State of an address. For the US, use the 2-letter state abbreviation. |

## Response

`AddressZen::Responses::VerifyResponse`. Read fields with readers named as the API names them, such as `response.result`, or with `response["result"]`. `to_h` returns the decoded body.

## Errors

An HTTP error raises `AddressZen::ApiError` with the HTTP `status`, the API error `code` and the decoded `body`. A transport failure raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

## Example

```ruby title="address-verify.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")

response = client.address_verify(query: "1010 Cauthen Ln, Alamogordo, NM 88310")

result = response.result

if result.is_a?(AddressZen::Types::UsaVerifyMatch)
  puts "#{result.address_line_one}, #{result.city}, #{result.state} #{result.zip_code}"
else
  puts "No match"
end
```
