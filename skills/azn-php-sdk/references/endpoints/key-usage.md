# `$client->keyUsage()`

Usage Stats

Reports the number of lookups a key consumed over a date range, as a total and a daily breakdown.

The range defaults to the last 21 days. `start` and `end` take UNIX timestamps in milliseconds, and `end` defaults to the current time. The maximum range is 90 days.

Query at most three tags at once.

## Endpoint

`GET /keys/{key}/usage`

See the [API reference](https://docs.addresszen.com/docs/api/key-usage) for this endpoint.

This operation needs a Management Key. Pass it as the second argument to `AddressZen::client()`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/php/setup).

## Signature

```php
public function keyUsage(string $key, array $params = []): ApiKeyUsageResponse
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
| `start` | `int` | no | Start Timestamp |
| `end` | `int` | no | End Timestamp |
| `tags` | `string\|list<string>` | no | Tags |
| `licensee` | `string` | no | Licensee Key |

## Response

`AddressZen\Responses\ApiKeyUsageResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="key-usage.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test', 'uk_test');

$response = $client->keyUsage('ak_test', [
    'start' => strtotime('-7 days') * 1000,
    'end' => time() * 1000,
]);

foreach ($response->result->dailyCount as $day) {
    echo $day->date, ': ', $day->count, PHP_EOL;
}

echo 'Total: ', $response->result->total, PHP_EOL;
```
