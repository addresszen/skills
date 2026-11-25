# `$client->createLicensee()`

Create

Creates a licensee on a key and returns it with its generated `sl_` key. The key must be enabled for sub-licensing.

## Endpoint

`POST /keys/{key}/licensees`

See the [API reference](https://docs.addresszen.com/docs/api/create-licensee) for this endpoint.

This operation needs a Management Key. Pass it as the second argument to `AddressZen::client()`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/php/setup).

## Signature

```php
public function createLicensee(string $key, array $body): LicenseeResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$key` | `string` | yes | API Key |
| `$body` | `array` | yes | The JSON request body. Keys under [Request Body](#request-body). |

## Query Parameters

_None._

## Request Body

Pass these as keys of `$body`.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `name` | `string` | no | Licensee individual or organisation name |
| `address` | `string` | no | Licensee's first, second and third line address as well as post town concatenated by commas |
| `postcode` | `string` | no | Licensee's postcode |
| `whitelist` | `string\|list<string>` | no | A list of allowed URLs. An empty list disables the check. |
| `daily` | `array<string, mixed>` | no |  |

## Response

`AddressZen\Responses\LicenseeResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="create-licensee.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test', 'uk_test');

$response = $client->createLicensee('ak_test', [
    'name' => 'Acme Inc',
    'address' => '1010 Cauthen Ln, Alamogordo, NM',
    'postcode' => '88310',
    'whitelist' => ['https://www.acme.example'],
]);

echo 'Licensee key: ', $response->result->key, PHP_EOL;
```
