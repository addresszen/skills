# Canada NAR Address

A Canadian civic address from the National Address Register (NAR), published by Statistics Canada under the Statistics Canada Open Licence. Each address carries its civic number, street, municipality, province and postal code, a point coordinate, and its census subdivision, federal electoral district and economic region, in English and French. Statistics Canada publishes around 17.2 million addresses and refreshes them annually. 99.5% carry a full postal code and 95.7% carry a latitude and longitude.

Conventions:

- One record per address. `id` is `cannar_` followed by `addr_guid`, a pipe and the language code (`cannar_<addr_guid>|en`). The suffix selects the English or French form of the record, so preserve it verbatim when resolving an address.
- `language` is `en` or `fr`. The API derives it rather than reading it from the file: a French street type gives `fr`, and the types both languages share (`AV`, `PROM`, `ROUTE`, `RTE`) give `fr` in Quebec and New Brunswick and `en` elsewhere. An address appears under one language only. There is no paired English and French copy of the same record. The `csd_*`, `fed_*` and `er_*` name pairs are returned in both languages whatever the record's `language`.
- `line_1` is the number and street. A hyphen joins the apartment or suite number to the civic number (`306-1 Finch Bay`). A letter civic number suffix joins without a space (`5A`), a numeric one with a space (`1 1/2`). The street comes from the `mail_street_*` fields where `mail_street_name` is present and from the `official_street_*` fields otherwise. In English the street type follows the name (`Iron Horse Dr`), except `Route`, which precedes it. In French the type is lower cased and precedes the name (`rue d'Andermatt`).
- `line_2` carries the PO Box or Rural Route line from `bu_n_civic_add` (`PO Box 377`, `RR 4`). There is no third line. `address` is the number component of `line_1` on its own, apartment included (`5A`, `306-1`).
- The API title cases `mail_street_name`, `mail_street_type`, `mail_mun_name` and `official_street_type`. Every other text field is as Statistics Canada ships it, so `mail_prov_abvn`, `mail_postal_code`, `mail_street_dir` and `official_street_dir` stay upper case and the `csd_*`, `fed_*` and `er_*` names keep their supplied case.
- No field is null. A value absent upstream is an empty string `""`, including `latitude` and `longitude` where the location has no coordinate.
- `latitude` and `longitude` repeat `reppoint_latitude` and `reppoint_longitude`: the WGS84 representative point of the location record, shared by every address at the same `loc_guid`. `bg_x` and `bg_y` are the building's coordinates in EPSG:3347, returned as strings.

