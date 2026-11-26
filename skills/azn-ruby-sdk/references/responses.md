# Responses

Every method returns an object built from the API's JSON, with one reader per field under the API's own name. `[]` reads any field by name, and `to_h` returns the decoded body.

```ruby title="fields.rb"
response = client.retrieve_address("usps_Z108703633|123||1119")
address = response.result

puts address.zip_plus_4_code    # reader
puts address["zip_plus_4_code"] # the API's field name, same value
```

## Field names

Readers use the API's field names verbatim: `line_1`, `last_line`, `zip_code`. A few fields are camelCase in the API, such as `dailyCount` and `hasMore`; each also has a snake_case alias, `daily_count` and `has_more`. Native records keep their source dataset's names, so a Korean address has readers such as `법정동코드` and a Danish one `wgs84koordinat_længde`.

## Missing and unknown fields

A field the API leaves out reads as `nil`, so a filtered request or an optional field never raises. A field the API adds after your SDK version has no reader yet, but `[]` and `to_h` return it, so you can read it before you upgrade.

## Get the raw hash

Call `to_h` on any response or nested object. It returns the decoded body with the API's field names, unknown fields included, so it round-trips through `JSON.generate`. The hash is frozen; `dup` it to change it.

```ruby title="hash.rb"
data = response.to_h
puts JSON.pretty_generate(data)
```

Two objects are `==` when they are the same class and hold the same body.

## Types

| Module | Holds |
| --- | --- |
| `AddressZen::Responses` | One class per operation response, such as `VerifyResponse` and `AutocompleteResponse`. Each has `code`, `message` and `result` |
| `AddressZen::Types` | Everything inside a result: `UsaVerifyMatch`, `Address`, `AddressSuggestion`, `Licensee`, `Config` and the native records |

The gem's `sig/` directory has an RBS signature for every class, reader and method, so Steep, Ruby LSP and other RBS tools check the keywords you pass and the readers you call. `key_logs` is the exception to the object rule: it returns the CSV as a string.

## Union results

Some results come in one of several forms, and the SDK picks the class that matches. Check with `is_a?` or `case`.

| Field | Classes |
| --- | --- |
| `address_verify` result | `UsaVerifyMatch`, or `UsaVerifyNoMatch` when nothing matches: `match` is `nil`, `count` is `0` and the address fields are empty strings |
| `UsaVerifyMatch` `match` | `UsaCassVerifiedAddress` for a CASS match in the United States, or `Address` for a match elsewhere, such as with `context: "GBR"`. An `Address` has a `dataset` and a `native` record |
| `Address` `native` | A class for the address's source dataset, such as `PafAddress`; a hash for a dataset the SDK does not know yet; or `nil` |
| `Place` `native` | `GeonamesPlace`; a hash for a dataset the SDK does not know yet; or `nil` |
| `email_validation` result | `Email`, or `UnknownEmail` when deliverability cannot be checked |
| `phone_number_validation` result | `PhoneNumber`, or `InvalidPhoneNumber` |

```ruby title="union.rb"
case (result = client.address_verify(query: "1010 Cauthen Ln, Alamogordo, NM 88310").result)
when AddressZen::Types::UsaVerifyMatch
  puts "#{result.zip_code} with confidence #{result.confidence}"
when AddressZen::Types::UsaVerifyNoMatch
  puts "No match: #{result.match_information}"
end
```

## New values

Your integration keeps working. The SDK never checks values against the spec, so a fixed set such as `dpv` on a CASS match or `result` on an email can gain a value without breaking anything: compare against the values you handle and fall through for the rest. The RBS signatures list the known values in a comment.

## Native records

`native` on an `Address` is the raw record from the address's source dataset, as a class named for the dataset, such as `PafAddress` for Royal Mail PAF. The `dataset` field on the address says which. A dataset the SDK does not know yet comes back as a plain hash, so a new dataset never breaks your integration. A United States address (`dataset` `usps`) has no native record, so its `native` is `nil`.

```ruby title="native.rb"
address = client.retrieve_address("usps_Z108703633|123||1119").result

case address.native
when nil then puts "No native record for #{address.dataset}"
when Hash then puts "New dataset: #{address.dataset}"
else puts address.native.class.name
end
```

The [data sources](https://docs.addresszen.com/docs/data) pages document every dataset's fields.
