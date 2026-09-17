# United States CASS Verified Address

Address retrieved using CASS compliant address verification process

**Schema name:** `UsaCassVerifiedAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `address1` | yes | string | Primary delivery address |  |
| `address2` | yes | string | Secondary address information |  |
| `address3` | yes | string | Additional secondary address information |  |
| `area_code` | yes | string | Area code. Also known as Numbering Plan Area (NPA) https://en.wikipedia.org/wiki/List_of_North_American_Numbering_Plan_area_codes |  |
| `carrier_route` | yes | string | Data required to perform a Carrier Route sort |  |
| `check_digit` | yes | string | Character following the 5 or 9 digit ZIP Code. Part of the 11-digit barcode |  |
| `city` | yes | string | City name |  |
| `city_abbreviation` | yes | string | City Abbreviation. Empty string if not present |  |
| `congressional_district` | yes | string | Identifies the Congressional District. Empty string if not present |  |
| `country_code` | yes | string | ISO3166 country code. Empty string if not present |  |
| `county` | yes | string | Name of the county |  |
| `day_light_savings` | yes | boolean | Daylight saving time indicator |  |
| `delivery_point` | yes | string | Last 2 digits of the primary street address number or Post Office box |  |
| `dpv` | yes | `Y` \| `S` \| `D` \| `N` \| `""` | Delivery Point Validation (DPV) Confirmation code. |  |
| `dpv_cmra` | yes | `Y` \| `N` \| `""` | Delivery Point Validation (DPV) CMRA code. |  |
| `dpv_footnotes` | yes | string | Delivery Point Validation (DPV) Footnotes. Empty string if not present |  |
| `dpv_no_stat` | yes | `Y` \| `N` \| `""` | Delivery Point Validation (DPV) NoStat code. |  |
| `dpv_vacant` | yes | `Y` \| `N` \| `""` | Delivery Point Validation (DPV) Vacant code. |  |
| `elot` | yes | string | Enhanced Line of Travel. For arranging records in the order that a route is served by a carrier. eLOT sequencing, when combined with Carrier Route codes, may allow Enhanced Carrier Route (ECR) discounts to be claimed. |  |
| `finance_number` | yes | string | Internal accounting number used by the USPS® when Post Offices or ZIP Codes are discontinued and reassigned. The finance number reflects the geographic grouping of ZIP + 4 areas in which these changes can be made. |  |
| `fips_county_code` | yes | string | Federal Information Processing Standard code for a county. Empty string if not present |  |
| `firm` | yes | string | Company name in a business address |  |
| `footnotes` | yes | string | Letter codes returned by ZIP+4 encoding. Empty string if not present |  |
| `geo_coded` | yes | boolean | Indicates whether the address was geo-coded |  |
| `lacs_indicator` | yes | `L` \| `""` | Indicates whether a record may benefit from LACS processing. |  |
| `lacs_link_footnote` | yes | `A` \| `00` \| `09` \| `14` \| `92` \| `""` | LACSLink Footnote. Return Code returned by the LACSLink process when an accurate address match could not be made. These codes help identify the type of move and the type of deficiency in the record which prevents a match. |  |
| `lacs_link_indicator` | yes | `Y` \| `S` \| `N` \| `""` | LACSLink Indicator. Indicates whether the input address matched a record in the LACSLink database. |  |
| `latitude` | yes | string | Latitude of the encoded address. Empty string if not present |  |
| `longitude` | yes | string | Longitude of the encoded address. Empty string if not present |  |
| `parsed_pmb_designator` | yes | string | Information if a Private Mail Box (PMB) is found in an address. Empty string if not present |  |
| `parsed_pmb_number` | yes | string | Information if a Private Mail Box (PMB) is found in an address. Empty string if not present |  |
| `parsed_post_directional` | yes | string | Notation following the street name indicating street direction. Empty string if not present |  |
| `parsed_pre_directional` | yes | string | Notation preceding the street name indicating street direction. Empty string if not present |  |
| `parsed_primary_number` | yes | string | Number preceding the street name. Empty string if not present |  |
| `parsed_street_name` | yes | string | Street name. Empty string if not present |  |
| `parsed_suffix` | yes | string | Part of the delivery address line following the street name. Empty string if not present |  |
| `parsed_unit_designator` | yes | string | Identification of the secondary address unit. Empty string if not present |  |
| `parsed_unit_number` | yes | string | Apartment or suite number. Empty string if not present |  |
| `rdi` | yes | string | Residential Delivery Indicator (RDI). Indicates whether USPS classifies the delivery point as residential. Empty string if not present |  |
| `record_type` | yes | string | Type of address record. |  |
| `state` | yes | string | Standard two-letter state abbreviation |  |
| `suite_link_footnote` | yes | `""` \| `00` \| `A` | Results of the SuiteLink lookup. |  |
| `time_zone` | yes | string | Time zone. Empty string if not present |  |
| `urbanization` | yes | string | Urban name required in the address of all mail being delivered to Puerto Rico. Empty string if not present |  |
| `zip_code` | yes | string | 5-digit ZIP Code and the four additional digits |  |

## Example

```json
{
  "address1": "1010 Cauthen Ln",
  "address2": "",
  "address3": "",
  "area_code": "575",
  "carrier_route": "C019",
  "check_digit": "4",
  "city": "Alamogordo",
  "city_abbreviation": "",
  "congressional_district": "02",
  "country_code": "US",
  "county": "Otero",
  "day_light_savings": true,
  "delivery_point": "10",
  "dpv": "Y",
  "dpv_cmra": "N",
  "dpv_footnotes": "AABB",
  "dpv_no_stat": "N",
  "dpv_vacant": "N",
  "elot": "0133A",
  "finance_number": "340105",
  "fips_county_code": "035",
  "firm": "",
  "footnotes": "M0>",
  "geo_coded": true,
  "lacs_indicator": "",
  "lacs_link_footnote": "",
  "lacs_link_indicator": "",
  "latitude": "32.91278",
  "longitude": "-105.94904",
  "parsed_pmb_designator": "",
  "parsed_pmb_number": "",
  "parsed_post_directional": "",
  "parsed_pre_directional": "",
  "parsed_primary_number": "1010",
  "parsed_street_name": "Cauthen",
  "parsed_suffix": "Ln",
  "parsed_unit_designator": "",
  "parsed_unit_number": "",
  "rdi": "Y",
  "record_type": "S",
  "state": "NM",
  "suite_link_footnote": "",
  "time_zone": "MST",
  "urbanization": "",
  "zip_code": "88310-5631"
}
```
