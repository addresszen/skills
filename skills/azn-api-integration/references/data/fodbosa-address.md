# Belgium FOD BOSA Address

A Belgian address from BeSt Address, the open address register published by FOD BOSA (Federal Public Service Policy and Support), covering Flanders, Wallonia and the Brussels Capital Region. Each address carries its street, house number and, where one exists, box number, the municipality (`municipality_id` is the NIS code), `postcode`, `region_code` and coordinates in both WGS84 (`epsg_4326_*`, mirrored as numeric `latitude` and `longitude`) and Belgian Lambert 72 (`epsg_31370_*`, in metres). Street, municipality and post town names come in Dutch, French and German. FOD BOSA publishes around 6.6 million current addresses and refreshes them weekly.

Conventions:

- One record per address point per language. The API emits an address once for each language in which it has a street name, or, for the few rows with no street name in any language, each language in which it has a municipality name. A bilingual Brussels address therefore exists as both a Dutch and a French record, sharing `address_id` but differing in `id`, `language` and `line_1`. `id` is `fodbosa_` followed by `address_id`, `street_id`, `municipality_id` and the language code, pipe separated (`fodbosa_1000000|3048|21007|fr`). The resolve endpoints read the trailing language code to find the record.
- Every property is always present. A value the register does not hold is an empty string `""`, never null. `latitude` and `longitude` are empty strings when the WGS84 pair does not parse.
- `line_1` is the street name and `house_number` joined by a space, with the box number appended after ` - ` and prefixed `bus` in Dutch and German or `boîte` in French: `rue Rodenbach 5 - boîte bt08`. Absent parts are dropped with their separator. There are no further address lines.
- `streetname_*` and `municipality_name_*` keep FOD BOSA's casing. `postname_*` is title cased because the register supplies it in upper case (`GENT` becomes `Gent`). The street name inside `line_1` is normalised further: double quotes and a trailing parenthetical are removed, and in French the leading street type is lower cased, so a `streetname_fr` of `Rue Rodenbach` appears in `line_1` as `rue Rodenbach`.
- Only `current` addresses are indexed. The register's `proposed`, `retired` and `rejected` records, around 7% of the file, are not served.
- FOD BOSA re-surveys address points between vintages, so a coordinate can move by a metre or so between weekly refreshes.

**Schema name:** `FodbosaAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | `fodbosa` | Dataset the address originates from. |  |
| `country` | yes | `Belgium` | Full country names (ISO 3166) |  |
| `country_iso` | yes | `BEL` | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | `BE` | 2 letter country code (ISO 3166-1) |  |
| `language` | yes | `de` \| `fr` \| `nl` | Language represented by 2 letter ISO Code (639-1) |  |
| `address` | yes | string | House number, duplicated from `house_number` for consistency with other datasets. It does not identify the address on its own: boxes on the same number differ only by `box_number`. |  |
| `line_1` | yes | string | First address line. Street name, house number and, where present, box number, rendered in the address language. |  |
| `latitude` | yes | string \| number | The latitude of the address or postcode (WGS84). |  |
| `longitude` | yes | string \| number | The longitude of the address or postcode (WGS84). |  |
| `epsg_31370_x` | yes | string | X coordinate of the address in the BD72 / Belgian Lambert 72 (EPSG:31370) coordinate system. |  |
| `epsg_31370_y` | yes | string | Y coordinate of the address in the BD72 / Belgian Lambert 72 (EPSG:31370) coordinate system. |  |
| `epsg_4326_lat` | yes | string | Latitude of the address in the WGS84 (EPSG:4326) coordinate system. String form of `latitude`. |  |
| `epsg_4326_lon` | yes | string | Longitude of the address in the WGS84 (EPSG:4326) coordinate system. String form of `longitude`. |  |
| `address_id` | yes | string | Address local identifier assigned by the data supplier. |  |
| `box_number` | yes | string | Box or apartment number. |  |
| `house_number` | yes | string | House number. |  |
| `municipality_id` | yes | string | Municipality local identifier (NIS code) assigned by the data supplier. |  |
| `municipality_name_de` | yes | string | Municipality name in German. |  |
| `municipality_name_fr` | yes | string | Municipality name in French. |  |
| `municipality_name_nl` | yes | string | Municipality name in Dutch. |  |
| `postcode` | yes | string | Postal code. 4 digits, first digit non-zero. |  |
| `postname_fr` | yes | string | Post town name in French. |  |
| `postname_nl` | yes | string | Post town name in Dutch. |  |
| `street_id` | yes | string | Street local identifier assigned by the data supplier. |  |
| `streetname_de` | yes | string | Street name in German. |  |
| `streetname_fr` | yes | string | Street name in French. |  |
| `streetname_nl` | yes | string | Street name in Dutch. |  |
| `region_code` | yes | string | ISO 3166-2 code of the region in which the address is located. One of `BE-BRU` (Brussels Capital Region), `BE-VLG` (Flanders) or `BE-WAL` (Wallonia). |  |
| `status` | yes | string | Address lifecycle status assigned by the data supplier. Only `current` addresses are indexed and served, so this is always `current`. The supplier's remaining codes (`proposed`, `reserved`, `retired`, `rejected`) are filtered out. |  |

## Example

```json
{
  "id": "fodbosa_1000000|3048|21007|fr",
  "dataset": "fodbosa",
  "country": "Belgium",
  "country_iso": "BEL",
  "country_iso_2": "BE",
  "language": "fr",
  "address": "5",
  "line_1": "rue Rodenbach 5 - boîte bt08",
  "latitude": 50.82029,
  "longitude": 4.34422,
  "epsg_31370_x": "148270.73200",
  "epsg_31370_y": "167761.35000",
  "epsg_4326_lat": "50.82029",
  "epsg_4326_lon": "4.34422",
  "address_id": "1000000",
  "box_number": "bt08",
  "house_number": "5",
  "municipality_id": "21007",
  "municipality_name_de": "",
  "municipality_name_fr": "Forest",
  "municipality_name_nl": "Vorst",
  "postcode": "1190",
  "postname_fr": "",
  "postname_nl": "",
  "street_id": "3048",
  "streetname_de": "",
  "streetname_fr": "Rue Rodenbach",
  "streetname_nl": "Rodenbachstraat",
  "region_code": "BE-BRU",
  "status": "current"
}
```
