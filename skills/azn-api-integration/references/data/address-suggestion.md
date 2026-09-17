# Address Suggestion

Represents an address suggestion for any address in the world

**Schema name:** `AddressSuggestion`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `suggestion` | yes | string | Address Suggestion to be displayed to the user |  |
| `urls` | yes | object | Always an empty object (`{}`). Retrieve the full address with `id` |  |

## Example

```json
{
  "id": "usps_V210079628|10||3797",
  "suggestion": "10 Downing St, Montpelier, VT, 05602",
  "urls": {}
}
```

## Used By

- [FindAddress](../endpoints/find-address.md)
