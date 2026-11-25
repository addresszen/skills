# API keys

The key methods show whether a key can take requests and which countries it covers. They also read limits, change settings and export usage. All of them except `keyAvailability()` need a [Management Key](https://docs.addresszen.com/docs/sdks/php/setup#management-key), passed as the second argument to `AddressZen::client()` or through `Factory::withManagementKey()`.

## Check a key

Call `keyAvailability()`. It needs only the API key and costs nothing, so it also works as a health check.

```php title="availability.php"
use AddressZen\AddressZen;

$client = AddressZen::client('ak_test');
$key = $client->keyAvailability('ak_test')->result;

echo var_export($key->available, true), PHP_EOL;
foreach ($key->contexts as $country) {
    echo $country->emoji, ' ', $country->description, ' ', $country->iso3, PHP_EOL;
}
```

`available` is `false` when the key has no lookups left, has hit a daily limit or is called from a URL it does not allow. `contexts` lists the licensed countries; pass an `iso3` code as `context` to [`findAddress()`](https://docs.addresszen.com/docs/sdks/php/endpoints/find-address). `context` is the licensed country that best matches the caller's IP address, or an empty string.

## Lookups remaining

`keyDetails()` returns `lookupsRemaining`, the daily, monthly and per-IP limits, allowed URLs, notification settings and datasets.

```php title="details.php"
use AddressZen\AddressZen;

$client = AddressZen::client('ak_test', getenv('ADDRESSZEN_MANAGEMENT_KEY'));
$details = $client->keyDetails('ak_test')->result;

echo $details->lookupsRemaining, ' lookups left, daily limit ', $details->dailyLimit->limit ?? 'none', PHP_EOL;
```

## Change a limit

Call `updateKeyDetails()` with only the settings to change. Everything else stays as it is.

```php title="update.php"
use AddressZen\AddressZen;

$client = AddressZen::client('ak_test', getenv('ADDRESSZEN_MANAGEMENT_KEY'));
$client->updateKeyDetails('ak_test', [
    'daily_limit' => ['limit' => 1000],
    'allowed_urls' => ['https://www.example.com'],
]);
```

The body uses the API's own field names. `null` inside a nested setting becomes JSON `null`, so `['daily_limit' => ['limit' => null]]` removes the daily limit, `['allowed_urls' => []]` removes the URL restriction and `['notifications' => ['enabled' => false]]` turns off notification emails. See [`updateKeyDetails()`](https://docs.addresszen.com/docs/sdks/php/endpoints/update-key-details) for every field.

## Export usage

`keyUsage()` returns totals and a daily breakdown. `keyLogs()` returns each billable lookup as a CSV string. Both take `start` and `end` as UNIX timestamps in milliseconds.

```php title="usage.php"
use AddressZen\AddressZen;

$client = AddressZen::client('ak_test', getenv('ADDRESSZEN_MANAGEMENT_KEY'));
$range = ['start' => strtotime('-7 days') * 1000, 'end' => time() * 1000];

$usage = $client->keyUsage('ak_test', $range)->result;
foreach ($usage->dailyCount as $day) {
    echo $day->date, ': ', $day->count, PHP_EOL;
}
echo 'Total: ', $usage->total, PHP_EOL;

file_put_contents('lookups.csv', $client->keyLogs('ak_test', $range));
```

Pass `licensee` in the same array to report one [licensee's](https://docs.addresszen.com/docs/sdks/php/licensees) usage.

## Saved configs

A config is a named JSON string stored against your key, such as the settings for an ecommerce plugin. `listConfigs()`, `createConfig()`, `updateConfig()` and `deleteConfig()` need the Management Key. `retrieveConfig()` needs no credentials, so an integration can read its own config at runtime. See [`createConfig()`](https://docs.addresszen.com/docs/sdks/php/endpoints/create-config) for the body.
