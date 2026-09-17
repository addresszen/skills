# USPS Address

The USPS ZIP + 4 record backing a `usps` address.
Carries the complete USPS field set for the delivery point, including elements the standard address format does not expose.

**Schema name:** `UspsAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | `usps` | Identifies the address as sourced from USPS |  |
| `country` | yes | string | Full country names (ISO 3166) |  |
| `country_iso` | yes | string | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | string | 2 letter country code (ISO 3166-1) |  |
| `language` | yes | `en` | Language represented by 2 letter ISO Code (639-1) |  |
| `primary_number` | yes | string | A house, rural route, contract box, or Post Office Box number. The numeric or alphanumeric component of an address preceding the street name. Often referred to as house number. |  |
| `secondary_number` | yes | string | Number of the sub unit, apartment, suite etc |  |
| `plus_4_code` | yes | string | 4 digit ZIP add-on code. |  |
| `line_1` | yes | string | The primary delivery line (usually the street address) of the address. |  |
| `line_2` | yes | string | Secondary delivery line of the address. Typically populated if the first line is the firm or building name. |  |
| `last_line` | yes | string | Last line of the address comprising of city, state, zip code and zip+4 |  |
| `zip_code` | yes | string | A 5-digit code that identifies a specific geographic delivery area. ZIP Codes can represent an area within a state, or a single building or company that has a very high mail volume. |  |
| `zip_plus_4_code` | yes | string | Nine-digit code that identifies a small geographic delivery area that is serviceable by a single carrier; appears in the last line of the address on a mail piece. |  |
| `update_key_number` | yes | string | Field that contains a number that uniquely identifies a record; used to identify the base record to which an add or delete transaction is being directed. The Update Key Number field is used only when applying transactions to the base file; it is not used in address matching and remains fixed for the life of the record. The field is alphanumeric and consists of the database segment code (V1, V2, W1, W2, X1, X2, Y1, Y2, Z1, or Z2) and eight characters containing an alphanumeric value ranging from 00000001 to AAAAAAAA. |  |
| `record_type_code` | yes | `G` \| `H` \| `F` \| `S` \| `P` \| `R` \| `M` \| `""` | An alphabetic value that identifies the type of data in the record. - G = General delivery (5-Digit ZIP, ZIP + 4, and Carrier Route products) - H = High-rise (ZIP + 4 only) - F = Firm (ZIP + 4 only) - S = Street (5-Digit ZIP, ZIP + 4, and Carrier Route products) - P = PO Box (5-Digit ZIP, ZIP + 4, and Carrier Route products) - R = Rural route/contract (5-Digit ZIP, ZIP + 4, and Carrier Route products) - M = Multi-carrier (Carrier Route product only) |  |
| `carrier_route_id` | yes | string | A 4 character ID identifying the postal route for the address. |  |
| `street_pre_directional_abbreviation` | yes | string | A geographic direction that precedes the street name. |  |
| `street_name` | yes | string | The official name of a street as assigned by a local governing authority. The Street Name field contains only the street name and does not include directionals (EAST, WEST, etc.) or suffixes (ST, DR, BLVD, etc.). This element may also contain literals, such as PO BOX, GENERAL DELIVERY, USS, PSC, or UNIT. |  |
| `street_suffix_abbreviation` | yes | string | Code that is the standard USPS abbreviation for the trailing designator in a street address. |  |
| `street_post_directional_abbreviation` | yes | string | A geographic direction that follows the street name. |  |
| `building_or_firm_name` | yes | string | The name of a company, building, apartment complex, shopping center, or other distinguishing secondary address information. |  |
| `address_secondary_abbreviation` | yes | string | A descriptive code used to identify the type of address secondary range information in the Address Secondary Range field. |  |
| `base_alternate_code` | yes | `A` \| `B` \| `""` | Code that specifies whether a record is a base (preferred) or alternate record. |  |
| `lacs_status_indicator` | yes | `""` \| `L` | The Locatable Address Conversion Service (LACS) indicator describes records that have been converted to the LACS system (a product/system in a different USPS® product line that allows mailers to identify and convert a rural route address to a city-style address). Rural route and some city addresses are being modified to city-style addresses so that emergency services (e.g., ambulances, police) can find these addresses more efficiently. |  |
| `government_building_indicator` | yes | `""` \| `A` \| `B` \| `C` \| `D` \| `E` \| `F` \| `G` | An alphabetic value that identifies the type of government agency at the delivery point and/or whether a firm is the only delivery at an address. For this purpose, "address" is defined as the complete delivery line (e.g., complete street address and, if included as part of the firm record, the secondary abbreviation and/or address secondary number). |  |
| `state_abbreviation` | yes | string | A 2-character abbreviation for the name of a state, U.S. territory, or armed forces ZIP Code designation. If APO/FPO/DPO, then the state abbreviation will be “AA,” “AE,” or “AP.” |  |
| `state` | yes | string | Full name of a state, U.S. territory, or armed forces ZIP Code designation. |  |
| `municipality_city_state_key` | yes | string | Municipality City State Key. Currently blank. |  |
| `urbanization_city_state_key` | yes | string | An index to the City State file that provides the urbanization name for this delivery range. |  |
| `preferred_last_line_city_state_key` | yes | string | In the Carrier Route, Five-Digit ZIP Code, Delivery Statistics, and ZIP + 4 products, an index to the City State product record that provides the preferred last-line name for this address range. In the City State product, the preferred last line city/state key contains the key value of a City State product record that has the default preferred or alternate preferred last-line key for a given ZIP Code. |  |
| `county` | yes | string | The name of the county or parish in which the 5-digit ZIP Code resides. If APO/FPO/DPO, then the county name will be blank. |  |
| `city` | yes | string | A valid city name for mailing purposes; appears in the last line of an address on a mail piece. |  |
| `city_abbreviation` | yes | string | A standard 13-character abbreviation for a city/state name. This field is only used for names that are greater than 13 characters in length and have a city/state mailing name indicator of "Y." If the field is longer than 13 characters and the city/state mailing name indicator is "N," the field will be blank. |  |
| `preferred_city` | yes | string | Field that contains the default preferred or alternate preferred last-line name for a ZIP Code. |  |
| `city_state_name_facility_code` | yes | `B` \| `C` \| `N` \| `P` \| `S` \| `U` \| `Y` \| `""` | The type of locale identified in the city/state name. The facility may be a USPS facility, such as a post office, station, or branch, or it may be a non-postal place name. City/state name facility codes include the following: |  |
| `zip_classification_code` | yes | `""` \| `M` \| `P` \| `U` | A field that describes the type of ZIP area that a 5-digit ZIP Code serves, e.g., a single educational institution, post office boxes only, or a single address that has unusually high mail volume or many different addresses. - M = Military ZIP Code - P = ZIP Code having only Post Office Boxes - U = Unique ZIP Code (ZIP assigned to a single organization) - Blank = Standard ZIP with many addresses assigned to it |  |
| `city_state_mailing_name_indicator` | yes | string | Specifies whether or not the city state name can be used as a last line of address on a mail piece. |  |
| `carrier_route_rate_sortation` | yes | string | Identifies where automation Carrier Route rates are available and where the commingling of automation and non-automation mail, including Enhanced Carrier Routes and 5-digit presort, on the same pallet or in the same container is allowed. |  |
| `finance_number` | yes | string \| number | A code assigned to Postal Service facilities (primarily Post Offices) to collect cost and statistical data and compile revenue and expense data. |  |
| `congressional_district_number` | yes | string \| number | A standard value identifying a geographic area within the United States served by a member of the U.S. House of Representatives. If Army/Air Force (APO), Fleet Post Office (FPO), or Diplomatic/Defense Post Office (DPO), this field will be blank. If there is only one member of Congress within a state, the code will be "AL" (at large). |  |
| `county_number` | yes | string \| number | The Federal Information Processing Standard (FIPS) code assigned to a given county or parish within a state. In Alaska, it identifies a region within the state. If APO/FPO/DPO, and the record type is “S,” “H,” or “F,” the county number will be blank. |  |

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
