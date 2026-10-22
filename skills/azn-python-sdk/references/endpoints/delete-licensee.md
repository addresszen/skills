# `delete_licensee`

Cancel

Cancels a licensee. Its key stops working and it drops out of the licensee list. Contact us to reverse it.

## Endpoint

`DELETE /keys/{key}/licensees/{licensee}`

See the [API reference](https://docs.addresszen.com/docs/api/delete-licensee) for this endpoint.

This operation needs a Management Key. Pass it as the required `user_token` keyword argument; the client sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/python/setup).

## Import

```python
from addresszen import AddressZen
```

Call `delete_licensee` on the `AddressZen` client. Path parameters are positional; query and body parameters are keyword-only.

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `str` | yes | **API Key** The API Key. Begins `ak_`. |
| `licensee` | `str` | yes | **Licensee Key** Uniquely identifies a licensee. |

## Query Parameters

_None._

## Response Type

```python
from addresszen.types import DeleteLicenseeResult
```

## Errors

Unsuccessful HTTP responses raise `APIError` or a subclass, with the HTTP `status` and the API error `code` and `message`. Connection failures and timeouts raise `TransportError`. Unexpected responses raise `ProtocolError`. All derive from `ClientError`. See [error handling](https://docs.addresszen.com/docs/sdks/python/errors).

## Example

```python title="delete_licensee.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    result = client.delete_licensee("ak_test", "sl_example", user_token="uk_example")
```
