# `$client->retrieveLicensee()`

Retrieve

Returns a licensee by its `sl_` key. A canceled or unknown licensee returns `404`.

## Endpoint

`GET /keys/{key}/licensees/{licensee}`

See the [API reference](https://docs.addresszen.com/docs/api/retrieve-licensee) for this endpoint.

This operation needs a Management Key. Pass it as the second argument to `AddressZen::client()`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/php/setup).

## Signature

```php
public function retrieveLicensee(string $key, string $licensee): LicenseeResponse
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

```php title="retrieve-licensee.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test', 'uk_test');

$response = $client->retrieveLicensee('ak_test', 'sl_hk71kco54zGSGvF9eXXrvvnMOLLNh');

echo $response->result->name, ': ', $response->result->key, PHP_EOL;
```
