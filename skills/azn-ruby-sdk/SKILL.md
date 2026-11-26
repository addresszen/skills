---
name: azn-ruby-sdk
description: Use when integrating the AddressZen Ruby SDK (the addresszen gem). Covers US address verification, autocomplete, email and phone validation, API keys, licensees and error handling, plus a reference for every API operation.
license: SEE LICENSE IN LICENSE
metadata:
  author: addresszen
  homepage: https://addresszen.com
references:
  - setup.md
  - address-verify.md
  - autocomplete.md
  - email-validation.md
  - phone-validation.md
  - keys.md
  - licensees.md
  - responses.md
  - errors.md
  - endpoints/
---

# AddressZen Ruby SDK

Call the AddressZen API from Ruby 3.3 or later with one method per API operation and response objects with a reader per field. No runtime dependencies: requests go through Net::HTTP unless you pass a `transport:`.

```bash
gem install addresszen
```

```ruby
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")

result = client.address_verify(query: "1010 Cauthen Ln, Alamogordo, NM 88310").result
if result.is_a?(AddressZen::Types::UsaVerifyMatch)
  puts "#{result.address_line_one}, #{result.city}, #{result.state} #{result.zip_code}"
end
```

Create one client and reuse it. Each API operation is one method on it, named from its operation ID in snake_case: `address_verify`, `find_address`, `retrieve_address`, `find_place`, `resolve_place`, `email_validation`, `phone_number_validation`, `key_availability`, `key_details`, `update_key_details`, `key_usage`, `key_logs`, the licensee methods (`list_licensees`, `create_licensee`, `retrieve_licensee`, `update_licensee`, `delete_licensee`, `regenerate_licensee_key`) and the config methods (`list_configs`, `create_config`, `retrieve_config`, `update_config`, `delete_config`). Path parameters are positional; query parameters and body fields are keyword arguments under the API's own names, as in `client.find_address(query: "1010 Cauthen Ln", limit: 5)`. A keyword left out or `nil` is not sent; an unknown keyword raises `ArgumentError`. Array values are sent comma-joined.

Responses have `code`, `message` and `result`. Readers use the API's field names verbatim (`address_line_one`, `zip_code`, `line_1`), with a snake_case alias for the few camelCase ones (`daily_count`, `has_more`, `created_at`). A missing field reads `nil`. `[]` reads any field by its API name and `to_h` returns the decoded body, unknown fields included.

## Gotchas

- `address_verify` takes only keywords: `query:` and the address parts (`zip_code:`, `city:`, `state:`) go in the body, `context:` in the query string. A US match is a `UsaVerifyMatch` whose `match` is a `UsaCassVerifiedAddress`; check `match.dpv` for deliverability, not `confidence`. An unverifiable address returns a `UsaVerifyNoMatch`, not an error. With another `context:`, such as `"GBR"`, `match` is an `Address`.
- `end:` on `key_usage` and `key_logs` is a valid keyword argument even though `end` is a Ruby keyword. `start:` and `end:` are UNIX timestamps in milliseconds.
- Flags such as `bias_ip:` and `current_carrier:` take the string `"true"`.
- Several results are one of two classes; check with `is_a?` or `case`: `UsaVerifyMatch` or `UsaVerifyNoMatch`, `Email` or `UnknownEmail`, `PhoneNumber` or `InvalidPhoneNumber`. Classes live in `AddressZen::Types` and `AddressZen::Responses`.
- `native` on an address is `nil` for a United States (`usps`) address; otherwise a class per dataset (`PafAddress` and so on), a plain hash for a dataset the SDK does not know yet, or `nil`. `native` on a place is a `GeonamesPlace`, a hash or `nil`.
- The SDK never validates values or enums, so a new API value never raises.
- Autocomplete suggestions are free, each `retrieve_address` costs a lookup, and the API rate limits keys that search without retrieving. Call `find_address` from your server, never with a key shipped to the browser.

## Authentication and errors

Pass `api_key:` to `AddressZen::Client.new`. Key management (except `key_availability`), licensee and config methods (except `retrieve_config`) also need `management_key:` (`uk_...`). The SDK sends credentials in the `Authorization` header; load the Management Key from a secret store and never ship it to a browser. To bill a licensee, build a client with its `sl_` key as `api_key:`.

An HTTP error raises `AddressZen::ApiError` with `status`, the API error `code`, `message` and the parsed `body`. Network failures raise `TransportError` (the original exception is `cause`), a non-JSON success raises `UnserializableResponseError`, and a Management Key operation without a key raises `MissingManagementKeyError` before any request. All inherit from `AddressZen::Error`. The SDK never retries: a timed-out verification may already be charged. See [error handling](./references/errors.md).

## Testing

Pass `transport:` any object with `call(request)` returning `AddressZen::Response.new(status:, headers:, body:)` to stub the API without a network. `AddressZen::Request` has `http_method`, `url`, `headers` and `body`. See [setup](./references/setup.md).

## References

- [Setup](./references/setup.md): client options, timeouts, User-Agent and custom transports
- [Address verification](./references/address-verify.md): CASS matches, deliverability, no match and other countries
- [Autocomplete](./references/autocomplete.md): find and retrieve addresses, and place search
- [Email validation](./references/email-validation.md)
- [Phone validation](./references/phone-validation.md)
- [API keys](./references/keys.md): details, usage, logs and configs
- [Licensees](./references/licensees.md)
- [Responses](./references/responses.md): readers, `[]`, `to_h`, unions and native records
- [Error handling](./references/errors.md)
- [Operations](./references/endpoints/)
