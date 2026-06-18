# Place Description

Represents a possible place given an autocomplete query.

**Schema name:** `PlaceSuggestion`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `name` | yes | string | Place name | `London` |
| `descriptive_name` | yes | string | Longer form description of the place. | `London, United Kingdom` |
| `country_iso` | yes | string | 3 letter country code (ISO 3166-1) | `GBR` |
| `id` | yes | string | Unique identifier for place | `geonames_5324` |

## Used By

- [FindPlace](../endpoints/find-place.md)
