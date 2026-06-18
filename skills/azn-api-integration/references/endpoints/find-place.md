# Find Place

**Endpoint:** `GET /places`

**Operation ID:** `FindPlace`

**Tags:** Place Search

Query for geographical places across countries. Each query will return a list of place suggestions, which consists of a place name, descriptive name and id.

This API returns geographical information such as countries, capitals, administrative areas and more. It is ideal for correctly identifying a place along with any other details like geolocation.

## Implementing Place Autocomplete

Extracting the full information of a place is a 2 step process:

1. Retrieve place suggestions via /places
2. Retrieve the entire place with the ID provided in the suggestion

## Suggestion Format

Each place suggestion contains a descriptive name which you can provide to users to uniquely identify a place.

## Rate Limiting and Cost

The rate limit for the Autocomplete API is 3000 requests per 5 minutes. HTTP Headers inform about the current rate limit.

Autocomplete API usage does not impact your balance, but resolving a suggestion to a full address requires a paid request. Autocomplete requests without subsequent paid requests may result in rate limitation or suspension.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `query` | query | no | string | Specifies the place you wish to query. Query can be shortened to `q=` |
| `country_iso` | query | no | string | Filter by country ISO code. Uses 3 letter country code (ISO 3166-1) standard. |
| `bias_country_iso` | query | no | string | Bias by country ISO code. Uses 3 letter country code (ISO 3166-1) standard. |
| `bias_lonlat` | query | no | string | Bias search to a geospatial circle determined by an origin and radius in meters. Max radius is `50000`. |
| `bias_ip` | query | no | `true` | Biases search based on approximate geolocation of IP address. |

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `code` | yes | integer |  |
| `message` | yes | string |  |
| `result` | yes | object |  |

## Response Example

```json
{
  "result": {
    "hits": [
      {
        "id": "geonames_2643743",
        "name": "London",
        "descriptive_name": "London, Greater London, England",
        "country_iso": "GBR"
      },
      "… 2 more items …"
    ]
  },
  "code": 2000,
  "message": "Success"
}
```

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 400 |  | Bad Request |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/find-place)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
