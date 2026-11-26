# Licensees

A licensee is one of your customers using AddressZen through your key. Sub-licensing lets a platform serve many customers from one account and one bill while tracking each customer's usage separately.

Your key must be enabled for sub-licensing; [contact us](https://addresszen.com/contact) to switch one over. Every licensee method needs a [Management Key](https://docs.addresszen.com/docs/sdks/ruby/setup#management-key). The [sub-licensing guide](https://docs.addresszen.com/docs/guides/sublicensing) covers billing.

## Add a licensee

Call `create_licensee` with the customer's name and address. The new licensee's own key, beginning `sl_`, is in `key`.

```ruby title="create.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test", management_key: ENV.fetch("ADDRESSZEN_MANAGEMENT_KEY"))
licensee = client.create_licensee(
  "ak_test",
  name: "Example Inc",
  address: "1010 Cauthen Ln, Alamogordo, NM",
  postcode: "88310",
  whitelist: ["https://www.example.com"]
).result

puts "#{licensee.id} #{licensee.key}"
```

`postcode:` takes the customer's ZIP or postal code, whatever their country. `whitelist:` lists the URLs the licensee's key may be used from.

## List licensees

`list_licensees` returns 10 per call, or up to 100 with `limit:`, oldest first. Canceled licensees are left out. `query:` filters by name. For the next page, pass the last licensee's `id` as `starting_after:`. `has_more` says whether another page exists.

```ruby title="list.rb"
starting_after = nil

loop do
  page = client.list_licensees("ak_test", limit: 100, starting_after: starting_after).result
  page.licensees.each { |licensee| puts "#{licensee.name}: #{licensee.daily.count} lookups today" }
  break unless page.has_more

  starting_after = page.licensees.last.id
end
```

## Update or delete a licensee

Pass your key and the licensee's key:

- `update_licensee` changes the `address:`, `postcode:`, allowed URLs (`whitelist:`) or `daily:` limit. The name cannot change after creation
- `regenerate_licensee_key` issues a new `sl_` key and stops the old one immediately
- `delete_licensee` cancels the licensee and stops its key. Contact us to undo it

`retrieve_licensee` returns one licensee.

## Report one licensee's usage

Pass `licensee:` to [`key_usage`](https://docs.addresszen.com/docs/sdks/ruby/keys#export-usage) or `key_logs`. To make requests on a licensee's behalf, create a client with its `sl_` key as `api_key:`.

See [`create_licensee`](https://docs.addresszen.com/docs/sdks/ruby/endpoints/create-licensee) and [`list_licensees`](https://docs.addresszen.com/docs/sdks/ruby/endpoints/list-licensees) for every keyword.
