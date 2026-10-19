# Address verification

`address_verify` checks a US address against the USPS Coding Accuracy Support System (CASS). It returns the address corrected and standardized, with its ZIP+4 code and USPS delivery data.

```python title="address_verify.py"
from addresszen import AddressZen, types

with AddressZen("ak_test") as client:
    result = client.address_verify(query="1010 Cauthen Ln, Alamogordo, NM 88310")
    if isinstance(result, types.UsaVerifyMatch) and result.fit > 0:
        print(result.zip_code, result.match.dpv, result.match.rdi)
    else:
        print("No match")
```

Your key needs address verification enabled, or the call raises `AuthenticationError` with status `401`.

## Match result

The standardized address is at the top level, in `address_line_one`, `address_line_two`, `city`, `state` and `zip_code`. The full USPS record behind it is in `match`. The example above returns ZIP+4 `88310-5631`. The [API reference](https://docs.addresszen.com/docs/api/address-verify) lists every field, including county, congressional district, time zone and coordinates.

## Deliverability

Check `match.dpv`, the USPS Delivery Point Validation result. `"Y"` means USPS confirms the address as a delivery point. `"D"` means the apartment or suite number is missing, `"S"` means it is extra or incorrect and `"N"` means USPS does not confirm the address.

`confidence` measures something else, how well your input matched an address, and the two can disagree. `123 Main St, Springfield, CO 81073` scores a `confidence` of `1` but a `dpv` of `"N"`: the street exists, but USPS does not confirm the number.

## No match

Check `fit`. No match still returns successfully, with `fit` and `confidence` at `0` and the reason in `match_information`. The result can still carry a `match` record that echoes your input, so neither the model type nor `match` tells you on its own.

## Fit and confidence

Both run from 0 to 1. `fit` compares only the parts you sent, so `1010 Cauthen Ln` with a ZIP code and nothing else can score a `fit` of 1. `confidence` also counts the parts you left out, so the same input scores below 1.

## Address in parts

Put the street line in `query` and add `zip_code`, or `city` and `state`.

```python title="address_verify_parts.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    result = client.address_verify(query="1010 Cauthen Ln", zip_code="88310")
```

`zip_code` accepts `88310-5631`, `883105631` or `88310`. `state` takes the two-letter abbreviation.

## Cost

One lookup for a match. No match costs nothing. A verification still running after 9.5 seconds raises `RateLimitError` with status `429`.
