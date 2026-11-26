# `$client->findAddress()`

Find Address

Returns address suggestions for a partial address, ranked by relevance. Use it to autofill an address form as the user types.

A suggestion is a display label and an `id`, not a full address. Retrieve the address with a second request to `/autocomplete/addresses/{id}/usa`. That second request is the one which decrements your lookup balance.

Autocomplete is not a free standalone resource. We rate limit, then suspend, keys that autocomplete without resolving suggestions.

Our address autocomplete JavaScript libraries add this to a form without calling the API directly.

## Coverage

Each search runs in one country, selected with `context`. A missing or unrecognized `context` falls back to your account default. Results come from the datasets enabled on your key: USPS ZIP+4 for the US and its territories, and the country datasets you license elsewhere. Where a key has more than one dataset for a country, `dataset` narrows the search.

## Filters

Filters restrict results, e.g. `state_code=NY` searches New York only. A filter which matches no address returns an empty set. An unrecognized filter name is ignored. Neither affects your lookup balance.

Filters combine with `AND` logic, so `state_code=CA&city=San Francisco` requires both. A comma-separated value combines terms for one filter, e.g. `postal_code_3=11225,11226,11238` accepts any of the three ZIP codes. Unless a parameter states otherwise, every filter takes multiple terms. The maximum is 10 filter terms.

## Address bias

Bias terms carry the `bias_` prefix and promote addresses rather than restricting the set, so unmatched addresses still appear, lower down. For example, `bias_state_code=NY,NJ` favors addresses in New York and New Jersey, and `bias_lonlat` favors addresses near a point. Invalid bias terms have no effect. Multiple bias terms are allowed unless stated otherwise, with a combined maximum of 5.

## Suggestion format

The suggestion string is subject to change. Present it to the user as it arrives rather than parsing it.

## Rate limiting and cost

The default rate limit is 3,000 requests per 5 minutes, counted per API key and IP address. The `X-RateLimit-Limit`, `X-RateLimit-Remaining` and `X-RateLimit-Reset` headers report the current window.

Autocomplete requests do not draw on your balance. Resolving a suggestion to a full address does.

## Endpoint

`GET /autocomplete/addresses`

See the [API reference](https://docs.addresszen.com/docs/api/find-address) for this endpoint.

## Signature

```php
public function findAddress(array $params = []): AutocompleteResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$params` | `array` | no | Query parameters. Keys under [Query Parameters](#query-parameters). |

## Query Parameters

Pass these as keys of `$params`.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `query` | `string` | no | Address Query |
| `dataset` | `string\|list<string>` | no | Filter by Dataset |
| `context` | `string` | no | Context |
| `limit` | `int` | no | Limit |
| `bias_lonlat` | `string` | no | Bias by Geolocation |
| `bias_ip` | `'true'` | no | Bias by Geolocation of IP |
| `box` | `string\|list<string>` | no | Filter by Bounding Box |
| `postal_code` | `string` | no | Filter by postal code |
| `postal_code_2` | `string` | no | Filter by postal code prefix |
| `postal_code_3` | `string` | no | Filter by short postal code |
| `city` | `string` | no | Filter by city |
| `state` | `string` | no | Filter by state |
| `state_code` | `string` | no | Filter by state code |
| `bias_postal_code` | `string` | no | Bias by postal code |
| `bias_postal_code_2` | `string` | no | Bias by postal code prefix |
| `bias_postal_code_3` | `string` | no | Bias by short postal code |
| `bias_city` | `string` | no | Bias by city |
| `bias_state` | `string` | no | Bias by state |
| `bias_state_code` | `string` | no | Bias by state code |
| `is_pobox` | `'true'\|'false'` | no | Filter by PO Box |
| `is_business` | `'true'\|'false'` | no | Filter by business address |

## Response

`AddressZen\Responses\AutocompleteResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="find-address.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test');

$response = $client->findAddress(['query' => '1010 Cauthen Ln', 'limit' => 5]);

foreach ($response->result->hits as $hit) {
    echo $hit->id, ': ', $hit->suggestion, PHP_EOL;
}
```
