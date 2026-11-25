# `$client->phoneNumberValidation()`

Phone Number Validation

Validates a phone number and returns its country, its national and international formats, and the network it was originally assigned to.

Requires an API Key licensed for phone validation.

Every query decrements your lookup balance, including a number that fails to parse and a number reported as invalid.

## Endpoint

`GET /phone_numbers`

See the [API reference](https://docs.addresszen.com/docs/api/phone-number-validation) for this endpoint.

## Signature

```php
public function phoneNumberValidation(array $params): PhoneNumberResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$params` | `array` | yes | Query parameters. Keys under [Query Parameters](#query-parameters). |

## Query Parameters

Pass these as keys of `$params`.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `query` | `string` | yes | Specifies the phone number to validate. Phone number must include a country code in an acceptable format. For instance, UK phone numbers should be prefixed with `+44`, `44` or `0044`. |
| `current_carrier` | `'true'` | no | When set to `true`, the API retrieves and populates the current network of the phone number. |
| `tags` | `string\|list<string>` | no | Tags |

## Response

`AddressZen\Responses\PhoneNumberResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="phone-number-validation.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;
use AddressZen\Types\PhoneNumber;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test');

$response = $client->phoneNumberValidation(['query' => '+1 202 555 0123']);

$result = $response->result;

if ($result instanceof PhoneNumber) {
    echo $result->internationalFormat, ' (', $result->country, ')', PHP_EOL;
} else {
    echo 'Invalid phone number', PHP_EOL;
}
```