**Schema name:** `CannarAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | `cannar` |  |  |
| `country` | yes | `Canada` | Full country names (ISO 3166) |  |
| `country_iso` | yes | `CAN` | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | `CA` | 2 letter country code (ISO 3166-1) |  |
| `language` | yes | `en` \| `fr` | Language represented by 2 letter ISO Code (639-1) |  |
| `address` | yes | string | House number, prefixed with the apartment or suite number and a hyphen where one is present. E.g. `1425` or `10-123 1/2`. |  |
| `line_1` | yes | string | First address line. House number and street. |  |
| `line_2` | yes | string | Second address line. Carries the PO Box or Rural Route delivery information where present. |  |
| `latitude` | yes | string \| number | The latitude of the address or postcode (WGS84). |  |
| `longitude` | yes | string \| number | The longitude of the address or postcode (WGS84). |  |
| `loc_guid` | yes | string | Globally unique identifier for location. |  |
| `addr_guid` | yes | string | Globally unique identifier for address. |  |
| `apt_no_label` | yes | string | Apartment or suite number. |  |
| `civic_no` | yes | string | The building number assigned to the address. |  |
| `civic_no_suffix` | yes | string | A suffix attached to the civic number. E.g. `A` or `1/2`. |  |
| `official_street_name` | yes | string | Official street name. |  |
| `official_street_type` | yes | string | Official street designator. E.g. `St`, `Ave`. |  |
| `official_street_dir` | yes | string | Official street direction. E.g. `N`, `SE`. |  |
| `prov_code` | yes | string | Province code. E.g. `59` for British Columbia. |  |
| `csd_eng_name` | yes | string | Census subdivision English name. |  |
| `csd_fre_name` | yes | string | Census subdivision French name. |  |
| `csd_type_eng_code` | yes | string | English code indicating the type of Census Subdivision. |  |
| `csd_type_fre_code` | yes | string | French code indicating the type of Census Subdivision. |  |
| `mail_street_name` | yes | string | Name of the street used in the mailing address. |  |
| `mail_street_type` | yes | string | Designator of the street used in the mailing address. |  |
| `mail_street_dir` | yes | string | Direction of the street used in the mailing address. |  |
| `mail_mun_name` | yes | string | Municipality name used in the mailing address. |  |
| `mail_prov_abvn` | yes | string | Province abbreviation used in the mailing address. |  |
| `mail_postal_code` | yes | string | Postal code used in the mailing address. Returned as supplied by the provider, without a space between the forward sortation area and local delivery unit. |  |
| `bg_dls_lsd` | yes | string | Legal Subdivision number within the Dominion Land Survey system for the address location. |  |
| `bg_dls_qtr` | yes | string | Quarter section within a section of the Dominion Land Survey system for the address location. |  |
| `bg_dls_sctn` | yes | string | Section number within a township of the Dominion Land Survey system for the address location. |  |
| `bg_dls_twnshp` | yes | string | Township number within the Dominion Land Survey system for the address location. |  |
| `bg_dls_rng` | yes | string | Range number within a meridian of the Dominion Land Survey system for the address location. |  |
| `bg_dls_mrd` | yes | string | Meridian number within the Dominion Land Survey system for the address location. |  |
| `bg_x` | yes | string | X coordinate of the building in the EPSG:3347 projected grid, in metres, returned as a string. |  |
| `bg_y` | yes | string | Y coordinate of the building in the EPSG:3347 projected grid, in metres, returned as a string. |  |
| `bu_n_civic_add` | yes | string | Additional delivery information for the mailing address, such as a PO Box or Rural Route. Upper cased, with the first `BOX` token recased to `Box` (`PO Box 377`). |  |
| `bu_use` | yes | string | Building usage code. |  |
| `csd_code` | yes | string | Unique identifier code for a Census Subdivision (CSD). |  |
| `fed_code` | yes | string | Unique identifier code for a federal electoral district. |  |
| `fed_eng_name` | yes | string | Name of the federal electoral district in English. |  |
| `fed_fre_name` | yes | string | Name of the federal electoral district in French. |  |
| `er_code` | yes | string | Unique identifier code for an economic region. |  |
| `er_eng_name` | yes | string | Name of the economic region in English. |  |
| `er_fre_name` | yes | string | Name of the economic region in French. |  |
| `reppoint_latitude` | yes | string \| number | The latitude of the address or postcode (WGS84). |  |
| `reppoint_longitude` | yes | string \| number | The longitude of the address or postcode (WGS84). |  |

## Example

```json
{
  "id": "cannar_9b7d2a10-5c31-4a6e-8f21-7d0c5e4b3a12|en",
  "dataset": "cannar",
  "country": "Canada",
  "country_iso": "CAN",
  "country_iso_2": "CA",
  "language": "en",
  "address": "1425",
  "line_1": "1425 James St",
  "line_2": "PO Box 4001 STN A",
  "latitude": 48.4283,
  "longitude": -123.355,
  "loc_guid": "1c3f0f4e-0d4a-4f2c-9c9d-3f9a1b2c4d5e",
  "addr_guid": "9b7d2a10-5c31-4a6e-8f21-7d0c5e4b3a12",
  "apt_no_label": "",
  "civic_no": "1425",
  "civic_no_suffix": "",
  "official_street_name": "James",
  "official_street_type": "St",
  "official_street_dir": "",
  "prov_code": "59",
  "csd_eng_name": "Victoria",
  "csd_fre_name": "Victoria",
  "csd_type_eng_code": "CY",
  "csd_type_fre_code": "V",
  "mail_street_name": "James",
  "mail_street_type": "St",
  "mail_street_dir": "",
  "mail_mun_name": "Victoria",
  "mail_prov_abvn": "BC",
  "mail_postal_code": "V8X3X4",
  "bg_dls_lsd": "",
  "bg_dls_qtr": "",
  "bg_dls_sctn": "",
  "bg_dls_twnshp": "",
  "bg_dls_rng": "",
  "bg_dls_mrd": "",
  "bg_x": "3958372.7",
  "bg_y": "1908456.3",
  "bu_n_civic_add": "PO Box 4001 STN A",
  "bu_use": "1",
  "csd_code": "5917034",
  "fed_code": "59034",
  "fed_eng_name": "Victoria",
  "fed_fre_name": "Victoria",
  "er_code": "5910",
  "er_eng_name": "Vancouver Island and Coast",
  "er_fre_name": "Île de Vancouver et la côte",
  "reppoint_latitude": 48.4283,
  "reppoint_longitude": -123.355
}
```
