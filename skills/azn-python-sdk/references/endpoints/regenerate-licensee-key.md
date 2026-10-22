# `regenerate_licensee_key`

Regenerate Key

Regenerates a licensee's key and returns the licensee with the new key. The previous key stops working immediately, so update any integration that uses it.

## Endpoint

`POST /keys/{key}/licensees/{licensee}/regenerate-key`

This operation needs a Management Key. Pass it as the required `user_token` keyword argument; the client sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/python/setup).

## Import

```python
from addresszen import AddressZen
```

Call `regenerate_licensee_key` on the `AddressZen` client. Path parameters are positional; query and body parameters are keyword-only.

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `str` | yes | **API Key** The API Key. Begins `ak_`. |
| `licensee` | `str` | yes | **Licensee Key** Uniquely identifies a licensee. |

## Query Parameters

_None._

## Response Type

```python
from addresszen.types import RegenerateLicenseeKeyResult
```

## Errors

Unsuccessful HTTP responses raise `APIError` or a subclass, with the HTTP `status` and the API error `code` and `message`. Connection failures and timeouts raise `TransportError`. Unexpected responses raise `ProtocolError`. All derive from `ClientError`. See [error handling](https://docs.addresszen.com/docs/sdks/python/errors).

## Example

```python title="regenerate_licensee_key.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    licensee = client.regenerate_licensee_key("ak_test", "sl_example", user_token="uk_example")
```
