---
name: azn-php-sdk
description: Use when integrating the AddressZen PHP SDK (addresszen/sdk on Packagist), its Symfony bundle or its Laravel package. Covers US address verification, autocomplete, email and phone validation, API keys, licensees and error handling, plus a reference for every API operation.
license: SEE LICENSE IN LICENSE
metadata:
  author: addresszen
  homepage: https://addresszen.com
references:
  - setup.md
  - address-verify.md
  - autocomplete.md
  - email-validation.md
  - phone-validation.md
  - keys.md
  - licensees.md
  - responses.md
  - errors.md
  - endpoints/
---

# AddressZen PHP SDK

Call the AddressZen API from PHP 8.2 or later with one typed method per API operation and read-only response objects. The SDK sends requests through the PSR-18 client already in the project, found by `php-http/discovery`, so Guzzle and Symfony HttpClient both work.

```bash
composer require addresszen/sdk
```

```php
use AddressZen\AddressZen;
use AddressZen\Types\UsaVerifyMatch;

$client = AddressZen::client('ak_test');

$result = $client->addressVerify(['query' => '1010 Cauthen Ln, Alamogordo, NM 88310'])->result;
if ($result instanceof UsaVerifyMatch) {
    echo $result->addressLineOne, ', ', $result->city, ', ', $result->state, ' ', $result->zipCode, PHP_EOL;
}
```

Create one client and reuse it. Each API operation is one method on it, named from its operation ID: `addressVerify()`, `findAddress()`, `retrieveAddress()`, `findPlace()`, `resolvePlace()`, `emailValidation()`, `phoneNumberValidation()`, `keyAvailability()`, `keyDetails()`, `updateKeyDetails()`, `keyUsage()`, `keyLogs()`, `listLicensees()`, `createLicensee()`, `retrieveLicensee()`, `updateLicensee()`, `deleteLicensee()`, `regenerateLicenseeKey()`, `listConfigs()`, `createConfig()`, `retrieveConfig()`, `updateConfig()` and `deleteConfig()`. Path parameters are positional, then `$body` for operations that take a JSON body, then `$params` for query parameters, in the API's snake_case names. The address to verify is the `query` key of `$body`; the search text for autocomplete, email and phone is the `query` key of `$params`, as in `$client->findAddress(['query' => '1010 Cauthen Ln', 'limit' => 5])`. Responses are read-only objects with camelCase properties, the API's own field names through array access, `toArray()` for the decoded body and `JsonSerializable`.

## Scope

Every API operation has a method, including autocomplete (`findAddress()` then `retrieveAddress()`), place search, configs, licensees, email and phone validation. There are no conveniences beyond the generated methods. Results that can take more than one shape are PHP unions: check them with `instanceof` (`UsaVerifyMatch` or `UsaVerifyNoMatch`, `Email` or `UnknownEmail`, `PhoneNumber` or `InvalidPhoneNumber`). The guides cover the common tasks; `references/endpoints/` has one page per method.

## Authentication and errors

Pass the API key to `AddressZen::client()`. Key management (except `keyAvailability()`), licensee and config methods (except `retrieveConfig()`) also need a Management Key (`uk_...`) as the second argument, or `Factory::withManagementKey()`. The SDK sends credentials in the `Authorization` header; load the Management Key from a secret store and never ship it to a browser. An HTTP error throws `ApiException` with `getStatusCode()`, the API error `getCode()`, `getMessage()` and the parsed `getBody()`. Network failures throw `TransporterException`, invalid JSON throws `UnserializableResponse`, and a Management Key operation without a key throws `MissingManagementKey` before any request. All extend `AddressZenException`. The SDK never retries: a timed-out verification may already be charged. See [error handling](./references/errors.md).

## Symfony

`addresszen/symfony-bundle` configures the client from `config/packages/addresszen.yaml` (`api_key`, `management_key`, `base_uri`, `http_client`, `headers`) and registers it as an autowirable service, so a controller type-hints `AddressZen\Client`. Symfony 6.4, 7 and 8. See the [Symfony page](https://docs.addresszen.com/docs/sdks/php/symfony).

## Laravel

`addresszen/laravel` reads `ADDRESSZEN_API_KEY` and `ADDRESSZEN_MANAGEMENT_KEY` from `.env`, binds the client in the container, so a controller type-hints `AddressZen\Client`, and adds an `AddressZen\Laravel\Facades\AddressZen` facade with every client method as a static call, such as `AddressZen::addressVerify(['query' => '1010 Cauthen Ln, Alamogordo, NM 88310'])`. Package discovery registers both; `php artisan vendor:publish --tag=addresszen-config` exposes the other options. Laravel 12 and 13. See the [Laravel page](https://docs.addresszen.com/docs/sdks/php/laravel).

## References

- [Setup](./references/setup.md): client options, HTTP client choice, timeouts and headers
- [Address verification](./references/address-verify.md): CASS matches, deliverability, no match and other countries
- [Autocomplete](./references/autocomplete.md): find and retrieve addresses, and place search
- [Email validation](./references/email-validation.md)
- [Phone validation](./references/phone-validation.md)
- [API keys](./references/keys.md): details, usage, logs and configs
- [Licensees](./references/licensees.md)
- [Responses](./references/responses.md): properties, array access, unions, native records and testing with a mock client
- [Error handling](./references/errors.md)
- [Operations](./references/endpoints/)
