# API keys

The key methods show whether a key can take requests and which countries it covers. They also read limits, change settings and export usage. All of them except `key_availability` need a [Management Key](https://docs.addresszen.com/docs/sdks/ruby/setup#management-key), passed to `AddressZen::Client.new` as `management_key:`.

## Check a key

Call `key_availability`. It needs only the API key and costs nothing, so it also works as a health check.

```ruby title="availability.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")
key = client.key_availability("ak_test").result

puts key.available
key.contexts.each { |country| puts "#{country.emoji} #{country.description} #{country.iso_3}" }
```

`available` is `false` when the key has no lookups left, has hit a daily limit or is called from a URL it does not allow. `contexts` lists the licensed countries; pass an `iso_3` code as `context:` to [`find_address`](https://docs.addresszen.com/docs/sdks/ruby/endpoints/find-address). `context` is the licensed country that best matches the caller's IP address, or an empty string.

## Lookups remaining

`key_details` returns `lookups_remaining`, the daily, monthly and per-IP limits, allowed URLs, notification settings and datasets.

```ruby title="details.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: ENV.fetch("ADDRESSZEN_MANAGEMENT_KEY"))
details = client.key_details("ak_test").result

puts "#{details.lookups_remaining} lookups left, daily limit #{details.daily_limit&.limit || 'none'}"
```

## Change a limit

Call `update_key_details` with only the settings to change. Everything else stays as it is.

```ruby title="update.rb"
client.update_key_details(
  "ak_test",
  daily_limit: { "limit" => 1000 },
  allowed_urls: ["https://www.example.com"]
)
```

Nested settings use the API's own field names. A keyword left out, or passed as `nil`, is not sent. Inside a nested setting `nil` becomes JSON `null`, so `daily_limit: { "limit" => nil }` removes the daily limit, `allowed_urls: []` removes the URL restriction and `notifications: { "enabled" => false }` turns off notification emails. See [`update_key_details`](https://docs.addresszen.com/docs/sdks/ruby/endpoints/update-key-details) for every field.

## Export usage

`key_usage` returns totals and a daily breakdown. `key_logs` returns each billable lookup as a CSV string. Both take `start:` and `end:` as UNIX timestamps in milliseconds.

```ruby title="usage.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: ENV.fetch("ADDRESSZEN_MANAGEMENT_KEY"))
now = (Time.now.to_f * 1000).to_i
week_ago = now - (7 * 86_400_000)

usage = client.key_usage("ak_test", start: week_ago, end: now).result
usage.daily_count.each { |day| puts "#{day.date}: #{day.count}" }
puts "Total: #{usage.total}"

File.write("lookups.csv", client.key_logs("ak_test", start: week_ago, end: now))
```

`end:` works as a keyword argument even though `end` is a Ruby keyword. Pass `licensee:` as well to report one [licensee's](https://docs.addresszen.com/docs/sdks/ruby/licensees) usage.

## Saved configs

A config is a named JSON string stored against your key, such as the settings for an ecommerce plugin. `list_configs`, `create_config`, `update_config` and `delete_config` need the Management Key. `retrieve_config` needs no credentials, so an integration can read its own config at runtime. See [`create_config`](https://docs.addresszen.com/docs/sdks/ruby/endpoints/create-config) for the keywords.
