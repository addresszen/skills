# Key

**Schema name:** `ApiKey`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `contexts` | yes | array<object> | A list of available contexts for a key |  |
| `context` | yes |  | Returns current context if it is in the list of available contexts for this key. |  |
| `available` | yes | boolean | Determines whether the key can be used by the requesting agent. | `true` |

## Used By

- [KeyAvailability](../endpoints/key-availability.md)
