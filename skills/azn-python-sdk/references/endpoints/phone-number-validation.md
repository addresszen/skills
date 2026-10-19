# `phone_number_validation`

Phone Number Validation

Validates a phone number and returns its country, its national and international formats, and the network it was originally assigned to.

Requires an API Key licensed for phone validation.

Every query decrements your lookup balance, including a number that fails to parse and a number reported as invalid.

## Endpoint

`GET /phone_numbers`

See the [API reference](https://docs.addresszen.com/docs/api/phone-number-validation) for this endpoint.

## Import

```python
from addresszen import AddressZen
```

Call `phone_number_validation` on the `AddressZen` client. Path parameters are positional; query and body parameters are keyword-only.

## Path Parameters

_None._

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `query` | `str` | yes | Specifies the phone number to validate. Phone number must include a country code in an acceptable format. For instance, UK phone numbers should be prefixed with `+44`, `44` or `0044`. |
| `current_carrier` | `Literal['true'] \| str` | no | When set to `true`, the API retrieves and populates the current network of the phone number. This operation can be slow, depending on the network and local conditions. |
| `tags` | `str` | no | **Tags** A comma separated list of tags to query over. Useful if you want to specify the circumstances in which the request was made. If you specify multiple tags, the response comprises only requests that satisfy all of them. Searching `"foo,bar"` queries only requests tagged both `"foo"` and `"bar"`. |

## Response Type

```python
from addresszen.types import PhoneNumberValidationResult
```

## Errors

Unsuccessful HTTP responses raise `APIError` or a subclass, with the HTTP `status` and the API error `code` and `message`. Connection failures and timeouts raise `TransportError`. Unexpected responses raise `ProtocolError`. All derive from `ClientError`. See [error handling](https://docs.addresszen.com/docs/sdks/python/errors).

## Example

```python title="phone_number_validation.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    phone = client.phone_number_validation(query="+442079460000")
```
