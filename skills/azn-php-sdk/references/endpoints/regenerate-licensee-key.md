# `$client->regenerateLicenseeKey()`

Regenerate Key

Regenerates a licensee's key and returns the licensee with the new key. The previous key stops working immediately, so update any integration that uses it.

## Endpoint

`POST /keys/{key}/licensees/{licensee}/regenerate-key`

This operation needs a Management Key. Pass it as the second argument to `AddressZen::client()`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/php/setup).

## Signature

```php
public function regenerateLicenseeKey(string $key, string $licensee): LicenseeResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$key` | `string` | yes | API Key |
| `$licensee` | `string` | yes | Licensee Key |

## Query Parameters

_None._

## Response

`AddressZen\Responses\LicenseeResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="regenerate-licensee-key.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test', 'uk_test');

$response = $client->regenerateLicenseeKey('ak_test', 'sl_hk71kco54zGSGvF9eXXrvvnMOLLNh');

echo 'New licensee key: ', $response->result->key, PHP_EOL;
```
