# `$client->updateConfig()`

Update

Replaces a configuration's payload and returns the updated configuration. The name is fixed at creation.

## Endpoint

`POST /keys/{key}/configs/{config}`

See the [API reference](https://docs.addresszen.com/docs/api/update-config) for this endpoint.

This operation needs a Management Key. Pass it as the second argument to `AddressZen::client()`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/php/setup).

## Signature

```php
public function updateConfig(string $key, string $config, array $body): ConfigResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$key` | `string` | yes | API Key |
| `$config` | `string` | yes | Configuration Name |
| `$body` | `array` | yes | The JSON request body. Keys under [Request Body](#request-body). |

## Query Parameters

_None._

## Request Body

Pass these as keys of `$body`.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `payload` | `string` | no | A serialized payload of up to `65536` characters |

## Response

`AddressZen\Responses\ConfigResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="update-config.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test', 'uk_test');

$response = $client->updateConfig('ak_test', 'woocommerce', [
    'payload' => json_encode(['removeOrganisation' => true], JSON_THROW_ON_ERROR),
]);

echo $response->result->name, ' updated ', $response->result->updatedAt, PHP_EOL;
```
