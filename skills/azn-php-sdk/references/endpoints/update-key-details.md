# `$client->updateKeyDetails()`

Update Details

Updates a key's settings and returns its private details. Only the fields you send change. A key on an unlimited plan ignores changes to `datasets`, `daily_limit` and `monthly_limit`. Datasets set by your plan cannot be changed here: sending one with a different value returns a 400.

## Endpoint

`PUT /keys/{key}/details`

See the [API reference](https://docs.addresszen.com/docs/api/update-key-details) for this endpoint.

This operation needs a Management Key. Pass it as the second argument to `AddressZen::client()`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/php/setup).

## Signature

```php
public function updateKeyDetails(string $key, array $body): ApiKeyDetailsResponse
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
| `name` | `string` | no | A name for the key |
| `daily_limit` | `array<string, mixed>` | no |  |
| `monthly_limit` | `array<string, mixed>` | no |  |
| `individual_limit` | `array<string, mixed>` | no |  |
| `allowed_urls` | `string\|list<string>` | no | A list of allowed URLs. An empty list disables the check. Up to 10 allowed. |
| `redact_days` | `int` | no | Number of days to preserve personal data stored in your key usage history. Set to 0 to prevent personal data storage |
| `notifications` | `array<string, mixed>` | no |  |
| `ip_forwarding` | `bool` | no | Accept IP addresses forwarded in the `AZ-Source-IP` header |
| `datasets` | `array<string, mixed>` | no | Datasets you can switch on or off for this key. Datasets set by your plan (`paf`, `mr`, `nyb`, `ecad`, `ecaf`) cannot be changed here: sending one with a different value returns a 400. |

## Response

`AddressZen\Responses\ApiKeyDetailsResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="update-key-details.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test', 'uk_test');

$response = $client->updateKeyDetails('ak_test', [
    'name' => 'Checkout',
    'allowed_urls' => ['https://www.example.com'],
]);

echo $response->result->name, PHP_EOL;
```
