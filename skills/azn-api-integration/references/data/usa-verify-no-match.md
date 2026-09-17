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
| `address_line_one` | yes | `""` | Empty if no match |  |
| `address_line_two` | yes | `""` | Empty if no match |  |
| `city` | yes | `""` | Empty if no match |  |
| `state` | yes | `""` | Empty if no match |  |
| `zip_code` | yes | `""` | Empty if no match |  |
| `country_iso_2` | yes | `""` | Empty if no match |  |

## Used By

- [AddressVerify](../endpoints/address-verify.md)
