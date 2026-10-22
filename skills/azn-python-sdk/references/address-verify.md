# Address verification

`address_verify` checks a US address against the USPS Coding Accuracy Support System (CASS). It returns the address corrected and standardized, with its ZIP+4 code and USPS delivery data. To verify an address in another country, pass `context` with its ISO 3166-1 alpha-3 code, e.g. `context="GBR"`. Outside the United States `match` is a `types.Address`, the format `retrieve_address` returns; in the United States it is a `types.UsaCassVerifiedAddress`.

```python title="address_verify.py"
from addresszen import AddressZen, types

with AddressZen("ak_test") as client:
    result = client.address_verify(query="1010 Cauthen Ln, Alamogordo, NM 88310")
    if not isinstance(result, types.UsaVerifyMatch):
        print("No match:", result.match_information)
    elif isinstance(result.match, types.UsaCassVerifiedAddress):
        print(result.zip_code, result.match.dpv, result.match.rdi)
    else:
        print(result.zip_code, result.match.dataset)
```

Your key needs address verification enabled, or the call raises `AuthenticationError` with status `401`.

## Match result

The standardized address is at the top level, in `address_line_one`, `address_line_two`, `city`, `state` and `zip_code`. The full USPS record behind it is in `match`. The example above returns ZIP+4 `88310-5631`. The [API reference](https://docs.addresszen.com/docs/api/address-verify) lists every field, including county, congressional district, time zone and coordinates.

## Deliverability

Check `match.dpv`, the USPS Delivery Point Validation result. `"Y"` means USPS confirms the address as a delivery point. `"D"` means the apartment or suite number is missing, `"S"` means it is extra or incorrect and `"N"` means USPS does not confirm the address.

`confidence` measures something else, how well your input matched an address, and the two can disagree. `123 Main St, Springfield, CO 81073` scores a `confidence` of `1` but a `dpv` of `"N"`: the street exists, but USPS does not confirm the number.

## No match

An address that cannot be verified still returns successfully, as a `types.UsaVerifyNoMatch` with `match` set to `None`, a `count` of `0`, empty address fields and the reason in `match_information`, such as `Address not found` or `House number not valid for this street`. The wording may change, so do not parse it. CASS corrects what it can first: an address with the wrong city or state for its ZIP code still verifies, with the corrected values.

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

Every verification the CASS engine answers costs one lookup, matched or not. A query that cannot be parsed into an address costs nothing. A verification still running after 9.5 seconds raises `RateLimitError` with status `429`.
