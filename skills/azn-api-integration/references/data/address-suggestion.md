# Address Suggestion

Represents an address suggestion for any address in the world

**Schema name:** `AddressSuggestion`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address | `paf_8387729` |
| `suggestion` | yes | string | Address Suggestion to be displayed to the user | `10 Downing St, Montpelier, VT, 05602` |
| `urls` | yes | object |  |  |

## Used By

- [FindAddress](../endpoints/find-address.md)
