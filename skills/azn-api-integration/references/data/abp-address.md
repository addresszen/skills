# AddressBase Premium Address

A property record from Ordnance Survey's AddressBase Premium, Ordnance Survey's most detailed address dataset for Great Britain. Each record is a Basic Land and Property Unit (BLPU) keyed by its UPRN. Alongside the Royal Mail delivery point it carries the local authority address (`pao_*`, `sao_*`, `usrn`), classification (`classification_code`), lifecycle (`logical_status`, `blpu_state`), coordinates, Welsh alternatives (`welsh_*`), the street record (`street_*`) and cross references to OS MasterMap (`toid`), the Valuation Office Agency (`council_tax_ref`, `ndr_ref`) and ONS (`ons_ward_code`, `ons_parish_code`). Ordnance Survey publishes around 40 million records and refreshes them every six weeks.

How it differs from the neighbouring datasets:

- **AddressBase Core** (`ab`) is a weekly, flat cut of the current approved records: one row per UPRN with coordinates, a two-character classification and the key identifiers. It carries no history, no provisional records, no Welsh alternatives, no local authority address breakdown and no street, VOA or ONS cross references.
- **Royal Mail PAF** (`paf`) lists delivery points, keyed by UDPRN. The vast majority of PAF addresses are matched to a UPRN, but there will always be a small number (~1%) with no corresponding record on AddressBase Premium. PAF holds around 30 million GB delivery points against AddressBase Premium's 40 million UPRNs; the difference is non-postal objects (substations, car parks, sites under construction), provisional and historic records. Every GB PAF delivery point appears here as the `dpa_*` record.
- **OS NGD Address** carries the same content restructured into feature types with daily currency. AddressBase Premium is not being retired. The Ordnance Survey end of life notice for autumn 2027 covers AddressBase and AddressBase Plus only.

