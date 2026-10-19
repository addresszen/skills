# `email_validation`

Email Validation

Validates an email address and reports whether it is deliverable.

Requires an API Key licensed for email validation. A query over 320 characters is rejected.

A validated address decrements your lookup balance. An address the API cannot check returns `unknown` and costs no lookup. An address whose domain does not resolve, or publishes no MX records, returns `not_deliverable` and also costs no lookup. Only those two domain failures populate `suggestions`. Every other response returns an empty list.

## Endpoint

`GET /emails`

See the [API reference](https://docs.addresszen.com/docs/api/email-validation) for this endpoint.

## Import

```python
from addresszen import AddressZen
```

Call `email_validation` on the `AddressZen` client. Path parameters are positional; query and body parameters are keyword-only.

## Path Parameters

_None._

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `query` | `str` | yes | Specifies the email address to validate |
| `tags` | `str` | no | **Tags** A comma separated list of tags to query over. Useful if you want to specify the circumstances in which the request was made. If you specify multiple tags, the response comprises only requests that satisfy all of them. Searching `"foo,bar"` queries only requests tagged both `"foo"` and `"bar"`. |

## Response Type

```python
from addresszen.types import EmailValidationResult
```

## Errors

Unsuccessful HTTP responses raise `APIError` or a subclass, with the HTTP `status` and the API error `code` and `message`. Connection failures and timeouts raise `TransportError`. Unexpected responses raise `ProtocolError`. All derive from `ClientError`. See [error handling](https://docs.addresszen.com/docs/sdks/python/errors).

## Example

```python title="email_validation.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    email = client.email_validation(query="person@example.com")
```
