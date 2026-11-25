# Phone validation

`phoneNumberValidation()` checks a phone number from any country and returns it in national and international format, with its country and the network it was assigned to.

```php title="phone.php"
use AddressZen\AddressZen;
use AddressZen\Types\PhoneNumber;

$client = AddressZen::client('ak_test');
$phone = $client->phoneNumberValidation(['query' => '+1 202 555 0123'])->result;

if ($phone instanceof PhoneNumber) {
    echo $phone->internationalFormat, ' ', $phone->isoCountry, ' ', $phone->originalCarrier?->name, PHP_EOL;
} else {
    echo 'Invalid phone number', PHP_EOL;
}
```

The number must include its country code: `+1` for the US and Canada, `+44` for the UK, `+81` for Japan. Your key needs phone validation enabled.

## Read the result

A valid number returns a `PhoneNumber` with `valid` `true` and:

| Property | Contents |
| --- | --- |
| `nationalFormat` | The number as dialed inside its country |
| `internationalFormat` | The number with its country code |
| `isoCountry` and `isoCountry2` | Three- and two-letter country codes, such as `USA` and `US` |
| `country` | Country name |
| `originalCarrier` | A `Carrier` for the network the number was first assigned to, with `name` and `networkType` such as `mobile`, `landline` or `virtual` |

An invalid number returns an `InvalidPhoneNumber` with `valid` `false` and every other property `null`. It is not an error, so check the class before reading the formats.

## Current network

Add `'current_carrier' => 'true'` alongside `query` to fill `currentCarrier` as well. Pass the string `'true'`, not PHP `true`. A number can move to another network, so `originalCarrier` alone can be out of date. The extra check can be slow on some networks, so allow for it in your [request timeout](https://docs.addresszen.com/docs/sdks/php/setup#set-a-request-timeout).

## Cost

One lookup per request, including numbers that are invalid or fail to parse.

See [`phoneNumberValidation()`](https://docs.addresszen.com/docs/sdks/php/endpoints/phone-number-validation) for the parameters.
