# Switzerland and Liechtenstein Address

An address in the Swisstopo dataset, which covers Switzerland and Liechtenstein.

Fields are grouped by the upstream Swisstopo product they come from: the building address directory (`gebaeudeadressverzeichnis`), the street directory (`strassenverzeichnis`) and the official directory of towns and cities (`amtovz`).

Records marked as multilingual upstream are split into one address per street name, so `language` identifies the language of the street name.

**Schema name:** `SwtAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | `swt` |  |  |
| `country` | yes | `Switzerland` \| `Liechtenstein` | Full country names (ISO 3166) |  |
| `country_iso` | yes | `CHE` \| `LIE` | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | `CH` \| `LI` | 2 letter country code (ISO 3166-1) |  |
| `language` | yes | `de` \| `fr` \| `it` \| `rm` | Language represented by 2 letter ISO Code (639-1) |  |
| `canton` | yes | string | Canton name, in the language of the address (e.g. `"Basel-Stadt"`, `"Grigioni"`, `"Grischun"`). For Liechtenstein addresses this is the district. |  |
| `address` | yes | string | House number. Same value as `adr_number`. |  |
| `line_1` | yes | string | First address line. The building name where present, otherwise the street name and house number. |  |
| `line_2` | yes | string | Second address line. The street name and house number where `line_1` holds a building name. |  |
| `latitude` | yes | string \| number | The latitude of the address or postcode (WGS84). |  |
| `longitude` | yes | string \| number | The longitude of the address or postcode (WGS84). |  |
| `adr_egaid` | yes | integer | Federal building address identifier (Eidgenössischer Gebäudeadressidentifikator). |  |
| `str_esid` | yes | integer | Federal street identifier (Eidgenössischer Strassenidentifikator). Joins the address to the street directory. |  |
| `bdg_egid` | yes | integer | Federal building identifier (Eidgenössischer Gebäudeidentifikator). |  |
| `adr_edid` | yes | integer | Entrance identifier within the building. |  |
| `stn_label` | yes | string | Street name label. For French and Italian addresses the leading street type is lowercased (e.g. `"rue de la Gare"`). |  |
| `adr_number` | yes | string | House/address number (e.g. `"12"`, `"12A"`). |  |
| `bdg_category` | yes | string | Building category from the Federal Building and Dwelling Register (GWR), e.g. `"residential"`, `"non_residential"`. |  |
| `bdg_name` | yes | string | Building name. |  |
| `zip_label` | yes | string | Postal code and locality label (e.g. `"8001 Zürich"`). |  |
| `com_fosnr` | yes | integer | Federal municipality number assigned by the Federal Statistical Office (FSO/BFS). |  |
| `com_name` | yes | string | Municipality name. |  |
| `com_canton` | yes | string | Canton abbreviation (e.g. `"ZH"`, `"BE"`). |  |
| `adr_status` | yes | string | Address status from the GWR, e.g. `"real"`, `"projected"`. |  |
| `adr_official` | yes | boolean | Whether the address is an official address. |  |
| `adr_modified` | yes | string | Date the address record was last modified, formatted `DD.MM.YYYY`. |  |
| `adr_easting` | yes | string | Easting coordinate of the address in the Swiss coordinate system CH1903+/LV95 (EPSG:2056), in metres. |  |
| `adr_northing` | yes | string | Northing coordinate of the address in the Swiss coordinate system CH1903+/LV95 (EPSG:2056), in metres. |  |
| `str_type` | yes | string | Street type, e.g. `"Street"`, `"Area"`. |  |
| `str_status` | yes | string | Street status, e.g. `"real"`, `"projected"`. |  |
| `str_official` | yes | boolean | Whether the street name is official. |  |
| `str_modified` | yes | string | Date the street record was last modified, formatted `DD.MM.YYYY`. |  |
| `str_easting` | yes | string | Easting coordinate of the street centroid in the Swiss coordinate system CH1903+/LV95 (EPSG:2056), in metres. |  |
| `str_northing` | yes | string | Northing coordinate of the street centroid in the Swiss coordinate system CH1903+/LV95 (EPSG:2056), in metres. |  |
| `ortschaftsname` | yes | string | Locality name from the Official Directory of Towns and Cities (Amtliches Ortschaftenverzeichnis). |  |
| `plz4` | yes | string | 4-digit Swiss postal code, zero padded. |  |
| `zusatzziffer` | yes | string | 2-digit supplementary code distinguishing localities that share a 4-digit postal code. |  |
| `zip_id` | yes | integer | Unique identifier for the postal code record. |  |
| `gemeindename` | yes | string | Municipality name (Gemeindename) from the locality directory. |  |
| `bfs_nr` | yes | integer | Federal municipality number assigned by the Federal Statistical Office (BFS-Nr). |  |
| `kantonskürzel` | yes | string | Canton abbreviation from the locality directory (e.g. `"ZH"`, `"GE"`). |  |
| `sprache` | yes | string | Language of the address, mirroring `language`. |  |
| `validity` | yes | string | Date the postal code record became valid, formatted `YYYY-MM-DD`. |  |

## Example

```json
{
  "id": "swt_102410972|de",
  "dataset": "swt",
  "country": "Switzerland",
  "country_iso": "CHE",
  "country_iso_2": "CH",
  "language": "de",
  "canton": "Basel-Stadt",
  "address": "15.1",
  "line_1": "Brohegasse 15.1",
  "line_2": "",
  "latitude": 47.571268381201655,
  "longitude": 7.663107983521497,
  "adr_egaid": 102410972,
  "str_esid": 10025136,
  "bdg_egid": 243057973,
  "adr_edid": 0,
  "stn_label": "Brohegasse",
  "adr_number": "15.1",
  "bdg_category": "non_residential",
  "bdg_name": "",
  "zip_label": "4126 Bettingen",
  "com_fosnr": 2702,
  "com_name": "Bettingen",
  "com_canton": "BS",
  "adr_status": "real",
  "adr_official": false,
  "adr_modified": "23.07.2024",
  "adr_easting": "2616891.820",
  "adr_northing": "1268975.560",
  "str_type": "Street",
  "str_status": "real",
  "str_official": true,
  "str_modified": "23.07.2024",
  "str_easting": "2616922.086",
  "str_northing": "1268999.001",
  "ortschaftsname": "Bettingen",
  "plz4": "4126",
  "zusatzziffer": "00",
  "zip_id": 2531,
  "gemeindename": "Bettingen",
  "bfs_nr": 2702,
  "kantonskürzel": "BS",
  "sprache": "de",
  "validity": "2008-07-01"
}
```
