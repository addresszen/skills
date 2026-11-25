# `$client->updateLicensee()`

Update

Updates a licensee's address, postcode, allowed URLs and daily limit. Returns the updated licensee. The name is fixed at creation.

## Endpoint

`POST /keys/{key}/licensees/{licensee}`

See the [API reference](https://docs.addresszen.com/docs/api/update-licensee) for this endpoint.

This operation needs a Management Key. Pass it as the second argument to `AddressZen::client()`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/php/setup).

## Signature

```php
public function updateLicensee(string $key, string $licensee, array $body): LicenseeResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$key` | `string` | yes | API Key |
| `$licensee` | `string` | yes | Licensee Key |
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

```php title="update-licensee.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test', 'uk_test');

$response = $client->updateLicensee('ak_test', 'sl_hk71kco54zGSGvF9eXXrvvnMOLLNh', [
    'name' => 'Acme Inc',
]);

echo $response->result->name, PHP_EOL;
```
