# `$client->keyAvailability()`

Availability

Returns public information on an API Key: whether it can be used right now (`available`), the search contexts the key is licensed for (`contexts`) and the context that best matches the caller's IP address (`context`).

The endpoint accepts API Keys (beginning `ak_`) and sub-licensed keys (beginning `sl_`), and needs no Management Key.

A key that exists but cannot be used, because it has no lookups left or has breached a limit, returns `200` with `"available": false`. An unknown or malformed key returns an error.

Supply a valid Management Key and the endpoint returns the key's private details instead, as `GET /keys/{key}/details` does. A Management Key that does not own the key is rejected.

## Endpoint

`GET /keys/{key}`

See the [API reference](https://docs.addresszen.com/docs/api/key-availability) for this endpoint.

## Signature

```php
public function keyAvailability(string $key): ApiKeyResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$key` | `string` | yes | API Key |

## Query Parameters

_None._

## Response

`AddressZen\Responses\ApiKeyResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="key-availability.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test');

$response = $client->keyAvailability('ak_test');

echo 'Available: ', var_export($response->result->available, true), PHP_EOL;
echo 'Context: ', $response->result->context, PHP_EOL;
```
