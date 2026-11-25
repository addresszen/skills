# Responses

Every method returns a read-only object built from the API's JSON. Fields are properties in camelCase, and the same object answers to the API's own field names through array access.

```php title="fields.php"
$response = $client->retrieveAddress('usps_Z108703633|123||1119');
$address = $response->result;

echo $address->zipPlus4Code, PHP_EOL;        // property
echo $address['zip_plus_4_code'], PHP_EOL;   // the API's field name, same value
```

Objects cannot be changed. Setting or unsetting an array key throws `BadMethodCallException`.

## Get the raw array

Call `toArray()` on any response or nested object. It returns the decoded body with the API's field names, so it round-trips through `json_encode()`. Every object is also `JsonSerializable`.

```php title="array.php"
$data = $response->toArray();
echo json_encode($response, JSON_PRETTY_PRINT);
```

## Types

| Namespace | Holds |
| --- | --- |
| `AddressZen\Responses` | One class per operation response, such as `VerifyResponse` and `AutocompleteResponse`. Each has `code`, `message` and `result` |
| `AddressZen\Types` | Everything inside a result: `UsaVerifyMatch`, `Address`, `AddressSuggestion`, `Licensee`, `Config` and the native records |

Every class carries a PHPStan array shape for its `toArray()` form, and `AddressZen\Params` holds a shape for each method's `$params` and `$body`. PHPStan and IDEs that read array shapes check the keys you pass. `keyLogs()` is the exception: it returns the CSV as a string.

## Read a field with more than one shape

Some results come in one of several forms, and the SDK picks the class that matches. Check with `instanceof`.

| Field | Classes |
| --- | --- |
| `addressVerify()` result | `UsaVerifyMatch`, or `UsaVerifyNoMatch` when nothing matches: `match` is `null`, `count` is `0` and the address fields are empty strings |
| `UsaVerifyMatch` `match` | `UsaCassVerifiedAddress` for a CASS match in the United States, or `Address` for a match elsewhere, such as with `['context' => 'GBR']` in the params. An `Address` has a `dataset` and a `native` record |
| `Address` `native` | A class for the address's source dataset, such as `UspsAddress` or `PafAddress`; an array for a dataset the SDK does not know yet; or `null` |
| `Place` `native` | `GeonamesPlace`; an array for a dataset the SDK does not know yet; or `null` |
| `emailValidation()` result | `Email`, or `UnknownEmail` when deliverability cannot be checked |
| `phoneNumberValidation()` result | `PhoneNumber`, or `InvalidPhoneNumber` |

```php title="union.php"
use AddressZen\Types\UsaCassVerifiedAddress;
use AddressZen\Types\UsaVerifyMatch;

$result = $client->addressVerify(['query' => '1010 Cauthen Ln, Alamogordo, NM 88310'])->result;

if ($result instanceof UsaVerifyMatch && $result->match instanceof UsaCassVerifiedAddress) {
    echo $result->zipCode, ' with confidence ', $result->confidence, PHP_EOL;
}
```

## New API values

Your integration keeps working. Fields with a fixed set of values, such as `dpv` on a CASS match or `result` on an email, are typed as that set for PHPStan and your IDE, but the SDK does not check them at runtime. A value added to the API after your SDK version arrives as a plain string, so compare against the values you handle and fall through for the rest. A field the API adds does not break the response either, but it is left out of the object, `toArray()` and array access until an SDK version that knows it. The exception is `native`: a record from an unknown dataset is kept whole, as an array.

## Missing fields

A missing optional field is `null`, and `toArray()` leaves it out. A missing required field throws `MissingResponseField`, which names the field. That means the API and the SDK disagree, so report it to support. See [errors](https://docs.addresszen.com/docs/sdks/php/errors).

## Native records

`native` on an `Address` is the raw record from the address's source dataset, as a class named for the dataset, such as `PafAddress` for Royal Mail PAF. The `dataset` field on the address says which. A United States (`usps`) address has no native record, since the address already is the USPS record, so `native` is `null`. A dataset the SDK does not know yet comes back as a plain array, so a new dataset never breaks your integration.

```php title="native.php"
use AddressZen\Contracts\ResponseContract;

$address = $client->retrieveAddress('usps_Z108703633|123||1119')->result;

if ($address->native === null) {
    echo 'No native record for ', $address->dataset, PHP_EOL;
} elseif ($address->native instanceof ResponseContract) {
    echo $address->native::class, PHP_EOL;
} else {
    echo 'New dataset: ', $address->dataset, PHP_EOL;
}
```

The [data sources](https://docs.addresszen.com/docs/data) pages document every dataset's fields.
