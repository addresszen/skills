# `create_config`

Create

Creates a named configuration on a key and returns it.

## Endpoint

`POST /keys/{key}/configs`

See the [API reference](https://docs.addresszen.com/docs/api/create-config) for this endpoint.

This operation needs a Management Key. Pass it as the required `user_token` keyword argument; the client sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/python/setup).

## Import

```python
from addresszen import AddressZen
```

Call `create_config` on the `AddressZen` client. Path parameters are positional; query and body parameters are keyword-only.

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `str` | yes | **API Key** The API Key. Begins `ak_`. |

## Query Parameters

_None._

## Request Body

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `name` | `str` | yes | A unique name to identify the configuration payload |
| `payload` | `str` | yes | A serialized payload of up to `65536` characters |

## Response Type

```python
from addresszen.types import CreateConfigResult
```

## Errors

Unsuccessful HTTP responses raise `APIError` or a subclass, with the HTTP `status` and the API error `code` and `message`. Connection failures and timeouts raise `TransportError`. Unexpected responses raise `ProtocolError`. All derive from `ClientError`. See [error handling](https://docs.addresszen.com/docs/sdks/python/errors).

## Example

```python title="create_config.py"
import json

from addresszen import AddressZen

with AddressZen("ak_test") as client:
    config = client.create_config(
        "ak_test", user_token="uk_example", name="checkout", payload=json.dumps({"enabled": True})
    )
```
