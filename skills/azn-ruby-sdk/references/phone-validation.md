# Phone validation

`phone_number_validation` checks a phone number from any country and returns it in national and international format, with its country and the network it was assigned to.

```ruby title="phone.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")
phone = client.phone_number_validation(query: "+1 202 555 0123").result

if phone.is_a?(AddressZen::Types::PhoneNumber)
  puts "#{phone.international_format} #{phone.iso_country} #{phone.original_carrier&.name}"
else
  puts "Invalid phone number"
end
```

The number must include its country code: `+1` for the US and Canada, `+44` for the UK, `+81` for Japan. Your key needs phone validation enabled.

## Read the result

A valid number returns a `PhoneNumber` with `valid` `true` and:

| Reader | Contents |
| --- | --- |
| `national_format` | The number as dialed inside its country |
| `international_format` | The number with its country code |
| `iso_country` and `iso_country_2` | Three- and two-letter country codes, such as `USA` and `US` |
| `country` | Country name |
| `original_carrier` | A `Carrier` for the network the number was first assigned to, with `name` and `network_type` such as `mobile`, `landline` or `virtual` |

An invalid number returns an `InvalidPhoneNumber` with `valid` `false` and every other reader `nil`. It is not an error, so check the class before reading the formats.

## Current network

Add `current_carrier: "true"` alongside `query:` to fill `current_carrier` as well. A number can move to another network, so `original_carrier` alone can be out of date. The extra check can be slow on some networks, so allow for it in your [request timeout](https://docs.addresszen.com/docs/sdks/ruby/setup#set-a-request-timeout).

## Cost

One lookup per request, including numbers that are invalid or fail to parse.

See [`phone_number_validation`](https://docs.addresszen.com/docs/sdks/ruby/endpoints/phone-number-validation) for the keywords.
