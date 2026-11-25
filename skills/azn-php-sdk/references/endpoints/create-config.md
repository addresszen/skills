# `$client->createConfig()`

Create

Creates a named configuration on a key and returns it.

## Endpoint

`POST /keys/{key}/configs`

See the [API reference](https://docs.addresszen.com/docs/api/create-config) for this endpoint.

This operation needs a Management Key. Pass it as the second argument to `AddressZen::client()`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/php/setup).

## Signature

```php
public function createConfig(string $key, array $body): ConfigResponse
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
| `name` | `string` | yes | A unique name to identify the configuration payload |
| `payload` | `string` | yes | A serialized payload of up to `65536` characters |

## Response

`AddressZen\Responses\ConfigResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="create-config.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test', 'uk_test');

$response = $client->createConfig('ak_test', [
    'name' => 'woocommerce',
    'payload' => json_encode(['removeOrganisation' => false], JSON_THROW_ON_ERROR),
]);

echo $response->result->name, ' created ', $response->result->createdAt, PHP_EOL;
```
