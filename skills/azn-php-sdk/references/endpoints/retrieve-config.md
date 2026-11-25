# `$client->retrieveConfig()`

Retrieve

Returns a configuration by name. This request needs no `user_token`, so a browser integration can read its own configuration at runtime.

## Endpoint

`GET /keys/{key}/configs/{config}`

See the [API reference](https://docs.addresszen.com/docs/api/retrieve-config) for this endpoint.

## Signature

```php
public function retrieveConfig(string $key, string $config): ConfigResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$key` | `string` | yes | API Key |
| `$config` | `string` | yes | Configuration Name |

## Query Parameters

_None._

## Response

`AddressZen\Responses\ConfigResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="retrieve-config.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test');

$response = $client->retrieveConfig('ak_test', 'woocommerce');

echo $response->result->payload, PHP_EOL;
```
