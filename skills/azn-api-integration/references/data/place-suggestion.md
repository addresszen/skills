# Place Suggestion

Represents a possible place given an autocomplete query.

**Schema name:** `PlaceSuggestion`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Unique identifier for place | `geonames_7296662` |
| `name` | yes | string | Place name | `Strumpshaw` |
| `descriptive_name` | yes | string | Longer form description of the place. | `Strumpshaw, Norfolk, England` |
| `country_iso` | yes | string | 3 letter country code (ISO 3166-1) | `GBR` |

## Example

```json
{
  "id": "geonames_7296662",
  "name": "Strumpshaw",
  "descriptive_name": "Strumpshaw, Norfolk, England",
  "country_iso": "GBR"
}
```

## Used By

- [FindPlace](../endpoints/find-place.md)
