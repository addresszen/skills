# `$client->resolvePlace()`

Resolve Place

Returns the full place for a place ID taken from a `/places` suggestion.

On top of the fields carried by the suggestion, the response adds coordinates, language and the underlying dataset record.

Each request decrements your lookup balance. An unknown ID returns `404`.

## Endpoint

`GET /places/{place}`

See the [API reference](https://docs.addresszen.com/docs/api/resolve-place) for this endpoint.

## Signature

```php
public function resolvePlace(string $place, array $params = []): ResolvePlaceResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$place` | `string` | yes | ID of place suggestion |
| `$params` | `array` | no | Query parameters. Keys under [Query Parameters](#query-parameters). |

## Query Parameters

Pass these as keys of `$params`.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `tags` | `string\|list<string>` | no | Tags |

## Response

`AddressZen\Responses\ResolvePlaceResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="resolve-place.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test');

$response = $client->resolvePlace('geonames_5128581');

$place = $response->result;

echo $place->descriptiveName, ' (', $place->countryIso, ')', PHP_EOL;
echo $place->latitude, ', ', $place->longitude, PHP_EOL;
```
