# Austria BEV Address

An address from the Adressregister, Austria's official address register published by the Bundesamt für Eich- und Vermessungswesen (BEV) under Open Government Data Austria.

One record per building at an address: the address (`adrcd`) is joined to its building (`subcd`, `objektnummer`), municipality, locality, street and census district lookups.

Field names follow the German source. House numbers are decomposed into up to four number/letter/connector parts (`hausnrzahl1`-`hausnrzahl4`) and supplied pre-combined (`hnr_adr_zusammen`, `hnr_geb_zusammen`, `address`). Values sourced from list columns (`kgnr`, `objfunktkennziffer`) are returned comma-separated.

**Schema name:** `BevAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | `bev` |  |  |
| `country` | yes | `Austria` | Full country names (ISO 3166) |  |
| `country_iso` | yes | `AUT` | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | `AT` | 2 letter country code (ISO 3166-1) |  |
| `language` | yes | `de` | Language represented by 2 letter ISO Code (639-1) |  |
| `address` | yes | string | Complete house number: `hnr_adr_zusammen` combined with `hnr_geb_zusammen`. |  |
| `line_1` | yes | string | First address line. The building or farmstead name (`hofname`) where one is present, otherwise the street line (street name plus `address`). |  |
| `line_2` | yes | string | Second address line. The street line (street name plus `address`) where `line_1` holds the building name. |  |
| `latitude` | yes | string \| number | The latitude of the address or postcode (WGS84). |  |
| `longitude` | yes | string \| number | The longitude of the address or postcode (WGS84). |  |
| `adrcd` | yes | string | Unique identifier of the address |  |
| `kgnr` | yes | string | Comma-separated cadastral numbers (Katastralgemeindenummer) of the land parcels associated with the address |  |
| `gkz` | yes | string | Municipality unique identifier |  |
| `okz` | yes | string | Locality unique identifier |  |
| `plz` | yes | string | Postal code |  |
| `skz` | yes | string | Street unique identifier |  |
| `zaehlsprengel` | yes | string | Census district unique identifier |  |
| `hausnrtext` | yes | string | Text before house number |  |
| `hausnrzahl1` | yes | integer | House number part 1 |  |
| `hausnrbuchstabe1` | yes | string | House letter part 1 |  |
| `hausnrverbindung1` | yes | string | House number connector 1. `-` indicates `hausnrzahl1` to `hausnrzahl2` is a range. |  |
| `hausnrzahl2` | yes | string \| integer |  |  |
| `hausnrbuchstabe2` | yes | string | House letter part 2 |  |
| `hausnrbereich` | yes | string | House number range scheme (even, odd, all or not specified), as German source text |  |
| `hnr_adr_zusammen` | yes | string | Complete house number of the address (combination of house number parts and letters) |  |
| `gnradresse` | yes | integer | Parcel number used as an address when no house number is present. `0` where unused. |  |
| `hofname` | yes | string | Name of building or building complex (e.g. farmstead), title cased |  |
| `rw` | yes | string | Easting / X coordinate in the coordinate reference system given by `epsg` |  |
| `hw` | yes | string | Northing / Y coordinate in the coordinate reference system given by `epsg` |  |
| `epsg` | yes | integer | Coordinate reference system identifier for `rw` and `hw` |  |
| `quelladresse` | yes | string | Coordinate accuracy level (building level, parcel level, etc.) |  |
| `bestimmungsart` | yes | string | Coordinate determination method (DKM, surveying office, municipality, etc.) |  |
| `subcd` | yes | string | Subcode to distinguish multiple buildings at the same address |  |
| `objektnummer` | yes | string | Object number of the building |  |
| `objfunktkennziffer` | yes | string | Comma-separated building function codes for the building (e.g. `01` pharmacy, `04` fire department, `08` school, `99` no function assigned) |  |
| `hauptadresse` | yes | integer | `1` where this is the primary address for the associated building, `0` otherwise |  |
| `hausnrverbindung2` | yes | string | House number connector 2 |  |
| `hausnrzahl3` | yes | string \| integer |  |  |
| `hausnrbuchstabe3` | yes | string | House letter part 3 |  |
| `hausnrverbindung3` | yes | string | House number connector 3 |  |
| `hausnrzahl4` | yes | string \| integer |  |  |
| `hausnrbuchstabe4` | yes | string | House letter part 4 |  |
| `hausnrgebaeudebez` | yes | string | Building description |  |
| `hnr_geb_zusammen` | yes | string | Complete building designation (combination of house number and building designation) |  |
| `eigenschaft` | yes | string | Code indicating the primary use or function of the building (e.g. `01` one apartment, `02` two or more apartments, `05` office building) |  |
| `gemeindename` | yes | string | Name of the municipality |  |
| `ortsname` | yes | string | Name of the locality |  |
| `strassenname` | yes | string | Name of the street |  |
| `strassennamenzusatz` | yes | string | Street type (e.g. "Allee", "Strasse") |  |
| `szusadrbest` | yes | integer | Indicates whether the street type is included in the street name |  |
| `zustellort` | yes | string | Postal town name |  |
| `zustellort_id` | yes | string | Postal town identifier |  |
| `zaehlsprengelname` | yes | string | Name of the census district |  |

## Example

```json
{
  "id": "bev_5000090|001",
  "dataset": "bev",
  "country": "Austria",
  "country_iso": "AUT",
  "country_iso_2": "AT",
  "language": "de",
  "address": "41",
  "line_1": "Poltenweg 41",
  "line_2": "",
  "latitude": 47.240128940538256,
  "longitude": 11.401418155046553,
  "adrcd": "5000090",
  "kgnr": "81134",
  "gkz": "70101",
  "okz": "16406",
  "plz": "6080",
  "skz": "001319",
  "zaehlsprengel": "70101700",
  "hausnrtext": "",
  "hausnrzahl1": 41,
  "hausnrbuchstabe1": "",
  "hausnrverbindung1": "",
  "hausnrzahl2": "",
  "hausnrbuchstabe2": "",
  "hausnrbereich": "keine Angabe",
  "hnr_adr_zusammen": "41",
  "gnradresse": 0,
  "hofname": "",
  "rw": "80893.30",
  "hw": "234024.51",
  "epsg": 31254,
  "quelladresse": "G",
  "bestimmungsart": "Z",
  "subcd": "001",
  "objektnummer": "1330150",
  "objfunktkennziffer": "99",
  "hauptadresse": 1,
  "hausnrverbindung2": "",
  "hausnrzahl3": "",
  "hausnrbuchstabe3": "",
  "hausnrverbindung3": "",
  "hausnrzahl4": "",
  "hausnrbuchstabe4": "",
  "hausnrgebaeudebez": "",
  "hnr_geb_zusammen": "",
  "eigenschaft": "02",
  "gemeindename": "Innsbruck",
  "ortsname": "Vill",
  "strassenname": "Poltenweg",
  "strassennamenzusatz": "",
  "szusadrbest": 0,
  "zustellort": "Innsbruck",
  "zustellort_id": "15215",
  "zaehlsprengelname": "70101 700"
}
```
