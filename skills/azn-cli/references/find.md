# azn find & resolve

Address autocomplete: two-step by design. Useful when you need to pin a specific address from partial info before using it downstream.

## `azn find <query>`

`GET /autocomplete/addresses`.

| Flag | Description |
|---|---|
| `--country <iso3>` | Limit suggestions to one country, by ISO-3 code (for example USA, GBR) |

**TTY (human):** prints a numbered list of suggestions with their ids.

**Non-TTY (agent):** emits suggestions as JSON:

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

`GET /autocomplete/addresses/{id}/usa`.

Returns the resolved address as `result`, in US format for addresses in any country. On a TTY, prints the address lines.

## Agent pattern

```bash
# Pick the top hit and resolve
ID=$(azn find "1600 amphitheatre" | jq -r '.suggestions[0].id')
azn resolve "$ID"
```
