# GeoNames Place

The GeoNames record backing a place, as indexed.

Only administrative divisions (feature class `A`) and capital or seat-of-administration cities (feature codes `PPLC` and `PPLA*`) are indexed. Historical features (feature codes ending in `H`) are excluded.

**Schema name:** `GeonamesPlace`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Unique place ID |  |
| `dataset` | yes | `geonames` | Indicates the provenance of a place |  |
| `geonameid` | yes | integer | Unique identifier for GeoNames place |  |
| `name` | yes | string | Place name (UTF8) |  |
| `asciiname` | yes | string | Place name (ASCII). Empty string if not available |  |
| `alternatenames` | yes | array<string> | List of alternate names for the place |  |
| `language` | yes | string | Language represented by 2 letter ISO Code (639-1) |  |
| `latitude` | yes | string \| number | The latitude of the address or postcode (WGS84). |  |
| `longitude` | yes | string \| number | The longitude of the address or postcode (WGS84). |  |
| `feature_class` | yes | `A` \| `P` | GeoNames single letter feature class (http://www.geonames.org/export/codes.html). Only two are indexed |  |
| `feature_code` | yes | string | Full GeoNames feature code (http://www.geonames.org/export/codes.html) |  |
| `country_code` | yes | string | 2 letter ISO country code. Empty string if not available |  |
| `country_iso` | yes | string | 3 letter ISO country code derived from `country_code`. Empty string if the country cannot be resolved |  |
| `cc2` | yes | array<string> | List of other country codes mapping to this place |  |
| `admin1_name` | yes | string | Name of first administrative area. Empty string if not available |  |
| `admin1_geonameid` | yes | integer | GeoName ID for first administrative area |  |
| `admin1_code` | yes | string | Fipscode (subject to change to iso code) |  |
| `admin2_name` | yes | string | Name of second administrative area. Empty string if not available |  |
| `admin2_geonameid` | yes | integer | GeoName ID for second administrative area |  |
| `admin2_code` | yes | string | Code for the second administrative division |  |
| `admin3_code` | yes | string | Code for third level administrative division |  |
| `admin4_code` | yes | string | Code for fourth level administrative division |  |
| `population` | yes | string | Population at place. Represented as a string as it can be larger than a 32 bit integer |  |
| `elevation` | yes | integer | Elevation in metres. `null` if not available |  |
| `dem` | yes | integer | Digital elevation model (srtm3 or gtopo30), average elevation in metres |  |
| `timezone` | yes | string | The IANA timezone ID. Empty string if not available |  |
| `modification_date` | yes | string | Date the GeoNames record was last modified |  |

## Example

```json
{
  "id": "geonames_7296662",
  "dataset": "geonames",
  "geonameid": 7296662,
  "name": "Strumpshaw",
  "asciiname": "Strumpshaw",
  "alternatenames": [],
  "language": "en",
  "latitude": 52.60599,
  "longitude": 1.47572,
  "feature_class": "A",
  "feature_code": "ADM4",
  "country_code": "GB",
  "country_iso": "GBR",
  "cc2": [],
  "admin1_name": "England",
  "admin1_geonameid": 6269131,
  "admin1_code": "ENG",
  "admin2_name": "Norfolk",
  "admin2_geonameid": 2641455,
  "admin2_code": "I9",
  "admin3_code": "33UC",
  "admin4_code": "33UC056",
  "population": "0",
  "elevation": null,
  "dem": 25,
  "timezone": "Europe/London",
  "modification_date": "2010-05-25T00:00:00.000Z"
}
```
