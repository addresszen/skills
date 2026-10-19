# Error handling

Every failure the SDK raises derives from `ClientError`. An unsuccessful HTTP response raises `APIError` or one of its subclasses. A network failure raises `TransportError`, and an unexpected response raises `ProtocolError`.

## Exceptions

| Exception | Raised when |
| --- | --- |
| `AuthenticationError` | HTTP `401` or `403`: the key or Management Key is wrong, or lacks permission |
| `PaymentRequiredError` | HTTP `402`: the balance is empty, or a lookup limit is reached |
| `NotFoundError` | HTTP `404`, such as an unknown address ID or licensee |
| `RateLimitError` | HTTP `429`, or `503` with API code `5030` |
| `ServerError` | Any other HTTP `5xx` |
| `APIError` | Any other unsuccessful HTTP response. Base class of the five above |
| `TransportError` | The request failed before a response arrived, such as a connection error or timeout |
| `ProtocolError` | The response was not a valid success envelope, or did not match the response schema. If only the result's fields failed, `result` holds the unvalidated result, otherwise `None` |

The SDK checks arguments against the API's schema before it sends a request. A wrong type or a missing settings key raises `TypeError`; a value out of range, too long or not matching its pattern raises `ValueError`. It does not check option values, so the API can add new ones.

## APIError attributes

| Attribute | Contents |
| --- | --- |
| `status` | HTTP status, such as `404` |
| `code` | API error code, such as `4040`. `0` when the body has none |
| `message` | API error message |
| `body` | Parsed JSON body as a dictionary |
| `retry_after` | Raw `Retry-After` header, or `None` |

```python title="errors.py"
from addresszen import AddressZen, APIError, AuthenticationError

with AddressZen("ak_test") as client:
    try:
        result = client.address_verify(query="1010 Cauthen Ln, Alamogordo, NM 88310")
    except AuthenticationError:
        print("Check the key, and that address verification is enabled on it")
    except APIError as error:
        print(error.status, error.code, error.message)
```

The exception's string holds the status, code and API message. The message and `body` can echo the address you sent, so treat them as personal data when you log them. The [error codes guide](https://docs.addresszen.com/docs/guides/error-codes) lists each code and how to fix it.

## Retries

The SDK does not retry. A timed-out request may still have been processed and charged, so the SDK leaves retries to you. Retry `RateLimitError`, `ServerError` and `TransportError` with a bounded number of attempts. `retry_after` is either a number of seconds or an HTTP date.
