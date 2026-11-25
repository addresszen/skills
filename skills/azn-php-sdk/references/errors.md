# Error handling

An HTTP error throws `ApiException`. A failed connection throws `TransporterException`. Every exception the SDK throws implements `AddressZenException`.

## ApiException

`ApiException` carries the HTTP status, the API error code and the decoded body.

| Member | Contents |
| --- | --- |
| `getStatusCode()` | HTTP status, such as `401`. Also the `status` property |
| `getCode()` | API error code, such as `4010`. `0` when the body carries none |
| `getMessage()` | API error message, or the HTTP reason phrase |
| `getBody()` | Decoded JSON body as an array, or the raw text when it is not JSON |
| `getResponse()` | The PSR-7 response |

```php title="errors.php"
use AddressZen\AddressZen;
use AddressZen\Exceptions\ApiException;

$client = AddressZen::client('ak_test');

try {
    $result = $client->addressVerify(['query' => '1010 Cauthen Ln, Alamogordo, NM 88310'])->result;
} catch (ApiException $e) {
    if ($e->getStatusCode() === 401) {
        echo 'Check the key, and that address verification is enabled on it', PHP_EOL;
    } else {
        echo $e->getStatusCode(), ' ', $e->getCode(), ' ', $e->getMessage(), PHP_EOL;
    }
}
```

The message and body can echo the address you sent, so treat them as personal data when you log them. The [error codes guide](https://docs.addresszen.com/docs/guides/error-codes) lists each code and how to fix it.

## Other exceptions

| Exception | When |
| --- | --- |
| `TransporterException` | The PSR-18 client could not complete the request: DNS, connection, TLS or timeout failure. The client's own exception is `getPrevious()` |
| `UnserializableResponse` | A success response whose body is not a JSON object |
| `MissingManagementKey` | A key, licensee or configuration operation on a client with no Management Key. Thrown before any request is sent |
| `MissingResponseField` | A success response without a field the SDK requires. `getMessage()` names the field and `$type` the class. Report it to support: the API and the SDK disagree |

`AddressZen::client('')` and a factory with no API key throw `InvalidArgumentException`.

## Catch every SDK error

Catch `AddressZenException`. It is an interface every SDK exception implements, so one catch covers API errors, transport failures and configuration mistakes.

```php title="catch-all.php"
use AddressZen\Exceptions\AddressZenException;

try {
    $response = $client->findAddress(['query' => '1010 Cauthen Ln']);
} catch (AddressZenException $e) {
    error_log($e->getMessage());
}
```

## Retries

The SDK never retries. A timed-out request may still have been processed and charged, so retries are left to you. Retry an `ApiException` with status `429` or `5xx`, and a `TransporterException`, with a bounded number of attempts.

## Tell a timeout from a connection failure

Both throw `TransporterException`. The cause is the HTTP client's own exception in `getPrevious()`. With Guzzle, a timeout and a refused connection both arrive as `GuzzleHttp\Exception\ConnectException`, with the detail in its message.
