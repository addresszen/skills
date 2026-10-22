# `key_availability`

Availability

Returns public information on an API Key: whether it can be used right now (`available`), the search contexts the key is licensed for (`contexts`) and the context that best matches the caller's IP address (`context`).

The endpoint accepts API Keys (beginning `ak_`) and sub-licensed keys (beginning `sl_`), and needs no Management Key.

A key that exists but cannot be used, because it has no lookups left or has breached a limit, returns `200` with `"available": false`. An unknown or malformed key returns an error.

Supply a valid Management Key and the endpoint returns the key's private details instead, as `GET /keys/{key}/details` does. A Management Key that does not own the key is rejected.

## Endpoint

`GET /keys/{key}`

See the [API reference](https://docs.addresszen.com/docs/api/key-availability) for this endpoint.

## Import

```python
from addresszen import AddressZen
```

Call `key_availability` on the `AddressZen` client. Path parameters are positional; query and body parameters are keyword-only.

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `str` | yes | **API Key** The API Key. Begins `ak_`. |

## Query Parameters

_None._

## Response Type

```python
from addresszen.types import KeyAvailabilityResult
```

## Errors

Unsuccessful HTTP responses raise `APIError` or a subclass, with the HTTP `status` and the API error `code` and `message`. Connection failures and timeouts raise `TransportError`. Unexpected responses raise `ProtocolError`. All derive from `ClientError`. See [error handling](https://docs.addresszen.com/docs/sdks/python/errors).

## Example

```python title="key_availability.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    availability = client.key_availability("ak_test")
```
