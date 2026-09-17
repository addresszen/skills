# Australia G-NAF Address

An Australian address from the Geocoded National Address File (G-NAF), published by Geoscape. Covers Australia and the external territories of Cocos (Keeling) Islands, Christmas Island and Norfolk Island.

Every attribute is always present. The API returns fields with no value as an empty string `""`.

The API returns attributes sourced from a one-to-many table (address aliases, site geocodes, locality aliases, street locality aliases) as a single comma separated string, with one element per related record. Related lists share an ordering, so the nth element of each describes the same record.

**Schema name:** `GnafAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | `gnaf` |  |  |
| `country` | yes | `Australia` \| `Cocos (Keeling) Islands` \| `Christmas Island` \| `Norfolk Island` | Full country names (ISO 3166) |  |
| `country_iso` | yes | `AUS` \| `CCK` \| `CXR` \| `NFK` | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | `AU` \| `CC` \| `CX` \| `NF` | 2 letter country code (ISO 3166-1) |  |
| `line_1` | yes | string | First address line. The building name where one is recorded, otherwise the street line. |  |
| `line_2` | yes | string | Second address line. The street line where `line_1` carries a building name. |  |
| `language` | yes | `en` | Language represented by 2 letter ISO Code (639-1) |  |
| `address` | yes | string | Address / House Number uniquely identifying the address along the specified street. For a ranged address this is the number matched from the query, not the whole range. |  |
| `latitude` | yes | string \| number | The latitude of the address or postcode (WGS84). |  |
| `longitude` | yes | string \| number | The longitude of the address or postcode (WGS84). |  |
| `address_detail_pid` | yes | string | The Persistent Identifier is unique to the real world feature this record represents. |  |
| `date_created` | yes | string | ISO 8601 date-time this record was created. |  |
| `date_last_modified` | yes | string | ISO 8601 date-time this record was last modified (not retired/recreated in line with ICSM standard). |  |
| `date_retired` | yes | string | ISO 8601 date-time this record was retired. |  |
| `building_name` | yes | string | Combines both building/property name fields. Field length: up to 200 alphanumeric characters (AS4590:2006 5.7). |  |
| `lot_number_prefix` | yes | string | Lot number prefix. Field length: up to two alphanumeric characters (AS4590:2006 5.8.1). |  |
| `lot_number` | yes | string | Lot number. Field length: up to five alphanumeric characters (AS4590:2006 5.8.1). |  |
| `lot_number_suffix` | yes | string | Lot number suffix. Field length: up to two alphanumeric characters (AS4590:2006 5.8.1). |  |
| `flat_type_code` | yes | string | Specification of the type of a separately identifiable portion within a building/complex. Field Length: up to seven upper case alpha characters (AS4590:2006 5.5.1.1). |  |
| `flat_number_prefix` | yes | string | Flat/unit number prefix. Field length: up to two alphanumeric characters (AS4590:2006 5.5.1.2). |  |
| `flat_number` | yes | string \| integer |  |  |
| `flat_number_suffix` | yes | string | Flat/unit number suffix. Field length: up to two alphanumeric characters (AS4590:2006 5.5.1.2). |  |
| `level_type_code` | yes | string | Level type. Field length: up to four alphanumeric characters (AS4590:2006 5.5.2.1). |  |
| `level_number_prefix` | yes | string | Level number prefix. Field length: up to two alphanumeric characters (AS4590:2006 5.5.2.2). |  |
| `level_number` | yes | string \| integer |  |  |
| `level_number_suffix` | yes | string | Level number suffix. Field length: up to two alphanumeric characters (AS4590:2006 5.5.2.2). |  |
| `number_first_prefix` | yes | string | Prefix for the first (or only) number in range. Field length: up to three uppercase alphanumeric characters (AS4590:2006 5.5.3.1). |  |
| `number_first` | yes | string \| integer |  |  |
| `number_first_suffix` | yes | string | Suffix for the first (or only) number in range. Field length: up to two uppercase alphanumeric characters (AS4590:2006 5.5.3.1). |  |
| `number_last_prefix` | yes | string | Prefix for the last number in range. Field length: up to three uppercase alphanumeric characters (AS4590:2006 5.5.3.2). |  |
| `number_last` | yes | string \| integer |  |  |
| `number_last_suffix` | yes | string | Suffix for the last number in range. Field length: up to two uppercase alphanumeric characters (AS4590:2006 5.5.3.2). |  |
| `street_locality_pid` | yes | string | Identifier of the street locality this address sits on. Not mandatory - some G-NAF records do not require a street (e.g. a remote rural property). |  |
| `alias_principal` | yes | string | A = Alias record, P = Principal record. |  |
| `postcode` | yes | string | Postcodes are optional as prescribed by AS4819 and AS4590:2006 5.13. |  |
| `private_street` | yes | string | Private street information. This is not broken up into name/type/suffix. Field length: up to 75 alphanumeric characters. This is not currently populated. |  |
| `legal_parcel_id` | yes | string | Generic parcel id field derived from the Geoscape Australia's Cadastre parcel where available. |  |
| `confidence` | yes | string \| integer |  |  |
| `level_geocoded_code` | yes | integer | Binary indicator of the level of geocoding this address has. e.g. 0 = 000 = (No geocode), 1 = 001 = (No Locality geocode, No Street geocode, Address geocode), etc. |  |
| `primary_secondary` | yes | string | Indicator that identifies if the address is P (Primary) or S (secondary). |  |
| `alias_type_code` | yes | string | Comma separated alias types for this address (e.g. "Synonym"), one per alias record. |  |
| `geocode_type_code` | yes | string | Unique abbreviation for the geocode type of the default geocode. |  |
| `default_latitude` | yes | string \| number |  |  |
| `default_longitude` | yes | string \| number |  |  |
| `address_change_type_code` | yes | string | The code indicating the type of change, for example, LOC-STN for locality name and street name change. |  |
| `mb_2016_match_code` | yes | string | Code for the 2016 mesh block match e.g. 1. |  |
| `mb_2021_match_code` | yes | string | Code for the 2021 mesh block match e.g. 1. |  |
| `address_type` | yes | string | Address type (e.g. "Postal", "Physical"). |  |
| `address_site_name` | yes | string | Address site name. Field length: 200 alphanumeric characters. |  |
| `geocode_site_name` | yes | string | Comma separated identifiers relating to each geocoded site (e.g. "Transformer 75658"), one per site geocode record. |  |
| `site_geocode_type_code` | yes | string | Comma separated abbreviations for each site geocode feature (e.g. "PRCL") (SAWG 7.4.1), one per site geocode record. |  |
| `reliability_code` | yes | string | Comma separated spatial precision of each site geocode, expressed as a number in the range 1 (unique identification of feature) to 6 (feature associated to region i.e. postcode). |  |
| `site_boundary_extent` | yes | string | Comma separated measurements (metres) of each site geocode from other geocodes associated with the same address persistent identifier. |  |
| `site_planimetric_accuracy` | yes | string | Comma separated planimetric accuracy of each site geocode. |  |
| `elevation` | yes | string | Comma separated elevation of each site geocode. This field is not currently populated. |  |
| `site_longitude` | yes | string | Comma separated longitude of each site geocode (GDA2020). |  |
| `site_latitude` | yes | string | Comma separated latitude of each site geocode (GDA2020). |  |
| `geocode_type_priority_order` | yes | string \| integer |  |  |
| `site_geocode_priority_order` | yes | string | Comma separated priority order of each site geocode type, 1 (most precise) to 29 (least precise), one per site geocode record. |  |
| `locality_name` | yes | string | The name of the locality or suburb. |  |
| `primary_postcode` | yes | string | Required to differentiate localities of the same name within a state. |  |
| `locality_class_code` | yes | string | Describes the class of locality (e.g. Gazetted, topographic feature etc.). Lookup to locality class. |  |
| `locality_gnaf_reliability_code` | yes | string \| integer |  |  |
| `locality_alias_name` | yes | string | Comma separated alias names for the locality or suburb. |  |
| `locality_alias_postcode` | yes | string | Comma separated postcodes, one per locality alias. |  |
| `locality_alias_type_code` | yes | string | Comma separated alias type codes, one per locality alias. |  |
| `locality_planimetric_accuracy` | yes | string \| integer |  |  |
| `locality_latitude` | yes | string \| number |  |  |
| `locality_longitude` | yes | string \| number |  |  |
| `mb_2016_code` | yes | string | The 2016 mesh block code. |  |
| `mb_2021_code` | yes | string | The 2021 mesh block code. |  |
| `ps_join_type_code` | yes | string | Comma separated join type codes, one per primary/secondary link on this address. Each is 1 OR 2 when the root address:- |  |
| `state_name` | yes | string | The state or territory name, title cased. E.g. Tasmania. |  |
| `state_abbreviation` | yes | string | The state or territory abbreviation. |  |
| `street_class_code` | yes | string | Defines whether this street represents a confirmed or unconfirmed street. |  |
| `street_name` | yes | string | Street name. e.g. "Barney". |  |
| `street_type_code` | yes | string | The street type code. e.g. "Street". |  |
| `street_suffix_code` | yes | string | The street suffix code. e.g. "West". |  |
| `gnaf_street_confidence` | yes | string \| integer |  |  |
| `street_locality_gnaf_reliability_code` | yes | string \| integer |  |  |
| `street_locality_alias_street_name` | yes | string | Comma separated street alias names. e.g. "Poplar". |  |
| `street_locality_alias_street_type_code` | yes | string | Comma separated street type codes, one per street alias. e.g. "Place". |  |
| `street_locality_alias_street_suffix_code` | yes | string | Comma separated street suffix codes, one per street alias. e.g. "West". |  |
| `street_locality_alias_type_code` | yes | string | Comma separated alias type codes, one per street alias. |  |
| `street_locality_boundary_extent` | yes | string \| integer |  |  |
| `street_locality_planimetric_accuracy` | yes | string \| integer |  |  |
| `street_locality_latitude` | yes | string \| number |  |  |
| `street_locality_longitude` | yes | string \| number |  |  |
| `street_type_name` | yes | string | Abbreviation of the street type. e.g. "St". |  |
| `street_locality_alias_street_type_name` | yes | string | Comma separated abbreviations of the street type, one per street alias. e.g. "St". |  |

## Example

```json
{
  "id": "gnaf_GAQLD157509281|99",
  "dataset": "gnaf",
  "country": "Australia",
  "country_iso": "AUS",
  "country_iso_2": "AU",
  "line_1": "Flat 3 99 Barney St",
  "line_2": "",
  "language": "en",
  "address": "99",
  "latitude": -23.85175973,
  "longitude": 151.27280546,
  "address_detail_pid": "GAQLD157509281",
  "date_created": "2015-07-22T00:00:00.000Z",
  "date_last_modified": "2021-07-07T00:00:00.000Z",
  "date_retired": "",
  "building_name": "",
  "lot_number_prefix": "",
  "lot_number": "1",
  "lot_number_suffix": "",
  "flat_type_code": "Flat",
  "flat_number_prefix": "",
  "flat_number": 3,
  "flat_number_suffix": "",
  "level_type_code": "",
  "level_number_prefix": "",
  "level_number": "",
  "level_number_suffix": "",
  "number_first_prefix": "",
  "number_first": 99,
  "number_first_suffix": "",
  "number_last_prefix": "",
  "number_last": "",
  "number_last_suffix": "",
  "street_locality_pid": "QLD106251",
  "alias_principal": "P",
  "postcode": "4680",
  "private_street": "",
  "legal_parcel_id": "1/RP611454",
  "confidence": 2,
  "level_geocoded_code": 7,
  "primary_secondary": "S",
  "alias_type_code": "",
  "geocode_type_code": "PC",
  "default_latitude": -23.85175973,
  "default_longitude": 151.27280546,
  "address_change_type_code": "",
  "mb_2016_match_code": "1",
  "mb_2021_match_code": "1",
  "address_type": "UN",
  "address_site_name": "",
  "geocode_site_name": "",
  "site_geocode_type_code": "PC",
  "reliability_code": "2",
  "site_boundary_extent": "",
  "site_planimetric_accuracy": "",
  "elevation": "",
  "site_longitude": "151.27280546",
  "site_latitude": "-23.85175973",
  "geocode_type_priority_order": 14,
  "site_geocode_priority_order": "14",
  "locality_name": "Barney Point",
  "primary_postcode": "",
  "locality_class_code": "G",
  "locality_gnaf_reliability_code": 5,
  "locality_alias_name": "South Gladstone,Gladstone Harbour,Gladstone City,Gladstone",
  "locality_alias_postcode": ",,,",
  "locality_alias_type_code": "SYN,SYN,SYN,SYN",
  "locality_planimetric_accuracy": "",
  "locality_latitude": -23.84320223,
  "locality_longitude": 151.26897733,
  "mb_2016_code": "30563058200",
  "mb_2021_code": "30563058200",
  "ps_join_type_code": "1",
  "state_name": "Queensland",
  "state_abbreviation": "QLD",
  "street_class_code": "C",
  "street_name": "Barney",
  "street_type_code": "Street",
  "street_suffix_code": "",
  "gnaf_street_confidence": 3,
  "street_locality_gnaf_reliability_code": 4,
  "street_locality_alias_street_name": "",
  "street_locality_alias_street_type_code": "",
  "street_locality_alias_street_suffix_code": "",
  "street_locality_alias_type_code": "",
  "street_locality_boundary_extent": 576,
  "street_locality_planimetric_accuracy": "",
  "street_locality_latitude": -23.85114069,
  "street_locality_longitude": 151.27296937,
  "street_type_name": "St",
  "street_locality_alias_street_type_name": ""
}
```
