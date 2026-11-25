# Licensees

A licensee is one of your customers using AddressZen through your key. Sub-licensing lets a platform serve many customers from one account and one bill while tracking each customer's usage separately.

Your key must be enabled for sub-licensing; [contact us](https://addresszen.com/contact) to switch one over. Every licensee method needs a [Management Key](https://docs.addresszen.com/docs/sdks/php/setup#management-key). The [sub-licensing guide](https://docs.addresszen.com/docs/guides/sublicensing) covers billing.

## Add a licensee

Call `createLicensee()` with the customer's name and address. The new licensee's own key, beginning `sl_`, is in `key`.

```php title="create.php"
use AddressZen\AddressZen;

$client = AddressZen::client('ak_test', getenv('ADDRESSZEN_MANAGEMENT_KEY'));
$licensee = $client->createLicensee('ak_test', [
    'name' => 'Example Inc',
    'address' => '1010 Cauthen Ln, Alamogordo, NM',
    'postcode' => '88310',
    'whitelist' => ['https://www.example.com'],
])->result;

echo $licensee->id, ' ', $licensee->key, PHP_EOL;
```

`postcode` takes the customer's ZIP or postal code, whatever their country. `whitelist` lists the URLs the licensee's key may be used from.

## List licensees

`listLicensees()` returns 10 per call, or up to 100 with `limit`, oldest first. Canceled licensees are left out. `query` filters by name. For the next page, pass the last licensee's `id` as `starting_after`. `hasMore` says whether another page exists.

```php title="list.php"
use AddressZen\AddressZen;

$client = AddressZen::client('ak_test', getenv('ADDRESSZEN_MANAGEMENT_KEY'));
$page = $client->listLicensees('ak_test', ['limit' => 100])->result;

foreach ($page->licensees as $licensee) {
    echo $licensee->name, ': ', $licensee->daily->count, ' lookups today', PHP_EOL;
}
```

## Update or delete a licensee

Pass your key and the licensee's key:

- `updateLicensee()` changes the `address`, `postcode`, allowed URLs (`whitelist`) or `daily` limit. The name cannot change after creation
- `regenerateLicenseeKey()` issues a new `sl_` key and stops the old one immediately
- `deleteLicensee()` cancels the licensee and stops its key. Contact us to undo it

`retrieveLicensee()` returns one licensee.

## Report one licensee's usage

Pass `licensee` to [`keyUsage()`](https://docs.addresszen.com/docs/sdks/php/keys#export-usage) or `keyLogs()`.

See [`createLicensee()`](https://docs.addresszen.com/docs/sdks/php/endpoints/create-licensee) and [`listLicensees()`](https://docs.addresszen.com/docs/sdks/php/endpoints/list-licensees) for the body and parameters.
