# `update_config`

Update

Replaces a configuration's payload and returns the updated configuration. The name is fixed at creation.

## Endpoint

`POST /keys/{key}/configs/{config}`

See the [API reference](https://docs.addresszen.com/docs/api/update-config) for this endpoint.

This operation needs a Management Key. Pass it as the required `user_token` keyword argument; the client sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/python/setup).

## Import

```python
from addresszen import AddressZen
```

Call `update_config` on the `AddressZen` client. Path parameters are positional; query and body parameters are keyword-only.

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `str` | yes | **API Key** The API Key. Begins `ak_`. |
| `config` | `str` | yes | **Configuration Name** User-provided configuration object name. |

## Query Parameters

_None._

## Request Body

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `payload` | `str` | no | A serialized payload of up to `65536` characters |

## Response Type

```python
from addresszen.types import UpdateConfigResult
```

## Errors

Unsuccessful HTTP responses raise `APIError` or a subclass, with the HTTP `status` and the API error `code` and `message`. Connection failures and timeouts raise `TransportError`. Unexpected responses raise `ProtocolError`. All derive from `ClientError`. See [error handling](https://docs.addresszen.com/docs/sdks/python/errors).

## Example

```python title="update_config.py"
import json

from addresszen import AddressZen

with AddressZen("ak_test") as client:
    config = client.update_config(
        "ak_test", "checkout", user_token="uk_example", payload=json.dumps({"enabled": False})
    )
```
