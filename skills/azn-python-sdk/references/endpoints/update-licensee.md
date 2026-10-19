# `update_licensee`

Update

Updates a licensee's address, postcode, allowed URLs and daily limit. Returns the updated licensee. The name is fixed at creation.

## Endpoint

`POST /keys/{key}/licensees/{licensee}`

See the [API reference](https://docs.addresszen.com/docs/api/update-licensee) for this endpoint.

This operation needs a Management Key. Pass it as the required `user_token` keyword argument; the client sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/python/setup).

## Import

```python
from addresszen import AddressZen
```

Call `update_licensee` on the `AddressZen` client. Path parameters are positional; query and body parameters are keyword-only.

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `str` | yes | **API Key** The API Key to retrieve. Begins `ak_`. |
| `licensee` | `str` | yes | **Licensee Key** Uniquely identifies a licensee. |

## Query Parameters

_None._

## Request Body

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `name` | `str` | no | Licensee individual or organisation name |
| `address` | `str` | no | Licensee's first, second and third line address as well as post town concatenated by commas |
| `postcode` | `str` | no | Licensee's postcode |
| `whitelist` | `list[str]` | no | A list of allowed URLs. An empty list disables the check. A request is allowed when its `Origin` or `Referer` header matches an entry. Use one of these formats: - `https://www.example.com` allows one site. Scheme and host must match - `*.example.com` allows the domain and all its subdomains |
| `daily` | `requests.UpdateLicenseeDaily` | no |  |

Nested settings are typed dictionaries from `addresszen.requests`.

```python
class UpdateLicenseeDaily(TypedDict):
    limit: NotRequired[float | None]
```

## Response Type

```python
from addresszen.types import UpdateLicenseeResult
```

## Errors

Unsuccessful HTTP responses raise `APIError` or a subclass, with the HTTP `status` and the API error `code` and `message`. Connection failures and timeouts raise `TransportError`. Unexpected responses raise `ProtocolError`. All derive from `ClientError`. See [error handling](https://docs.addresszen.com/docs/sdks/python/errors).

## Example

```python title="update_licensee.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    licensee = client.update_licensee("ak_test", "sl_example", user_token="uk_example", name="Updated Company")
```
