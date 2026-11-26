# `$client->retrieveAddress()`

Retrieve Address

Returns the full address for an autocomplete suggestion id.

This is the charged step of address autocomplete. A successful retrieval decrements your lookup balance. An id which resolves to no address returns `404`.

Every address comes back in one US-shaped format, whatever country or dataset it came from: up to two address lines and US field names such as `zip_code`, `state` and `city`.

## Endpoint

`GET /autocomplete/addresses/{address}/usa`

See the [API reference](https://docs.addresszen.com/docs/api/retrieve-address) for this endpoint.

## Signature

```php
public function retrieveAddress(string $address, array $params = []): UsaResolveAddressResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$address` | `string` | yes | ID of address suggestion |
| `$params` | `array` | no | Query parameters. Keys under [Query Parameters](#query-parameters). |

## Query Parameters

Pass these as keys of `$params`.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `licensee` | `string` | no | Licensee Key |
| `filter` | `string\|list<string>` | no | Restrict Result Fields |
| `tags` | `string\|list<string>` | no | Tags |
| `remove_firm` | `'true'` | no | Remove Firm |

## Response

`AddressZen\Responses\UsaResolveAddressResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="retrieve-address.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test');

$response = $client->retrieveAddress('usps_Z108703633|123||1119');

$address = $response->result;

echo $address->line1, PHP_EOL;
echo $address->lastLine, PHP_EOL;
```
