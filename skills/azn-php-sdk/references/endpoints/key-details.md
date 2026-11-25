# `$client->keyDetails()`

Details

Returns private data on a key: remaining lookups, licensed datasets, usage limits, notification settings and the search contexts the key can serve.

## Endpoint

`GET /keys/{key}/details`

See the [API reference](https://docs.addresszen.com/docs/api/key-details) for this endpoint.

This operation needs a Management Key. Pass it as the second argument to `AddressZen::client()`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/php/setup).

## Signature

```php
public function keyDetails(string $key): ApiKeyDetailsResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$key` | `string` | yes | API Key |

## Query Parameters

_None._

## Response

`AddressZen\Responses\ApiKeyDetailsResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="key-details.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test', 'uk_test');

$response = $client->keyDetails('ak_test');

echo $response->result->name, ': ', $response->result->lookupsRemaining, ' lookups remaining', PHP_EOL;
```
