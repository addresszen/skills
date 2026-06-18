# GeoNames Place

Full GeoNames place specification

**Schema name:** `GeonamesPlace`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `geonameid` | yes | integer | Unique identifier for GeoNames place | `5353` |
| `name` | yes | string | Place name (UTF8) | `London` |
| `asciiname` | yes | string | Place Name (ASCII) | `London` |
| `alternatenames` | yes | array<oneOf> | List of alternate ASCII names |  |
| `latitude` | yes |  | The latitude of the postcode (WGS84/ETRS89). |  |
| `longitude` | yes |  | The longitude of the postcode (WGS84/ETRS89). |  |
| `feature_class` | yes | string | GeoNames single letter feature code |  |
| `feature_code` | yes | string | Full GeoNames feature code (http://www.geonames.org/export/codes.html) | `ADM1` |
| `country_code` | yes | string | 2 Letter ISO country code | `GB` |
| `cc2` | yes | array<oneOf> | List of other countries codes mapping to this place |  |
| `admin1_name` | yes | string | Name of first administrative area | `England` |
| `admin1_geonameid` | yes | integer | GeoName ID for first administrative area | `5353` |
| `admin1_code` | yes | string | Fipscode (subject to change to iso code) | `ENG` |
| `admin2_name` | yes | string | Name of second administrative area | `England` |
| `admin2_geonameid` | yes | integer | GeoName ID for second administrative area | `5353` |
| `admin2_code` | yes | string | Code for the second administrative division | `06` |
| `admin3_code` | yes | string | Code for third level administrative division | `08` |
| `admin4_code` | yes | string | Code for fourth level administrative division | `07` |
| `population` | yes | string | Population at place. Represented as string as it could be a larger than a 32bit integer | `7392832` |
| `elevation` | yes | integer | Elevation in meters |  |
| `dem` | yes | integer | Digital elevation model | `32` |
| `timezone` | yes | string | The IANA timezone ID | `Europe/London` |
| `modification_date` | yes | string | Datetime format | `2015-03-09` |
| `dataset` | no | string |  |  |
| `id` | no | string | Unique place ID | `geonames_5353` |
