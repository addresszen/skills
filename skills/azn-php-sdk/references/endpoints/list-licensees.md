# `$client->listLicensees()`

List

Returns a key's licensees, oldest first, up to 100 per request. The list omits canceled licensees. The key must be enabled for sub-licensing.

## Endpoint

`GET /keys/{key}/licensees`

See the [API reference](https://docs.addresszen.com/docs/api/list-licensees) for this endpoint.

This operation needs a Management Key. Pass it as the second argument to `AddressZen::client()`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/php/setup).

## Signature

```php
public function listLicensees(string $key, array $params = []): LicenseesResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$key` | `string` | yes | API Key |
| `$params` | `array` | no | Query parameters. Keys under [Query Parameters](#query-parameters). |

## Query Parameters

Pass these as keys of `$params`.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `starting_after` | `string` | no | ID of the licensee after which to list results. Pass the `id` of the last licensee on the previous page. |
| `limit` | `int` | no | Limit |
| `query` | `string` | no | Filter results by licensee name. Can be shortened to `q=` |

## Response

`AddressZen\Responses\LicenseesResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="list-licensees.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test', 'uk_test');

$response = $client->listLicensees('ak_test', ['limit' => 10]);

foreach ($response->result->licensees as $licensee) {
    echo $licensee->id, ': ', $licensee->name, ' (', $licensee->key, ')', PHP_EOL;
}

echo 'More pages: ', var_export($response->result->hasMore, true), PHP_EOL;
```
