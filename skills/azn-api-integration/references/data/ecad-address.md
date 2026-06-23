# Ireland ECAD Address

The ECAD contains additional data for each ECAF address.

**Schema name:** `EcadAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address | `paf_8387729` |
| `dataset` | yes | string | Source of address |  |
| `country_iso` | yes |  | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | string | 2 letter country code (ISO 3166-1) |  |
| `country` | yes | string | Full country names (ISO 3166) |  |
| `language` | yes |  | Language represented by 2 letter ISO Code (639-1) |  |
| `line_1` | yes | string | Address Line 1 |  |
| `line_2` | yes | string | Address Line 2 |  |
| `line_3` | yes | string | Address Line 3 |  |
| `line_4` | yes | string | Address Line 4 |  |
| `line_5` | yes | string | Address Line 5 |  |
| `line_6` | yes | string | Address Line 6 |  |
| `line_7` | yes | string | Address Line 7 |  |
| `line_8` | yes | string | Address Line 8 |  |
| `line_9` | yes | string | Address Line 9 |  |
| `department` | yes | string | The department or division within an organisation. If the department element exists, then the organisation must also exist. | `Accounts Department` |
| `organisation` | yes | string | Organisation name | `Oak Tree Limited` |
| `sub_building_name` | yes | string | The sub-building refers to an apartment, flat or unit within a building. | `Flat 1` |
| `building_name` | yes | string | The name given to the building. Prepended by sub building, if any, when the sub building does not appear on a line to itself. The building name is omitted if it is the same as either the Organisation or Building Group. | `Rose Cottage` |
| `building_number` | yes | string | A number associated with the whole building. The building number may have a numeric and an alphanumeric component, which are concatenated e.g. 2A, or alternatively will have a simple building number or a complex building number. The building number always relates to the whole building and not a sub-unit within it. | `22` |
| `building_group` | yes | string | A building group is a collection of buildings with a collective name, located on or near the same thoroughfare. | `Marrian Terrace` |
| `primary_thoroughfare` | yes | string | The name of the thoroughfare on which premises are located. It may appear on a line by itself or be appended to either a sub building or building number. | `Griffith Road` |
| `secondary_thoroughfare` | yes | string | It is never present without a primary thoroughfare. The primary thoroughfare is dependent on the secondary thoroughfare and appears before the secondary thoroughfare in any address. | `Navan Road` |
| `primary_locality` | yes | string | First locality elements which can refer to areas, districts, industrial estates, towns, etc. | `Cookstown Industrial Estate` |
| `secondary_locality` | yes | string | Never present without a primary locality. The secondary locality has a wider geographic scope than the primary locality. | `Manorhamilton` |
| `tertiary_locality` | yes | string | Also known as the Post Town. | `Dublin 14` |
| `post_county` | yes | string | One of the 26 Counties in the Republic of Ireland. These counties are sub-national divisions used for the purposes of administrative, geographical and political demarcation. Post County is the County associated with the Post Town, not the geographic county in which the building is located. The Post County is normally used as part of the Postal Address with some exceptions e.g. Dublin Postal Districts where the Post County is not used and some Post Towns (e.g. Tipperary, Kildare, etc.) that have the same name as the Post County. | `Cork` |
| `eircode` | yes | string | The seven character Eircode has an A65 F4E2 format. The Eircode is a mandatory address element. The last line of a Postal Address will contain the Eircode, displayed with a space. e.g. `A65 F4E2`. | `A65 R2AF` |
| `address_reference` | yes | string | The address reference is the An Post GeoDirectory address reference identifier used by the Universal Service Provider. |  |
| `longitude` | yes |  | The longitude of the postcode (WGS84/ETRS89). |  |
| `latitude` | yes |  | The latitude of the postcode (WGS84/ETRS89). |  |
| `ecad_id` | no | string | Unique 10 digit ECAD ID | `17000000` |
| `organisation_id` | yes | string | Organisation ID | `10098783` |
| `address_point_id` | yes | string | Address Point ID | `10098783` |
| `building_id` | yes | string | Building ID | `10098783` |
| `building_group_id` | yes | string | Building Group ID | `10098783` |
| `primary_thoroughfare_id` | yes | string | Primary Thoroughfare ID | `10098783` |
| `secondary_thoroughfare_id` | yes | string | Secondary Thoroughfare ID | `10098783` |
| `primary_locality_id` | yes | string | Primary Locality ID | `10098783` |
| `secondary_locality_id` | yes | string | Secondary Locality ID | `10098783` |
| `post_town` | yes | string | The post town is a significant element of the Postal Address, however it is not always populated in an address. The official post office guide, Eolaí an Phoist1, describes post towns in the following manner: |  |
| `post_town_id` | yes | string | Post Town ID | `10098783` |
| `post_county_id` | yes | string | Post County ID | `10098783` |
| `nua` | yes | boolean | NUA means "non-unique address". |  |
| `gaeltacht` | yes | boolean | Gaeltact refers to a district where the Irish government recognises that the Irish language is the predominant language. |  |
| `address_type` | yes | string | Addresses points can assume one of the following values: |  |
| `building_address_type` | yes | string | The building type can assume one of the following values: |  |
| `building_group_address_type` | yes | string | The building group type can be: |  |
| `primary_locality_address_type` | yes | string | The locality type can be: |  |
| `secondary_locality_address_type` | yes | string | The locality type can be: |  |
| `building_type` | yes | string | Describes the type of building, e.g. detached, semi-detached, bungalow. |  |
| `holiday_home` | yes |  | A Yes/No field, indicating whether or not the building is a holiday home. |  |
| `under_construction` | yes |  | A Yes/No field, indicating whether or not the building is under construction. |  |
| `building_use` | yes |  | Can be one of: |  |
| `vacant` | yes |  | A Yes/No field, indicating whether the building is vacant. |  |
| `org_vacant` | yes |  | A Yes/No field, indicating whether the organisation is vacant. |  |
| `nace_code` | yes | string | The NACE Code for the Category. |  |
| `nace_category` | yes | string | Name of the NACE Category |  |
| `local_authority` | yes | string | Name of local authority |  |
| `ded_id` | yes | string | Unique Identifier for Electoral Divisions 2017 data. |  |
| `small_area_id` | yes | string | Unique Identifier for the Small Area 2017 data. |  |
| `townland_id` | yes | string | Unique Identifier for townland 2017 data. |  |
| `gaeltacht_id` | yes | string | Unique Identifier for the 7 Gaeltacht areas 2017 data. |  |
| `postaim_presort_61` | yes | string | An Post sorting information. |  |
| `postaim_presort_152` | yes | string | An Post sorting information. |  |
| `publicity_post_zone` | yes | string | An Post publicity post zone information. |  |
