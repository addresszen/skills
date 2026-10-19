# `retrieve_address`

Retrieve Address

Returns the full address for an autocomplete suggestion id.

This is the charged step of address autocomplete. A successful retrieval decrements your lookup balance. An id which resolves to no address returns `404`.

Every address comes back in one US-shaped format, whatever country or dataset it came from: up to two address lines and US field names such as `zip_code`, `state` and `city`.

## Endpoint

`GET /autocomplete/addresses/{address}/usa`

See the [API reference](https://docs.addresszen.com/docs/api/retrieve-address) for this endpoint.

## Import

```python
from addresszen import AddressZen
```

Call `retrieve_address` on the `AddressZen` client. Path parameters are positional; query and body parameters are keyword-only.

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `address` | `str` | yes | **ID of address suggestion** ID of address suggestion provided by the API to fully retrieve. |

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `licensee` | `str` | no | **Licensee Key** Uniquely identifies a licensee. |
| `filter` | `str` | no | **Restrict Result Fields** Comma separated whitelist of address elements to return. E.g. `filter=line_1,line_2,line_3` returns only the `line_1`, `line_2` and `line_3` address elements in your response. |
| `tags` | `str` | no | **Tags** A comma separated list of tags to query over. Useful if you want to specify the circumstances in which the request was made. If you specify multiple tags, the response comprises only requests that satisfy all of them. Searching `"foo,bar"` queries only requests tagged both `"foo"` and `"bar"`. |

## Response Type

```python
from addresszen.types import RetrieveAddressResult
```

With `filter`, returns dictionaries of the requested fields instead of models.

## Errors

Unsuccessful HTTP responses raise `APIError` or a subclass, with the HTTP `status` and the API error `code` and `message`. Connection failures and timeouts raise `TransportError`. Unexpected responses raise `ProtocolError`. All derive from `ClientError`. See [error handling](https://docs.addresszen.com/docs/sdks/python/errors).

## Example

```python title="retrieve_address.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    address = client.retrieve_address("usps_Z108703633|123||1119")
```
