# No Address Match

**Schema name:** `UsaVerifyNoMatch`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `query` | yes | string | Originally submitted query |  |
| `query_city` | yes | string | Originally submitted city |  |
| `query_state` | yes | string | Originally submitted state |  |
| `query_zip_code` | yes | string | Originally submitted zip_code |  |
| `match` | yes | `null` | Nearest matching address |  |
| `count` | yes | `0` |  |  |
| `fit` | yes | `0` |  |  |
| `confidence` | yes | `0` |  |  |
| `match_information` | yes | string | Why the address could not be verified, for people to read. For example `Address not found`, `House number not valid for this street`, `Invalid city, state or ZIP code` or `Address could not be parsed`. | `Address not found` |
| `address_line_one` | yes | `""` | Empty if no match |  |
| `address_line_two` | yes | `""` | Empty if no match |  |
| `city` | yes | `""` | Empty if no match |  |
| `state` | yes | `""` | Empty if no match |  |
| `zip_code` | yes | `""` | Empty if no match |  |
| `country_iso_2` | yes | `""` | Empty if no match |  |

## Used By

- [AddressVerify](../endpoints/address-verify.md)
