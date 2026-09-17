# Address

A single address.

Every address is returned in this shape, whatever dataset it came from. US and non-US addresses share the same fields, so an integration reads one format only.

- `dataset` identifies where the address came from. Fields a dataset does not carry are returned as an empty string (`""`)
- `native` carries the raw dataset record, exactly as the dataset supplies it. Retrieve Address returns it for every dataset except `usps`, whose address already is the USPS record

**Schema name:** `Address`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | string | Indicates the provenance of an address. |  |
| `country_iso` | yes | string | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | string | 2 letter country code (ISO 3166-1) |  |
| `country` | yes | string | Full country names (ISO 3166) |  |
| `language` | yes | string | Language represented by 2 letter ISO Code (639-1) |  |
| `primary_number` | yes | string | Building, house, rural route, contract box or PO Box number. The numeric or alphanumeric component of an address preceding the street name. |  |
| `secondary_number` | yes | string | Number of the sub unit, apartment, suite etc. |  |
| `plus_4_code` | yes | string | 4 digit ZIP add-on code. USPS addresses only. |  |
| `line_1` | yes | string | The primary delivery line (usually the street address) of the address. |  |
| `line_2` | yes | string | Secondary delivery line of the address. Typically populated if the first line is the firm or building name. |  |
| `last_line` | yes | string | Final line of the address, comprising city, state or region and postal code. |  |
| `zip_code` | yes | string | Postal code identifying the delivery area. For US addresses this is the 5 digit ZIP Code. |  |
| `zip_plus_4_code` | yes | string | Nine-digit code that identifies a small geographic delivery area serviceable by a single carrier; appears in the last line of the address on a mail piece. USPS addresses only. |  |
| `update_key_number` | yes | string | Key that uniquely identifies the source dataset record. For USPS this is the Update Key Number: a database segment code (V1, V2, W1, W2, X1, X2, Y1, Y2, Z1 or Z2) followed by eight alphanumeric characters. It is fixed for the life of the record and is not used in address matching. |  |
| `record_type_code` | yes | `G` \| `H` \| `F` \| `S` \| `P` \| `R` \| `M` \| `""` | An alphabetic value identifying the type of USPS record backing the address. |  |
| `carrier_route_id` | yes | string | A 4 character ID identifying the USPS postal route for the address. The first character indicates the route type: |  |
| `street_pre_directional_abbreviation` | yes | string | A geographic direction that precedes the street name. |  |
| `street_name` | yes | string | The official name of the street as assigned by the local governing authority. Contains the street name only, without directionals (EAST, WEST, etc.) or suffixes (ST, DR, BLVD, etc.). May also contain literals such as PO BOX, GENERAL DELIVERY, USS, PSC or UNIT. |  |
| `street_suffix_abbreviation` | yes | string | Standard abbreviation for the trailing designator in a street address. |  |
| `street_post_directional_abbreviation` | yes | string | A geographic direction that follows the street name. |  |
| `building_or_firm_name` | yes | string | The name of a company, building, apartment complex, shopping center, or other distinguishing secondary address information. |  |
| `address_secondary_abbreviation` | yes | string | A descriptive code identifying the type of secondary range held in the secondary number field, e.g. apartment, suite or trailer. |  |
| `base_alternate_code` | yes | `A` \| `B` \| `""` | Code specifying whether the backing USPS record is a base (preferred) or alternate record. |  |
| `lacs_status_indicator` | yes | `""` \| `L` | The Locatable Address Conversion Service (LACS) indicator marks USPS records converted to the LACS system, which lets mailers convert a rural route address to a city-style address so emergency services can locate it. |  |
| `government_building_indicator` | yes | `""` \| `A` \| `B` \| `C` \| `D` \| `E` \| `F` \| `G` | An alphabetic value identifying the type of government agency at the delivery point and/or whether a firm is the only delivery at an address. |  |
| `state_abbreviation` | yes | string | Abbreviated name of the state, province or region. For US addresses this is the 2 character state, territory or armed forces designation ("AA", "AE" or "AP" for APO/FPO/DPO). |  |
| `state` | yes | string | Full name of the state, province or region. |  |
| `municipality_city_state_key` | yes | string | Municipality City State Key. Currently blank. |  |
| `urbanization_city_state_key` | yes | string | An index to the USPS City State file that provides the urbanization name for this delivery range. |  |
| `preferred_last_line_city_state_key` | yes | string | An index to the USPS City State product record that provides the preferred last-line name for this address range. |  |
| `county` | yes | string | Name of the county, parish or equivalent administrative area. Blank for APO/FPO/DPO addresses. |  |
| `city` | yes | string | City or town name used for mailing; appears in the last line of the address. |  |
| `city_abbreviation` | yes | string | A standard 13-character abbreviation for a city/state name. Only used for names longer than 13 characters with a city state mailing name indicator of "Y"; blank otherwise. |  |
| `preferred_city` | yes | string | The default preferred or alternate preferred last-line name for a ZIP Code. |  |
| `city_state_name_facility_code` | yes | `B` \| `C` \| `N` \| `P` \| `S` \| `U` \| `Y` \| `""` | The type of locale identified in the city/state name. The facility may be a USPS facility, such as a post office, station or branch, or a non-postal place name. |  |
| `zip_classification_code` | yes | `""` \| `M` \| `P` \| `U` | Describes the type of ZIP area a 5-digit ZIP Code serves, e.g. a single educational institution, post office boxes only, or a single address with unusually high mail volume. |  |
| `city_state_mailing_name_indicator` | yes | string | Specifies whether the city state name can be used as the last line of an address on a mail piece. |  |
| `carrier_route_rate_sortation` | yes | string | Identifies where automation Carrier Route rates are available and where the commingling of automation and non-automation mail, including Enhanced Carrier Routes and 5-digit presort, on the same pallet or in the same container is allowed. |  |
| `finance_number` | yes | string \| number | A code assigned to USPS facilities (primarily Post Offices) to collect cost and statistical data and compile revenue and expense data. |  |
| `congressional_district_number` | yes | string \| number | A standard value identifying a geographic area within the United States served by a member of the U.S. House of Representatives. Blank for APO/FPO/DPO addresses. If there is only one member of Congress within a state, the code will be "AL" (at large). |  |
| `county_number` | yes | string \| number | The Federal Information Processing Standard (FIPS) code assigned to a given county or parish within a state. In Alaska it identifies a region within the state. Blank for APO/FPO/DPO addresses whose record type is "S", "H" or "F". |  |
| `native` | no | [NativeRecord](./native-record.md) | The raw dataset record backing an address, exactly as the dataset supplies it. One schema per dataset; `dataset` on the record says which. |  |

