# Autocomplete

`findAddress()` turns a partial address into suggestions as the user types. `retrieveAddress()` turns the chosen suggestion into a full address. Each search runs in one country, set with `context`.

```php title="autocomplete.php"
use AddressZen\AddressZen;

$client = AddressZen::client('ak_test');

$hits = $client->findAddress(['query' => '1010 Cauthen Ln', 'limit' => 5])->result->hits;
if ($hits === []) {
    exit('No matches');
}

$address = $client->retrieveAddress($hits[0]->id)->result;
echo $address->line1, ', ', $address->lastLine, PHP_EOL;
```

## Find suggestions

Call `findAddress()` with the partial address as `query`. The response holds `result->hits`, a list of `AddressSuggestion` objects with an `id` and a `suggestion` to show. An empty list means nothing matched. The suggestion format may change, so show it as it arrives rather than parsing it.

The same array takes any other [`findAddress()`](https://docs.addresszen.com/docs/sdks/php/endpoints/find-address) parameter: `limit`, `context` and the filters and biases, such as `state_code`, `postal_code` or `bias_lonlat`. Filters restrict results and biases promote them. Pass several terms for one filter as a list, such as `'state_code' => ['NM', 'TX']`, and the SDK joins them with commas. To favor addresses near the caller's IP address, pass `'bias_ip' => 'true'` as a string.

The SDK runs on your server. Have the browser send each keystroke to an endpoint of yours that calls `findAddress()`, so your key never leaves the server.

## Let users switch country

Set `context` to a three-letter ISO 3166-1 code, such as `USA`, `CAN` or `JPN`. Without it, the search uses your account's default country. `keyAvailability()` lists the countries a key can search. It needs only the API key and costs nothing.

```php title="countries.php"
use AddressZen\AddressZen;

$client = AddressZen::client('ak_test');
$key = $client->keyAvailability('ak_test')->result;

foreach ($key->contexts as $country) {
    echo $country->emoji, ' ', $country->description, ' ', $country->iso3, PHP_EOL;
}

$context = $key->context !== '' ? $key->context : $key->contexts[0]->iso3;
$hits = $client->findAddress(['query' => '1010 Cauthen Ln', 'context' => $context])->result->hits;
```

Each entry in `contexts` has `iso3` (the `context` code), `iso2`, `description` and `emoji`. `context` is the licensed country that best matches the IP address the request came from, or an empty string when none does. When the SDK runs on your server, that is your server's address, so take the user's choice over it.

## Retrieve the full address

Pass the hit's `id` to `retrieveAddress()`. The result is an `Address` in one US-shaped format, whatever the country: `line1`, `line2`, `lastLine`, `city`, `state`, `zipCode`, `zipPlus4Code`, `countryIso` and the other standard fields. A field the country's dataset does not carry is an empty string. See [responses](https://docs.addresszen.com/docs/sdks/php/responses) for how to read it.

`dataset` names the source, and `native` holds the raw record from that dataset when the API returns one. It is `null` otherwise, so narrow it before reading dataset-specific fields.

```php title="native.php"
use AddressZen\Types\UspsAddress;

$address = $client->retrieveAddress('usps_Z108703633|123||1119')->result;

if ($address->native instanceof UspsAddress) {
    echo $address->native->primaryNumber, PHP_EOL;
}
```

## Cost

Suggestions are free. Each `retrieveAddress()` costs one lookup. The API rate limits, then suspends, keys that request suggestions without retrieving any. The default limit is 3,000 suggestion requests per 5 minutes for each key and IP address.

## Search places

`findPlace()` and `resolvePlace()` work the same way for places: countries, administrative areas, capitals and other administrative seats. `findPlace()` returns up to 10 `PlaceSuggestion` hits with an `id` and a `descriptiveName` to show. `resolvePlace()` turns an `id` into a `Place`.

```php title="places.php"
$hits = $client->findPlace(['query' => 'Alamogordo', 'country_iso' => 'USA'])->result->hits;

if ($hits !== []) {
    $place = $client->resolvePlace($hits[0]->id)->result;
    echo $place->descriptiveName, ' ', $place->latitude, ', ', $place->longitude, PHP_EOL;
}
```

Place suggestions are free. Each `resolvePlace()` costs one lookup, and the API rate limits, then suspends, integrations that search without resolving.

## Errors

An HTTP error throws `ApiException`. An unknown suggestion `id` returns status `404`. A failed connection throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors) and [`retrieveAddress()`](https://docs.addresszen.com/docs/sdks/php/endpoints/retrieve-address) for the parameters.
