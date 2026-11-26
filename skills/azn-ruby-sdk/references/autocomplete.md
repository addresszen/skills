# Autocomplete

`find_address` turns a partial address into suggestions as the user types. `retrieve_address` turns the chosen suggestion into a full address. Each search runs in one country, set with `context:`.

```ruby title="autocomplete.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")

hits = client.find_address(query: "1010 Cauthen Ln", limit: 5).result.hits
abort "No matches" if hits.empty?

address = client.retrieve_address(hits.first.id).result
puts "#{address.line_1}, #{address.last_line}"
```

## Find suggestions

Call `find_address` with the partial address as `query:`. The response holds `result.hits`, an array of `AddressSuggestion` objects with an `id` and a `suggestion` to show. An empty array means nothing matched. The suggestion format may change, so show it as it arrives rather than parsing it.

It takes every other [`find_address`](https://docs.addresszen.com/docs/sdks/ruby/endpoints/find-address) keyword too: `limit:`, `context:` and the filters and biases, such as `state_code:`, `postal_code:` or `bias_lonlat:`. Filters restrict results and biases promote them. Pass several terms for one filter as a comma-separated string, such as `state_code: "NM,TX"`. To favor addresses near the caller's IP address, pass `bias_ip: "true"`.

The SDK runs on your server. Have the browser send each keystroke to an endpoint of yours that calls `find_address`, so your key never leaves the server.

## Let users switch country

Set `context:` to a three-letter ISO 3166-1 code, such as `USA`, `CAN` or `JPN`. Without it, the search uses your account's default country. `key_availability` lists the countries a key can search. It needs only the API key and costs nothing.

```ruby title="countries.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")
key = client.key_availability("ak_test").result

key.contexts.each do |country|
  puts "#{country.emoji} #{country.description} #{country.iso_3}"
end

context = key.context.empty? ? key.contexts.first.iso_3 : key.context
hits = client.find_address(query: "1010 Cauthen Ln", context: context).result.hits
```

Each entry in `contexts` has `iso_3` (the `context:` code), `iso_2`, `description` and `emoji`. `context` is the licensed country that best matches the IP address the request came from, or an empty string when none does. When the SDK runs on your server, that is your server's address, so take the user's choice over it.

## Retrieve the full address

Pass the hit's `id` to `retrieve_address`. The result is an `Address` in one US-shaped format, whatever the country: `line_1`, `line_2`, `last_line`, `city`, `state`, `zip_code`, `zip_plus_4_code`, `country_iso` and the other standard fields. A field the country's dataset does not carry is an empty string. See [responses](https://docs.addresszen.com/docs/sdks/ruby/responses) for how to read it.

`dataset` names the source. A United States address comes from `usps` and has no native record, so its `native` is `nil`. An address from another country's dataset carries that dataset's raw record in `native`; see [native records](https://docs.addresszen.com/docs/sdks/ruby/responses#native-records).

## Cost

Suggestions are free. Each `retrieve_address` costs one lookup. The API rate limits, then suspends, keys that request suggestions without retrieving any. The default limit is 3,000 suggestion requests per 5 minutes for each key and IP address.

## Search places

`find_place` and `resolve_place` work the same way for places: countries, administrative areas, capitals and other administrative seats. `find_place` returns up to 10 `PlaceSuggestion` hits with an `id` and a `descriptive_name` to show. `resolve_place` turns an `id` into a `Place`.

```ruby title="places.rb"
hits = client.find_place(query: "Alamogordo", country_iso: "USA").result.hits

unless hits.empty?
  place = client.resolve_place(hits.first.id).result
  puts "#{place.descriptive_name} #{place.latitude}, #{place.longitude}"
end
```

Place suggestions are free. Each `resolve_place` costs one lookup, and the API rate limits, then suspends, integrations that search without resolving.

## Errors

An HTTP error raises `AddressZen::ApiError`. An unknown suggestion `id` returns status `404`. A failed connection raises `AddressZen::TransportError`. See [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors) and [`retrieve_address`](https://docs.addresszen.com/docs/sdks/ruby/endpoints/retrieve-address) for the keywords.
