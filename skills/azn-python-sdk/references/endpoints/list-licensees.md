# `list_licensees`

List

Returns a key's licensees, oldest first, up to 100 per request. The list omits canceled licensees. The key must be enabled for sub-licensing.

## Endpoint

`GET /keys/{key}/licensees`

See the [API reference](https://docs.addresszen.com/docs/api/list-licensees) for this endpoint.

This operation needs a Management Key. Pass it as the required `user_token` keyword argument; the client sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/python/setup).

## Import

```python
from addresszen import AddressZen
```

Call `list_licensees` on the `AddressZen` client. Path parameters are positional; query and body parameters are keyword-only.

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `str` | yes | **API Key** The API Key to retrieve. Begins `ak_`. |

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `starting_after` | `int` | no | ID of the licensee after which to list results |
| `limit` | `int` | no | **Limit** Specifies the maximum number of records to retrieve. By default the limit is 10. Requesting a larger result set adds latency. |
| `query` | `str` | no | Filter results by licensee name. Can be shortened to `q=` |

## Response Type

```python
from addresszen.types import ListLicenseesResult
```

## Errors

Unsuccessful HTTP responses raise `APIError` or a subclass, with the HTTP `status` and the API error `code` and `message`. Connection failures and timeouts raise `TransportError`. Unexpected responses raise `ProtocolError`. All derive from `ClientError`. See [error handling](https://docs.addresszen.com/docs/sdks/python/errors).

## Example

```python title="list_licensees.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    licensees = client.list_licensees("ak_test", user_token="uk_example")
```
