# Phone validation

`phone_number_validation` checks a phone number from any country and returns it in national and international format, with its country and the network it was assigned to.

```python title="phone_validation.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    phone = client.phone_number_validation(query="+442071128019")
    if phone.valid:
        print(phone.international_format, phone.iso_country, phone.original_carrier)
```

The number must include its country code: `+1` for the US and Canada, `+44` for the UK, `+81` for Japan. Your key needs phone validation enabled.

## Result

A valid number returns `valid=True` with:

| Field | Contents |
| --- | --- |
| `national_format` | The number as dialed inside its country |
| `international_format` | The number with its country code |
| `iso_country`, `iso_country_2` | Three- and two-letter country codes, such as `USA` and `US` |
| `country` | Country name |
| `original_carrier` | The network the number was first assigned to, with `network_type` such as `mobile`, `landline` or `virtual` |

An invalid number returns `valid=False` with every other field `None`. It does not raise an error.

## Current network

Pass `current_carrier="true"` to fill `current_carrier` too. Numbers can move between networks, so `original_carrier` alone can be out of date. The extra check can be slow on some networks, so allow for it in your `timeout`.

## Cost

One lookup per request, including a number that is invalid or fails to parse.

See [`phone_number_validation`](https://docs.addresszen.com/docs/sdks/python/endpoints/phone-number-validation) for the parameters.
