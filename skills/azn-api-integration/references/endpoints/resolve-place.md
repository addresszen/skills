# Resolve Place

**Endpoint:** `GET /places/{place}`

**Operation ID:** `ResolvePlace`

**Tags:** Place Search

Resolves a place autocompletion by its place ID.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `place` | path | yes | string | ID of place suggestion |
| `tags` | query | no | string | A comma separated list of tags to query over. |

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `code` | yes | integer |  |
| `message` | yes | string |  |
| `result` | yes |  | Represents a geographical place |

## Response Example

```json
{
  "result": {
    "id": "geonames_2643743",
    "dataset": "geonames",
    "name": "London",
    "descriptive_name": "London, Greater London, England",
    "language": "en",
    "longitude": -0.12574,
    "latitude": 51.50853,
    "country_iso": "GBR",
    "native": {
      "admin1_code": "ENG",
      "admin2_name": "Greater London",
      "geonameid": 2643743,
      "timezone": "Europe/London",
      "latitude": 51.50853,
      "language": "en",
      "dem": 25,
      "admin4_code": "",
      "admin1_geonameid": 6269131,
      "alternatenames": [
        "ILondon",
        "… 108 more items …"
      ],
      "cc2": [],
      "admin2_code": "GLA",
      "modification_date": "2022-03-09T00:00:00.000Z",
      "asciiname": "London",
      "id": "geonames_2643743",
      "feature_code": "PPLC",
      "country_iso": "GBR",
      "longitude": -0.12574,
      "elevation": null,
      "admin2_geonameid": 2648110,
      "admin1_name": "England",
      "population": "8961989",
      "country_code": "GB",
      "feature_class": "P",
      "name": "London",
      "admin3_code": "",
      "dataset": "geonames"
    }
  },
  "code": 2000,
  "message": "Success"
}
```

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 404 |  | Resource not found |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/resolve-place)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
