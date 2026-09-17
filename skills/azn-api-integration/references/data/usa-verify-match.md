# Address Match

**Schema name:** `UsaVerifyMatch`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `query` | yes | string | Submitted query |  |
| `query_city` | yes | string | Submitted city |  |
| `query_state` | yes | string | Submitted state |  |
| `query_zip_code` | yes | string | Submitted zip_code |  |
| `match` | yes | [UsaCassVerifiedAddress](./usa-cass-verified-address.md) | Nearest matching address |  |
| `count` | yes | number | The number of addresses we matched to the input. We return the closest match by default. |  |
| `fit` | yes | number | A score represented as number between 1 and 0. Fit compares the address elements present in your query against the matching address elements. It does not incorporate elements you have not presented in the score. A partial address (e.g. 12 Pye Green Road) will have a fit of 1 even though it is missing post town and postcode. Its confidence score will be less than 1 however because it is missing some crucial elements. |  |
| `confidence` | yes | number | A confidence score represented as number between 1 and 0. 1 indicates a full match. 0 indicates no complete matching elements. |  |
| `match_information` | yes | string | Additional information about the match. | `Single Response - The delivery address was found in the National Database and no further information was required.` |
| `address_line_one` | yes | string | Primary delivery address | `123 Main St` |
| `address_line_two` | yes | string | Secondary address information | `` |
| `city` | yes | string | City name | `Springfield` |
| `state` | yes | string | State name | `CO` |
| `zip_code` | yes | string | Zip code | `81073-1119` |
| `country_iso_2` | yes | string | 2 letter ISO country code | `US` |

## Used By

- [AddressVerify](../endpoints/address-verify.md)
