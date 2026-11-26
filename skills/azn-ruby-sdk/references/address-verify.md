# Address verification

`address_verify` checks a US address against the USPS Coding Accuracy Support System (CASS). It returns the address corrected and standardized, with its ZIP+4 code and USPS delivery data.

```ruby title="verify.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")
result = client.address_verify(query: "1010 Cauthen Ln, Alamogordo, NM 88310").result

if !result.is_a?(AddressZen::Types::UsaVerifyMatch)
  puts "No match: #{result.match_information}"
elsif result.match.is_a?(AddressZen::Types::UsaCassVerifiedAddress)
  puts "#{result.zip_code} dpv=#{result.match.dpv} rdi=#{result.match.rdi}"
else
  puts "#{result.zip_code} #{result.match.dataset}"
end
```

Every argument is a keyword: `query:` and the address parts go in the request body, and `context:`, `tags:` and `remove_firm:` in the query string. Your key needs address verification enabled, or the call raises `AddressZen::ApiError` with status `401`.

## Read a match

A `UsaVerifyMatch`. The standardized address is at the top level, in `address_line_one`, `address_line_two`, `city`, `state` and `zip_code`. The full USPS record behind it is in `match`, a `UsaCassVerifiedAddress`. The example above returns ZIP+4 `88310-5631`. The [API reference](https://docs.addresszen.com/docs/api/address-verify) lists every field, including county, congressional district, time zone and coordinates.

## Check deliverability

Check `match.dpv`, the USPS Delivery Point Validation result. `Y` means USPS confirms the address as a delivery point. `D` means the apartment or suite number is missing, `S` means it is extra or incorrect and `N` means USPS does not confirm the address.

`confidence` measures something else, how well your input matched an address, and the two can disagree. `123 Main St, Springfield, CO 81073` scores a `confidence` of `1` but a `dpv` of `N`: the street exists, but USPS does not confirm the number.

## Handle no match

An address that cannot be verified still returns successfully, as a `UsaVerifyNoMatch` with `match` set to `nil`, a `count` of `0`, empty address fields and the reason in `match_information`, such as `Address not found` or `House number not valid for this street`. The wording may change, so do not parse it. CASS corrects what it can first: an address with the wrong city or state for its ZIP code still verifies, with the corrected values.

## Fit and confidence

Both run from 0 to 1. `fit` compares only the parts you sent, so `1010 Cauthen Ln` with a ZIP code and nothing else can score a `fit` of 1. `confidence` also counts the parts you left out, so the same input scores below 1.

## Send the address in parts

Put the street line in `query:` and add `zip_code:`, or `city:` and `state:`.

```ruby title="verify_parts.rb"
result = client.address_verify(query: "1010 Cauthen Ln", zip_code: "88310").result
```

`zip_code:` accepts `88310-5631`, `883105631` or `88310`. `state:` takes the two-letter abbreviation.

## Verify outside the United States

Pass `context:` with the country's ISO 3166-1 alpha-3 code. Outside the United States `match` is an `Address`, the same class `retrieve_address` returns, with a `dataset` and a `native` record from that country's source.

```ruby title="verify_elsewhere.rb"
result = client.address_verify(query: "10 Downing Street, London, SW1A 2AA", context: "GBR").result

if result.is_a?(AddressZen::Types::UsaVerifyMatch) && result.match.is_a?(AddressZen::Types::Address)
  puts "#{result.match.line_1} #{result.match.dataset}"
end
```

See [responses](https://docs.addresszen.com/docs/sdks/ruby/responses) for every class a result can take.

## Cost

Every verification the CASS engine answers costs one lookup, matched or not. A query that cannot be parsed into an address costs nothing. A verification still running after 9.5 seconds raises `AddressZen::ApiError` with status `429`.

See [`address_verify`](https://docs.addresszen.com/docs/sdks/ruby/endpoints/address-verify) for the keywords.
