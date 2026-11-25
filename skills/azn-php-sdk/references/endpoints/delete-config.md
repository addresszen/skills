# `$client->deleteConfig()`

Delete

Permanently deletes a configuration object.

## Endpoint

`DELETE /keys/{key}/configs/{config}`

See the [API reference](https://docs.addresszen.com/docs/api/delete-config) for this endpoint.

This operation needs a Management Key. Pass it as the second argument to `AddressZen::client()`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/php/setup).

## Signature

```php
public function deleteConfig(string $key, string $config): DeleteConfigResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$key` | `string` | yes | API Key |
| `$config` | `string` | yes | Configuration Name |

## Query Parameters

_None._

## Response

`AddressZen\Responses\DeleteConfigResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="delete-config.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test', 'uk_test');

$response = $client->deleteConfig('ak_test', 'woocommerce');

echo 'Deleted: ', $response->result->deleted, PHP_EOL;
```
