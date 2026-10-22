# `create_licensee`

Create

Creates a licensee on a key and returns it with its generated `sl_` key. The key must be enabled for sub-licensing.

## Endpoint

`POST /keys/{key}/licensees`

See the [API reference](https://docs.addresszen.com/docs/api/create-licensee) for this endpoint.

This operation needs a Management Key. Pass it as the required `user_token` keyword argument; the client sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/python/setup).

## Import

```python
from addresszen import AddressZen
```

Call `create_licensee` on the `AddressZen` client. Path parameters are positional; query and body parameters are keyword-only.

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `str` | yes | **API Key** The API Key. Begins `ak_`. |

## Query Parameters

_None._

## Request Body

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `name` | `str` | no | Licensee individual or organisation name |
| `address` | `str` | no | Licensee's first, second and third line address as well as post town concatenated by commas |
| `postcode` | `str` | no | Licensee's postcode |
| `whitelist` | `list[str]` | no | A list of allowed URLs. An empty list disables the check. A request is allowed when its `Origin` or `Referer` header matches an entry. Use one of these formats: - `https://www.example.com` allows one site. Scheme and host must match - `*.example.com` allows the domain and all its subdomains |
| `daily` | `requests.CreateLicenseeDaily` | no |  |

Nested settings are typed dictionaries from `addresszen.requests`.

```python
class CreateLicenseeDaily(TypedDict):
    limit: NotRequired[float | None]
```

## Response Type

```python
from addresszen.types import CreateLicenseeResult
```

## Errors

Unsuccessful HTTP responses raise `APIError` or a subclass, with the HTTP `status` and the API error `code` and `message`. Connection failures and timeouts raise `TransportError`. Unexpected responses raise `ProtocolError`. All derive from `ClientError`. See [error handling](https://docs.addresszen.com/docs/sdks/python/errors).

## Example

```python title="create_licensee.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    licensee = client.create_licensee("ak_test", user_token="uk_example", name="Example Company")
```