## Example

```json
{
  "id": "usps_V124884241|1040||0001",
  "dataset": "usps",
  "country": "United States",
  "country_iso": "USA",
  "country_iso_2": "US",
  "language": "en",
  "primary_number": "1040",
  "secondary_number": "",
  "plus_4_code": "0001",
  "line_1": "1040 Waverly Ave",
  "line_2": "",
  "last_line": "Holtsville NY 00501-0001",
  "zip_code": "00501",
  "zip_plus_4_code": "00501-0001",
  "update_key_number": "V124884241",
  "record_type_code": "S",
  "carrier_route_id": "C000",
  "street_pre_directional_abbreviation": "",
  "street_name": "Waverly",
  "street_suffix_abbreviation": "Ave",
  "street_post_directional_abbreviation": "",
  "building_or_firm_name": "",
  "address_secondary_abbreviation": "",
  "base_alternate_code": "B",
  "lacs_status_indicator": "",
  "government_building_indicator": "",
  "state_abbreviation": "NY",
  "state": "New York",
  "municipality_city_state_key": "",
  "urbanization_city_state_key": "",
  "preferred_last_line_city_state_key": "V13916",
  "county": "Suffolk",
  "city": "Holtsville",
  "city_abbreviation": "",
  "preferred_city": "Holtsville",
  "city_state_name_facility_code": "P",
  "zip_classification_code": "U",
  "city_state_mailing_name_indicator": "Y",
  "carrier_route_rate_sortation": "C",
  "finance_number": 353910,
  "congressional_district_number": 2,
  "county_number": 103
}
```
