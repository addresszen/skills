# Setup

Install `addresszen/sdk`, then create a client with your API key. The SDK needs PHP 8.2 or later and a PSR-18 HTTP client.

## Install

```bash
composer require addresszen/sdk
```

The SDK sends requests through whichever PSR-18 client and PSR-17 factories your project already has, found by `php-http/discovery`. If Composer reports that no client is installed, add one:

```bash
composer require guzzlehttp/guzzle
```

Symfony HttpClient, with `symfony/http-client` and `nyholm/psr7`, works the same way.

## Create a client

Pass your API key to `AddressZen::client()`.

```php title="client.php"
use AddressZen\AddressZen;

$client = AddressZen::client('ak_test');
```

## Management Key

Key details, usage and logs, licensees and configurations need your Management Key, which begins `uk_`. Pass it as the second argument. It grants control of your account, so keep it on your server and out of version control.

```php title="management.php"
$client = AddressZen::client('ak_test', getenv('ADDRESSZEN_MANAGEMENT_KEY'));

$details = $client->keyDetails('ak_test');
echo $details->result->lookupsRemaining, PHP_EOL;
```

A client without a Management Key throws `MissingManagementKey` before sending a request that needs one.

## Client options

For anything beyond a key, build the client with the factory.

```php title="factory.php"
use AddressZen\AddressZen;
use GuzzleHttp\Client as Guzzle;

$client = AddressZen::factory()
    ->withApiKey('ak_test')
    ->withManagementKey(getenv('ADDRESSZEN_MANAGEMENT_KEY'))
    ->withHttpClient(new Guzzle(['timeout' => 5]))
    ->withHttpHeader('User-Agent', 'my-app/1.0')
    ->make();
```

| Method | Purpose |
| --- | --- |
| `withApiKey(string)` | Required. The API key, or a licensee key beginning `sl_` |
| `withManagementKey(?string)` | The Management Key for account operations |
| `withBaseUri(string)` | Defaults to `https://api.addresszen.com/v1` |
| `withHttpClient(ClientInterface)` | A PSR-18 client. Found by discovery when not set |
| `withRequestFactory(RequestFactoryInterface)` | A PSR-17 request factory. Found by discovery when not set |
| `withStreamFactory(StreamFactoryInterface)` | A PSR-17 stream factory for JSON bodies. Found by discovery when not set |
| `withHttpHeader(string, string)` | A header sent with every request. A `User-Agent` you set is sent ahead of the SDK and PHP versions, for example `my-app/1.0 addresszen-php-sdk/0.1.0 php/8.4.1` |

## Set a request timeout

Set it on the HTTP client. The SDK has no timeout of its own, so the client's rules apply. A request that runs past the limit throws `TransporterException`, as described in [error handling](https://docs.addresszen.com/docs/sdks/php/errors).

```php title="timeout.php"
$client = AddressZen::factory()
    ->withApiKey('ak_test')
    ->withHttpClient(new GuzzleHttp\Client(['timeout' => 5, 'connect_timeout' => 2]))
    ->make();
```

## Credentials

The API key goes in the `Authorization` header of every address, place, email and phone request. The Management Key goes in the same header of every key, licensee and configuration request, and nowhere else. `keyAvailability()` and `retrieveConfig()` send no credentials.

To bill a single request to a licensee, pass its key as the `api_key` query parameter. It takes the place of the header for that request.

```php title="licensee.php"
$address = $client->retrieveAddress('usps_Z108703633|123||1119', ['api_key' => 'sl_licensee_key'])->result;
```

## User-Agent

Every request carries `User-Agent: addresszen-php-sdk/<version> php/<PHP version>`, such as `addresszen-php-sdk/0.1.0 php/8.4.1`. The header holds no credentials or address data.