**Schema name:** `AbpAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `uprn` | yes | string | Unique Property Reference Number - a persistent identifier for a Basic |  |
| `parent_uprn` | no | string | UPRN of the parent record where a parent-child relationship exists |  |
| `logical_status` | yes | integer | Logical lifecycle status of the BLPU. `1` Approved, `6` Provisional, |  |
| `blpu_state` | no | string | Physical state of the BLPU. `1` Under construction, `2` In use, |  |
| `blpu_state_date` | no | string | Date the BLPU achieved its current state. |  |
| `country` | yes | string | Country containing the BLPU, determined by intersection with OS |  |
| `latitude` | yes | number | Latitude coordinate in the ETRS89 coordinate reference system. |  |
| `longitude` | yes | number | Longitude coordinate in the ETRS89 coordinate reference system. |  |
| `x_coordinate` | yes | number | X location in metres on the OSGB36 British National Grid |  |
| `y_coordinate` | yes | number | Y location in metres on the OSGB36 British National Grid |  |
| `rpc` | no | integer | Representative Point Code - reliability of the BLPU's coordinate, as |  |
| `local_custodian_code` | yes | integer | 4-digit identifier of the Local Authority responsible for maintaining |  |
| `addressbase_postal` | yes | string | Whether the address can receive mail per AddressBase rules. `D` linked |  |
| `postcode_locator` | yes | string | Royal Mail PAF postcode, locally assigned by the custodian, or |  |
| `multi_occ_count` | yes | integer | Count of child UPRNs for this record where parent-child relationships |  |
| `blpu_start_date` | no | string | Date the address record was inserted into the database. |  |
| `blpu_end_date` | no | string | Date the address record was closed in the database. |  |
| `blpu_last_update_date` | no | string | Date of the most recent attribute change on the BLPU record. |  |
| `blpu_entry_date` | no | string | Date the record was inserted into the Local Authority database. |  |
| `udprn` | no | string | Royal Mail's Unique Delivery Point Reference Number - primary key for |  |
| `organisation_name` | no | string | Royal Mail-recognised organisation name from DPA, falling back to the |  |
| `legal_name` | no | string | Registered legal name from the AddressBase Organisation record. |  |
| `department_name` | no | string | Subdivision of an organisation that receives mail at a distinct |  |
| `sub_building_name` | no | string | Property subdivision identifier (e.g. flat number). Requires |  |
| `building_name` | no | string | Descriptive name applied to a single building or small group of |  |
| `building_number` | no | integer | Numeric identifier for a single building or small group of buildings. |  |
| `dependent_thoroughfare` | no | string | Named thoroughfare within another named thoroughfare. Requires |  |
| `thoroughfare` | no | string | Road, track or named access route with Royal Mail delivery points. |  |
| `double_dependent_locality` | no | string | Estate or area name used to distinguish similar thoroughfares within a |  |
| `dependent_locality` | no | string | Subdivision of a post town to differentiate same-name thoroughfares. |  |
| `post_town` | no | string | Town or city of the Royal Mail sorting office serving this record. |  |
| `postcode` | yes | string | Royal Mail postcode from DPA, falling back to BLPU's `postcode_locator` |  |
| `postcode_type` | no | string | Royal Mail postal-user category. `S` Small user (e.g. a residential |  |
| `delivery_point_suffix` | no | string | Two-character code uniquely identifying an individual delivery point |  |
| `po_box_number` | no | string | Post Office Box number. |  |
| `welsh_dependent_thoroughfare` | no | string | Welsh translation of `dependent_thoroughfare`. Requires `welsh_thoroughfare`. |  |
| `welsh_thoroughfare` | no | string | Welsh translation of `thoroughfare`. |  |
| `welsh_double_dependent_locality` | no | string | Welsh translation of `double_dependent_locality`. Requires `welsh_dependent_locality`. |  |
| `welsh_dependent_locality` | no | string | Welsh translation of `dependent_locality`. |  |
| `welsh_post_town` | no | string | Welsh translation of `post_town`. |  |
| `dpa_process_date` | no | string | Date the PAF record was processed into the database. |  |
| `dpa_start_date` | no | string | Date the address record was matched to the Delivery Point Address. |  |
| `dpa_end_date` | no | string | Date the PAF record no longer existed in the database. |  |
| `dpa_last_update_date` | no | string | Date any attribute on the DPA record was last changed. |  |
| `dpa_entry_date` | no | string | Date the PAF record was first loaded by GeoPlace. |  |
| `classification_code` | no | string | Current AddressBase classification code (e.g. `RD` residential, |  |
| `class_scheme` | no | string | Name of the classification scheme applied to this record. |  |
| `scheme_version` | no | number | Version number of the classification scheme in use (e.g. `1.0`). |  |
| `classification_start_date` | no | string | Date the classification record was first loaded into the database. |  |
| `classification_end_date` | no | string | Date the classification record ceased to exist. |  |
| `classification_last_update_date` | no | string | Date of the most recent attribute change on the classification record. |  |
| `classification_entry_date` | no | string | Date the associated address record was inserted into the Local |  |
| `organisation_start_date` | no | string | Date the organisation record was initially loaded into the database. |  |
| `organisation_end_date` | no | string | Date the organisation record ceased to exist. |  |
| `organisation_last_update_date` | no | string | Date of the most recent attribute change on the organisation record. |  |
| `organisation_entry_date` | no | string | Date the UPRN was entered into the Local Authority database. |  |
| `lpi_key` | no | string | Unique identifier and primary key for the LPI record. |  |
| `lpi_language` | no | string | Language used for this LPI record. `ENG` English, `CYM` Welsh, |  |
| `lpi_logical_status` | no | integer | Logical status of the LPI record. `1` Approved, `3` Alternative, |  |
| `lpi_start_date` | no | string | Date the LPI was first loaded into the database. |  |
| `lpi_end_date` | no | string | Date the LPI record ceased to exist. |  |
| `lpi_last_update_date` | no | string | Date of the most recent attribute change on the LPI record. |  |
| `lpi_entry_date` | no | string | Date the LPI record was inserted into the Local Authority database. |  |
| `sao_start_number` | no | integer | Number of the Secondary Addressable Object, or range start. Requires |  |
| `sao_start_suffix` | no | string | Suffix appended to `sao_start_number`. Requires `sao_start_number`. |  |
| `sao_end_number` | no | integer | End number of the SAO range. Requires `sao_start_number`. |  |
| `sao_end_suffix` | no | string | Suffix appended to `sao_end_number`. Requires `sao_end_number`. |  |
| `sao_text` | no | string | Building name or description for the Secondary Addressable Object |  |
| `pao_start_number` | no | integer | Number of the Primary Addressable Object, or range start. Mandatory if |  |
| `pao_start_suffix` | no | string | Suffix appended to `pao_start_number`. Requires `pao_start_number`. |  |
| `pao_end_number` | no | integer | End number of the PAO range. Requires `pao_start_number`. |  |
| `pao_end_suffix` | no | string | Suffix appended to `pao_end_number`. Requires `pao_end_number`. |  |
| `pao_text` | no | string | Building name or description for the Primary Addressable Object. |  |
| `usrn` | no | string | Unique Street Reference Number linking this LPI to its Street record. |  |
| `usrn_match_indicator` | no | string | Confidence of the LPI to Street linkage. `1` Matched manually to the |  |
| `area_name` | no | string | Third-level geographic area name such as island or property group. |  |
| `level` | no | string | Vertical position of the property (e.g. "GROUND FLOOR"). |  |
| `official_flag` | no | string | Whether the LPI corresponds to an entry in the official Street Name and |  |
| `street_record_type` | no | integer | Description of the street record type. `1` Official designated Street |  |
| `swa_org_ref_naming` | no | integer | Code identifying the Street Naming and Numbering Authority or Local |  |
| `street_state` | no | string | Current state of the street. `1` Under construction, `2` Open, |  |
| `street_state_date` | no | string | Date when the street achieved its current state. |  |
| `street_surface` | no | string | Surface finish of the street. `1` Metalled, `2` Unmetalled, `3` Mixed. |  |
| `street_classification` | no | string | Primary classification of the street record. `4` Pedestrian way or |  |
| `street_start_date` | no | string | Date this street record or version was inserted into the database. |  |
| `street_last_update_date` | no | string | Date when any attribute of the street record was last changed. |  |
| `street_record_entry_date` | no | string | Date the street record was entered into the Local Authority database. |  |
| `street_start_x` | no | number | X coordinate (BNG) for the street start point. |  |
| `street_start_y` | no | number | Y coordinate (BNG) for the street start point. |  |
| `street_start_lat` | no | number | Latitude (ETRS89) for the street start point. |  |
| `street_start_long` | no | number | Longitude (ETRS89) for the street start point. |  |
| `street_end_x` | no | number | X coordinate (BNG) for the street end point. |  |
| `street_end_y` | no | number | Y coordinate (BNG) for the street end point. |  |
| `street_end_lat` | no | number | Latitude (ETRS89) for the street end point. |  |
| `street_end_long` | no | number | Longitude (ETRS89) for the street end point. |  |
| `street_tolerance` | no | integer | Accuracy of street-coordinate data capture, in metres. |  |
| `street_description` | no | string | Street name, description or street number. |  |
| `street_locality` | no | string | Geographical area within a town. |  |
| `street_town` | no | string | Name of the town. Required for Street Record Types `1` and `2`; |  |
| `adminstrative_area` | no | string | Local Highway Authority name (administrative area / county / unitary |  |
| `sd_language` | no | string | Language of the street descriptor. `ENG` English, `CYM` Welsh, |  |
| `sd_start_date` | no | string | Date the street descriptor record was first created in the database. |  |
| `sd_end_date` | no | string | Date the street descriptor record ceased to exist. |  |
| `sd_last_update_date` | no | string | Date of the most recent attribute change on the street descriptor record. |  |
| `sd_entry_date` | no | string | Date the street descriptor record was entered into the Local Authority |  |
| `toid` | no | string | OS MasterMap Topography Layer TOID (cross-reference source `7666MT`) |  |
| `toid_address` | no | string | OS MasterMap Address Layer 2 TOID (cross-reference source `7666MA`) |  |
| `toid_highways` | no | string | OS MasterMap Highways TOID (cross-reference source `7666MI`) linked to |  |
| `council_tax_ref` | no | string | Centrally created Valuation Office Agency council tax reference |  |
| `ndr_ref` | no | string | Centrally created Valuation Office Agency non-domestic rates reference |  |
| `ons_ward_code` | no | string | Office for National Statistics ward code (cross-reference source |  |
| `ons_parish_code` | no | string | Office for National Statistics parish code (cross-reference source |  |
| `id` | yes | string | Stable identifier for the record, `abp_` prefixed to the UPRN. Accepted |  |
| `dataset` | yes | `abp` | Dataset this record belongs to. |  |
| `country_iso` | yes | `GBR` | ISO 3166-1 alpha-3 code for the country covered by the dataset. Always |  |
| `suggestion_line` | yes | string | Single-line address used for autocomplete suggestions: the address line |  |

## Example

```json
{
  "uprn": "49020496",
  "parent_uprn": "49020495",
  "logical_status": 1,
  "blpu_state": "2",
  "blpu_state_date": "2011-10-06T00:00:00.000Z",
  "country": "W",
  "latitude": 52.4121999,
  "longitude": -4.0883772,
  "x_coordinate": 258053.87,
  "y_coordinate": 281405.95,
  "rpc": 2,
  "local_custodian_code": 6820,
  "addressbase_postal": "D",
  "postcode_locator": "SY23 1JT",
  "multi_occ_count": 4,
  "blpu_start_date": "2007-10-24T00:00:00.000Z",
  "blpu_end_date": null,
  "blpu_last_update_date": "2025-10-13T00:00:00.000Z",
  "blpu_entry_date": "2006-11-24T00:00:00.000Z",
  "udprn": "24255522",
  "organisation_name": null,
  "legal_name": null,
  "department_name": null,
  "sub_building_name": null,
  "building_name": null,
  "building_number": 1,
  "dependent_thoroughfare": "Castle Terrace",
  "thoroughfare": "South Road",
  "double_dependent_locality": null,
  "dependent_locality": null,
  "post_town": "Aberystwyth",
  "postcode": "SY23 1JT",
  "postcode_type": "S",
  "delivery_point_suffix": "1A",
  "po_box_number": null,
  "welsh_dependent_thoroughfare": "HEOL Y CASTELL",
  "welsh_thoroughfare": "TAN Y CAE",
  "welsh_double_dependent_locality": null,
  "welsh_dependent_locality": null,
  "welsh_post_town": "ABERYSTWYTH",
  "dpa_process_date": "2016-01-18T00:00:00.000Z",
  "dpa_start_date": "2012-04-23T00:00:00.000Z",
  "dpa_end_date": null,
  "dpa_last_update_date": "2016-02-10T00:00:00.000Z",
  "dpa_entry_date": "2012-03-19T00:00:00.000Z",
  "classification_code": "RD04",
  "class_scheme": "AddressBase Premium Classification Scheme",
  "scheme_version": 1,
  "classification_start_date": "2007-10-24T00:00:00.000Z",
  "classification_end_date": null,
  "classification_last_update_date": "2018-09-23T00:00:00.000Z",
  "classification_entry_date": "2006-11-24T00:00:00.000Z",
  "organisation_start_date": null,
  "organisation_end_date": null,
  "organisation_last_update_date": null,
  "organisation_entry_date": null,
  "lpi_key": "6820L000054880",
  "lpi_language": "CYM",
  "lpi_logical_status": 1,
  "lpi_start_date": "2007-10-24T00:00:00.000Z",
  "lpi_end_date": null,
  "lpi_last_update_date": "2025-09-26T00:00:00.000Z",
  "lpi_entry_date": "2007-09-04T00:00:00.000Z",
  "sao_start_number": null,
  "sao_start_suffix": null,
  "sao_end_number": null,
  "sao_end_suffix": null,
  "sao_text": null,
  "pao_start_number": 1,
  "pao_start_suffix": null,
  "pao_end_number": null,
  "pao_end_suffix": null,
  "pao_text": "HEOL Y CASTELL",
  "usrn": "47114724",
  "usrn_match_indicator": "1",
  "area_name": null,
  "level": null,
  "official_flag": "Y",
  "street_record_type": 1,
  "swa_org_ref_naming": 6820,
  "street_state": "2",
  "street_state_date": "1990-01-01T00:00:00.000Z",
  "street_surface": "1",
  "street_classification": null,
  "street_start_date": "2007-10-24T00:00:00.000Z",
  "street_last_update_date": "2022-01-14T00:00:00.000Z",
  "street_record_entry_date": "1998-07-14T00:00:00.000Z",
  "street_start_x": 257968,
  "street_start_y": 281400,
  "street_start_lat": 52.4121241,
  "street_start_long": -4.0896363,
  "street_end_x": 258266,
  "street_end_y": 281393,
  "street_end_lat": 52.4121386,
  "street_end_long": -4.0852551,
  "street_tolerance": 10,
  "street_description": "SOUTH ROAD",
  "street_locality": null,
  "street_town": "ABERYSTWYTH",
  "adminstrative_area": "CEREDIGION",
  "sd_language": "ENG",
  "sd_start_date": "2007-10-24T00:00:00.000Z",
  "sd_end_date": null,
  "sd_last_update_date": "2016-02-06T00:00:00.000Z",
  "sd_entry_date": "1998-07-14T00:00:00.000Z",
  "toid": "osgb1000020592167",
  "toid_address": "osgb1000002175099422",
  "toid_highways": "osgb5000005181786114",
  "council_tax_ref": null,
  "ndr_ref": null,
  "ons_ward_code": "W05001302",
  "ons_parish_code": "W04000359",
  "id": "abp_49020496",
  "dataset": "abp",
  "country_iso": "GBR",
  "suggestion_line": "1 Castle Terrace South Road, Aberystwyth, SY23"
}
```
