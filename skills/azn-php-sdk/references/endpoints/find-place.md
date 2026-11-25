# `$client->findPlace()`

Find Place

Returns place suggestions for a query, ranked by relevance. Places cover countries, administrative areas, capitals and other administrative seats.

## Implementing Place Autocomplete

Retrieving a full place takes two requests:

1. Fetch suggestions from `/places`
2. Fetch the place using the `id` on a suggestion

A query returns at most 10 suggestions. An empty query returns an empty result set. Show users the `descriptive_name`. The API drops suggestions that share one, so each name in a response identifies a single place.

## Rate Limiting and Cost

The rate limit is 3,000 requests per 5 minutes.

`/places` does not decrement your lookup balance, but resolving a suggestion to a full place does. We rate limit and then suspend integrations that repeatedly call `/places` without resolving.

## Endpoint

`GET /places`

See the [API reference](https://docs.addresszen.com/docs/api/find-place) for this endpoint.

## Signature

```php
public function findPlace(array $params = []): PlaceResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$params` | `array` | no | Query parameters. Keys under [Query Parameters](#query-parameters). |

## Query Parameters

Pass these as keys of `$params`.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `query` | `string` | no | Specifies the place to query. Can be shortened to `q=` |
| `country_iso` | `string\|list<string>` | no | Filter by Country |
| `bias_country_iso` | `string\|list<string>` | no | Bias by Country Bias by country ISO code. Uses 3 letter country code (ISO 3166-1) standard. Bias by multiple countries with a comma separated list. E.g. `GBR,IRL` |
| `bias_lonlat` | `string` | no | Bias by Geolocation |
| `bias_ip` | `'true'` | no | Bias by Geolocation of IP |

## Response

`AddressZen\Responses\PlaceResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="find-place.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test');

$response = $client->findPlace(['query' => 'Springfield', 'country_iso' => 'USA']);

foreach ($response->result->hits as $place) {
    echo $place->id, ': ', $place->descriptiveName, PHP_EOL;
}
```
