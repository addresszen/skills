# `$client->keyLogs()`

Logs (CSV)

Returns a CSV of the charged lookups made on a key, one row per request.

Requires the account Management Key. The maximum interval is 90 days. Without a start or end date the interval is the last 21 days.

The response is `text/csv` and downloads as an attachment. A non-200 response reverts to JSON, with the error code and message in the body.

## CSV format

The CSV has no header row. Columns, in order:

1. Timestamp (ISO 8601)
2. IP address the request was received from
3. Search term
4. URL the request originated from
5. Lookup type
6. Tags
7. Lookups consumed
8. Licensee name (sublicensing keys only)
9. Source IP address

The source IP column carries the address forwarded in the `AZ-Source-IP` header. We record it only for keys with IP address forwarding enabled, and only when the header holds a valid IP address. It is empty otherwise.

## Data redaction

We redact personally identifiable data (PII) in your usage log weekly, covering the IP, source IP, search term and URL columns.

The default retention is 28 days. Change the period from your dashboard. Set it to `0` days to stop collecting PII altogether.

## Endpoint

`GET /keys/{key}/lookups`

See the [API reference](https://docs.addresszen.com/docs/api/key-logs) for this endpoint.

This operation needs a Management Key. Pass it as the second argument to `AddressZen::client()`, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/php/setup).

## Signature

```php
public function keyLogs(string $key, array $params = []): string
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
| `licensee` | `string` | no | Licensee Key |

## Response

The CSV text, as a `string`.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="key-logs.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test', 'uk_test');

$csv = $client->keyLogs('ak_test', [
    'start' => strtotime('-7 days') * 1000,
    'end' => time() * 1000,
]);

echo $csv;
```
