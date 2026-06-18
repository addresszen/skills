# UK Address Suggestion

Represents a possible address given an autocomplete query.

UK Address Suggestions will return a UDPRN attribute if it references a deliverable endpoint found on Royal Mail's Postcode Address File dataset.

UK Address Suggestion will return a UMPRN if it references a multiple occupancy premise found on Royal Mail's Multiple Residence dataset.

**Schema name:** `UkAddressSuggestion`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address | `paf_8387729` |
| `suggestion` | yes | string | Address suggestion for a given query. | `Flat 6, 12 Roskear, Camborne, TR14` |
| `udprn` | yes | integer | UDPRN stands for ‘Unique Delivery Point Reference Number’. Royal Mail assigns a unique UDPRN code for each premise on PAF. Simple, unique reference number for each Delivery Point. Unlikely to be reused when an address expires. | `23747771` |
| `umprn` | no | number | Optionally returned field, representing the UMPRN of a Multiple Residence household | `51103417` |
| `urls` | yes | object |  |  |

## Used By

- [FindAddress](../endpoints/find-address.md)
