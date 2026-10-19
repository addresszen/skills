---
name: azn-python-sdk
description: Use when integrating the AddressZen Python SDK (addresszen on PyPI). Covers US address verification, email and phone validation, API keys, licensees and error handling, plus a reference for every API operation including autocomplete by country.
license: SEE LICENSE IN LICENSE
metadata:
  author: addresszen
  homepage: https://addresszen.com
references:
  - setup.md
  - address-verify.md
  - email-validation.md
  - phone-validation.md
  - keys.md
  - licensees.md
  - errors.md
  - common.md
  - endpoints/
---

# AddressZen Python SDK

Call the AddressZen API from Python 3.12 or later with typed methods and Pydantic v2 response models. The client is synchronous and built on HTTPX.

```bash
pip install addresszen
```

```python
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    result = client.address_verify(query="1010 Cauthen Ln, Alamogordo, NM 88310")
    print(result.address_line_one, result.city, result.state, result.zip_code)
```

Create one client and reuse it; close it with `with` or `close()`. Path parameters are positional, everything else is keyword-only. Methods return the API's `result` as models: read attributes, or call `model_dump()` for a dictionary.

## Scope

Every API operation has a method, including autocomplete (`find_address`, `retrieve_address`, with `context` set to a three-letter ISO 3166-1 code such as `USA`, `CAN` or `JPN`), place search, configs, licensees, email and phone validation. The guides cover the common tasks; `references/endpoints/` has one page per method.

## Authentication and errors

Pass the API key to the client. Key management (except `key_availability`), licensee and config methods also need a Management Key (`uk_...`) as the `user_token` keyword argument. The SDK sends it in the `Authorization` header; load it from a secret store and never ship it to a browser. Unsuccessful responses raise `APIError` subclasses (`AuthenticationError`, `PaymentRequiredError`, `NotFoundError`, `RateLimitError`, `ServerError`) with `status`, `code` and `message`. Network failures raise `TransportError`; invalid responses raise `ProtocolError`. All derive from `ClientError`. The SDK never retries: a timed-out lookup may already be charged. See [error handling](./references/errors.md).

## References

- [Setup](./references/setup.md)
- [Address verification](./references/address-verify.md)
- [Email validation](./references/email-validation.md)
- [Phone validation](./references/phone-validation.md)
- [API keys](./references/keys.md)
- [Licensees](./references/licensees.md)
- [Error handling](./references/errors.md)
- [Responses, arguments and testing](./references/common.md)
- [Operations](./references/endpoints/)
