# Email validation

`email_validation` checks whether an email address can receive mail, wherever its domain is hosted. It also flags disposable, free, role and catch-all addresses.

```ruby title="email.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")
email = client.email_validation(query: "support@addresszen.com").result

if email.is_a?(AddressZen::Types::Email)
  puts "#{email.result} deliverable=#{email.deliverable}"
else
  puts "Could not check the address"
end
```

Your key needs email validation enabled.

## Read the result

`result` is one of three values:

| `result` | Meaning | Class |
| --- | --- | --- |
| `deliverable` | The mailbox accepts mail | `Email`, with `deliverable` `true` |
| `not_deliverable` | Mail will bounce, or the domain cannot receive mail | `Email`, with `deliverable` `false` |
| `unknown` | The API could not check the address | `UnknownEmail`, with every flag `nil` |

An `Email` carries four more flags, each `true` or `false`:

- `disposable`: a throwaway domain, such as temp-mail.org
- `free`: a free provider, such as Gmail or Outlook
- `role`: a shared mailbox, such as admin@ or support@
- `catchall`: the domain accepts mail for any name, so a `deliverable` result proves less

## Suggested corrections

Only when the domain does not resolve or publishes no MX records. Then `suggestions` can hold corrected addresses. The API does not validate them, so check one before you use it. Every other result returns an empty array.

## Cost

One lookup for a checked address. An `unknown` result is free, and so is a domain that does not resolve or has no MX records. The API rejects an address over 320 characters with an `AddressZen::ApiError`.

See [`email_validation`](https://docs.addresszen.com/docs/sdks/ruby/endpoints/email-validation) for the keywords.
