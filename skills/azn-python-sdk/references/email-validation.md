# Email validation

`email_validation` checks whether an email address can receive mail, wherever its domain is hosted. It also flags disposable, free, role and catch-all addresses.

```python title="email_validation.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    email = client.email_validation(query="person@example.com")
    print(email.result, email.deliverable, email.suggestions)
```

Your key needs email validation enabled.

## Result

| `result` | Meaning | `deliverable` |
| --- | --- | --- |
| `deliverable` | The mailbox accepts mail | `True` |
| `not_deliverable` | Mail will bounce, or the domain cannot receive mail | `False` |
| `unknown` | The API could not check the address | `None` |

A checked address also sets four flags to `True` or `False`:

- `disposable`: a throwaway domain, such as temp-mail.org
- `free`: a free provider, such as Gmail or Outlook
- `role`: a shared mailbox, such as admin@ or support@
- `catchall`: the domain accepts mail for any name, so `deliverable` proves less

An `unknown` result sets every flag to `None`.

## Suggested corrections

Only when the domain does not resolve or publishes no MX records. Then `suggestions` can hold corrected addresses. The API does not validate them, so check one before you use it.

## Cost

One lookup for a checked address. An `unknown` result is free, and so is a domain that does not resolve or has no MX records. The API rejects an address over 320 characters with an `APIError`.

See [`email_validation`](https://docs.addresszen.com/docs/sdks/python/endpoints/email-validation) for the parameters.
