# `$client->listConfigs()`

List

Returns every configuration stored against a key, oldest first.

## Endpoint

`GET /keys/{key}/configs`

See the [API reference](https://docs.addresszen.com/docs/api/list-configs) for this endpoint.

This operation needs a Management Key. Pass it as the second argument to `AddressZen::client()`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/php/setup).

## Signature

```php
public function listConfigs(string $key): ConfigsResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$key` | `string` | yes | API Key |

## Query Parameters

_None._

## Response

`AddressZen\Responses\ConfigsResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="list-configs.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test', 'uk_test');

$response = $client->listConfigs('ak_test');

foreach ($response->result->configs as $config) {
    echo $config->name, ' updated ', $config->updatedAt, PHP_EOL;
}
```
