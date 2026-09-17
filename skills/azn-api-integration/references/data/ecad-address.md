# Ireland ECAD Address

ECAD is the Eircode Address Database. It carries every ECAF postal address element plus GeoDirectory identifiers, building and organisation attributes, administrative area references and An Post sorting information. English and Irish language versions of each address are indexed separately and distinguished by `language`.

Unavailable elements are returned as an empty string, never `null`.

**Schema name:** `EcadAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | `ecad` | Source of address |  |
| `country_iso` | yes | `IRL` | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | `IE` | 2 letter country code (ISO 3166-1) |  |
| `country` | yes | `Ireland` | Full country names (ISO 3166) |  |
| `language` | yes | `en` \| `ga` | Language represented by 2 letter ISO Code (639-1) |  |
| `line_1` | yes | string | Address Line 1 |  |
| `line_2` | yes | string | Address Line 2 |  |
| `line_3` | yes | string | Address Line 3 |  |
| `line_4` | yes | string | Address Line 4 |  |
| `line_5` | yes | string | Address Line 5 |  |
| `line_6` | yes | string | Address Line 6 |  |
| `line_7` | yes | string | Address Line 7 |  |
| `line_8` | yes | string | Address Line 8 |  |
| `line_9` | yes | string | Address Line 9 |  |
| `department` | yes | string | The department or division within an organisation, e.g. `Accounts Department`. If the department element exists, then the organisation must also exist. |  |
| `organisation` | yes | string | Organisation name, e.g. `Oak Tree Limited`. |  |
| `sub_building_name` | yes | string | The sub-building refers to an apartment, flat or unit within a building, e.g. `Flat 1`. |  |
| `building_name` | yes | string | The name given to the building, e.g. `Rose Cottage`. Prepended by sub building, if any, when the sub building does not appear on a line to itself. The building name is omitted if it is the same as either the Organisation or Building Group. |  |
| `building_number` | yes | string | A number associated with the whole building. The building number may have a numeric and an alphanumeric component, which are concatenated e.g. 2A, or alternatively will have a simple building number or a complex building number. The building number always relates to the whole building and not a sub-unit within it. |  |
| `building_group` | yes | string | A building group is a collection of buildings with a collective name, located on or near the same thoroughfare, e.g. `Marrian Terrace`. |  |
| `primary_thoroughfare` | yes | string | The name of the thoroughfare on which premises are located, e.g. `Griffith Road`. It may appear on a line by itself or be appended to either a sub building or building number. |  |
| `secondary_thoroughfare` | yes | string | It is never present without a primary thoroughfare. The primary thoroughfare is dependent on the secondary thoroughfare and appears before the secondary thoroughfare in any address. |  |
| `primary_locality` | yes | string | First locality elements which can refer to areas, districts, industrial estates, towns, etc. |  |
| `secondary_locality` | yes | string | Never present without a primary locality. The secondary locality has a wider geographic scope than the primary locality. |  |
| `tertiary_locality` | yes | string | Also known as the Post Town. |  |
| `post_county` | yes | string | One of the 26 Counties in the Republic of Ireland. These counties are sub-national divisions used for the purposes of administrative, geographical and political demarcation. Post County is the County associated with the Post Town, not the geographic county in which the building is located. The Post County is normally used as part of the Postal Address with some exceptions e.g. Dublin Postal Districts where the Post County is not used and some Post Towns (e.g. Tipperary, Kildare, etc.) that have the same name as the Post County. |  |
| `eircode` | yes | string | The seven character Eircode has an A65 F4E2 format. The Eircode is a mandatory address element. The last line of a Postal Address will contain the Eircode, displayed with a space. e.g. `A65 F4E2`. |  |
| `address_reference` | yes | string | The address reference is the An Post GeoDirectory address reference identifier used by the Universal Service Provider. |  |
| `longitude` | yes | string \| number | The longitude of the address or postcode (WGS84). |  |
| `latitude` | yes | string \| number | The latitude of the address or postcode (WGS84). |  |
| `ecad_id` | yes | string | Unique ECAD identifier for the postal address. Up to 10 digits. |  |
| `organisation_id` | yes | string | GeoDirectory identifier for the organisation. Empty string if the address has no organisation. |  |
| `address_point_id` | yes | string | GeoDirectory identifier for the address point. |  |
| `building_id` | yes | string | GeoDirectory identifier for the building. |  |
| `building_group_id` | yes | string | GeoDirectory identifier for the building group. Empty string if the address has no building group. |  |
| `primary_thoroughfare_id` | yes | string | GeoDirectory identifier for the primary thoroughfare. |  |
| `secondary_thoroughfare_id` | yes | string | GeoDirectory identifier for the secondary thoroughfare. Empty string if the address has no secondary thoroughfare. |  |
| `primary_locality_id` | yes | string | GeoDirectory identifier for the primary locality. Empty string if the address has no primary locality. |  |
| `secondary_locality_id` | yes | string | GeoDirectory identifier for the secondary locality. Empty string if the address has no secondary locality. |  |
| `post_town` | yes | string | The name of the post town associated with the premises for postal delivery purposes. Returned in the language given by `language`, and mirrors `tertiary_locality` for this dataset. |  |
| `post_town_id` | yes | string | GeoDirectory identifier for the post town. |  |
| `post_county_id` | yes | string | GeoDirectory identifier for the post county. Empty string if the address has no post county. |  |
| `nua` | yes | boolean | NUA means "non-unique address". |  |
| `gaeltacht` | yes | boolean | Gaeltacht refers to a district where the Irish government recognises that the Irish language is the predominant language. |  |
| `address_type` | yes | string | Addresses points can assume one of the following values: |  |
| `building_address_type` | yes | string | The building type can assume one of the following values: |  |
| `building_group_address_type` | yes | string | The building group type can be: |  |
| `primary_locality_address_type` | yes | string | The locality type can be: |  |
| `secondary_locality_address_type` | yes | string | The locality type can be: |  |
| `building_type` | yes | string | Describes the type of building, e.g. detached, semi-detached, bungalow. |  |
| `holiday_home` | yes | `Y` \| `N` \| `""` | A Yes/No field, indicating whether or not the building is a holiday home. Empty string if unknown. |  |
| `under_construction` | yes | `Y` \| `N` \| `""` | A Yes/No field, indicating whether or not the building is under construction. Empty string if unknown. |  |
| `building_use` | yes | `R` \| `C` \| `B` \| `U` \| `""` | Can be one of: |  |
| `vacant` | yes | `Y` \| `N` \| `""` | A Yes/No field, indicating whether the building is vacant. Empty string if unknown. |  |
| `org_vacant` | yes | `Y` \| `N` \| `""` | A Yes/No field, indicating whether the organisation is vacant. Empty string if unknown or the address has no organisation. |  |
| `nace_code` | yes | string | The NACE Code for the Category. |  |
| `nace_category` | yes | string | Name of the NACE Category |  |
| `local_authority` | yes | string | Name of local authority |  |
| `ded_id` | yes | string | Unique Identifier for the Electoral Division, from the 2017 data. |  |
| `small_area_id` | yes | string | Unique Identifier for the Small Area, from the 2017 data. |  |
| `townland_id` | yes | string | Unique Identifier for the townland, from the 2017 data. |  |
| `gaeltacht_id` | yes | string | Unique Identifier for the Gaeltacht area, from the 2017 data. There are 7 Gaeltacht areas. Empty string if the address is not in a Gaeltacht. |  |
| `postaim_presort_61` | yes | string | An Post sorting information. |  |
| `postaim_presort_152` | yes | string | An Post sorting information. |  |
| `publicity_post_zone` | yes | string | An Post publicity post zone information. |  |

## Example

```json
{
  "id": "ecad_1700000000|en",
  "dataset": "ecad",
  "ecad_id": "1700000000",
  "country_iso": "IRL",
  "country_iso_2": "IE",
  "country": "Ireland",
  "language": "en",
  "line_1": "Apartment 4",
  "line_2": "The Mall",
  "line_3": "Riverside Way",
  "line_4": "Midleton",
  "line_5": "Co. Cork",
  "line_6": "P25 PR28",
  "line_7": "",
  "line_8": "",
  "line_9": "",
  "department": "",
  "organisation": "",
  "sub_building_name": "Apartment 4",
  "building_name": "",
  "building_number": "",
  "building_group": "The Mall",
  "primary_thoroughfare": "Riverside Way",
  "secondary_thoroughfare": "",
  "primary_locality": "",
  "secondary_locality": "",
  "tertiary_locality": "Midleton",
  "post_county": "Cork",
  "eircode": "P25 PR28",
  "address_reference": "4065432740654331",
  "organisation_id": "",
  "address_point_id": "1700000000",
  "building_id": "1401909875",
  "building_group_id": "1300011097",
  "primary_thoroughfare_id": "1200004534",
  "secondary_thoroughfare_id": "",
  "primary_locality_id": "",
  "secondary_locality_id": "",
  "post_town": "Midleton",
  "post_town_id": "1100000075",
  "post_county_id": "1001000000",
  "nua": false,
  "gaeltacht": false,
  "address_type": "Residential Address Point",
  "building_address_type": "Multi Occupancy Mixed Building",
  "building_group_address_type": "Apartment Complex",
  "primary_locality_address_type": "",
  "secondary_locality_address_type": "",
  "building_type": "Semi-Detached",
  "holiday_home": "N",
  "under_construction": "N",
  "building_use": "B",
  "vacant": "N",
  "org_vacant": "",
  "nace_code": "",
  "nace_category": "",
  "local_authority": "",
  "ded_id": "",
  "small_area_id": "",
  "townland_id": "",
  "gaeltacht_id": "",
  "postaim_presort_61": "Portlaoise Hub",
  "postaim_presort_152": "Midleton",
  "publicity_post_zone": "19",
  "longitude": "",
  "latitude": ""
}
```
