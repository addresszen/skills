# `$client->emailValidation()`

Email Validation

Validates an email address and reports whether it is deliverable.

Requires an API Key licensed for email validation. A query over 320 characters is rejected.

A validated address decrements your lookup balance. An address the API cannot check returns `unknown` and costs no lookup. An address whose domain does not resolve, or publishes no MX records, returns `not_deliverable` and also costs no lookup. Only those two domain failures populate `suggestions`. Every other response returns an empty list.

## Endpoint

`GET /emails`

See the [API reference](https://docs.addresszen.com/docs/api/email-validation) for this endpoint.

## Signature

```php
public function emailValidation(array $params): EmailResponse
```

## Arguments

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `$params` | `array` | yes | Query parameters. Keys under [Query Parameters](#query-parameters). |

## Query Parameters

Pass these as keys of `$params`.

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `query` | `string` | yes | Specifies the email address to validate |
| `tags` | `string\|list<string>` | no | Tags |

## Response

`AddressZen\Responses\EmailResponse`. Read fields as properties, such as `$response->result`, or as an array with the API's field names. `toArray()` returns the decoded body.

## Errors

An HTTP error throws `ApiException` with the HTTP status, the API error code from `getCode()` and the decoded body. A transport failure throws `TransporterException`. See [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

## Example

```php title="email-validation.php"
<?php

declare(strict_types=1);

use AddressZen\AddressZen;
use AddressZen\Types\Email;

require 'vendor/autoload.php';

$client = AddressZen::client('ak_test');

$response = $client->emailValidation(['query' => 'support@addresszen.com']);

$result = $response->result;

if ($result instanceof Email) {
    echo $result->result, PHP_EOL;
    echo 'Deliverable: ', var_export($result->deliverable, true), PHP_EOL;
    echo 'Disposable: ', var_export($result->disposable, true), PHP_EOL;
} else {
    echo 'Deliverability unknown', PHP_EOL;
}
```
