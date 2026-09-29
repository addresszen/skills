# azn find & resolve

Address autocomplete: two-step by design. Useful when you need to pin a specific address from partial info before using it downstream.

## `azn find [query]`

`GET /autocomplete/addresses`.

| Flag | Description |
|---|---|
| `--country <iso3>` | Filter by ISO-3 (for example USA, GBR) |

**TTY (human):** prompts for input if no query, shows a `select` picker, auto-resolves the chosen suggestion, and prints the full address.

**Non-TTY (agent):** the query is required. Emits suggestions as JSON:

```json
{
  "count": 2,
  "suggestions": [
    { "id": "ABC123", "suggestion": "1600 Amphitheatre Pkwy, Mountain View, CA" },
    { "id": "DEF456", "suggestion": "1601 Amphitheatre Pkwy, Mountain View, CA" }
  ]
}
```

## `azn resolve <id>`

`GET /autocomplete/addresses/{id}/{country}`.

| Flag | Description |
|---|---|
| `--country <iso3>` | Resolution dataset: `usa` (default) or `gbr` |

Returns the resolved address object.

## Agent pattern

```bash
# Pick the top hit and resolve
ID=$(azn find "1600 amphitheatre" | jq -r '.suggestions[0].id')
azn resolve "$ID"
```
