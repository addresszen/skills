# Ireland ECAF Address

ECAF is the Eircode Address File, which holds one record per Irish postal address. English and Irish language versions of each address are indexed separately and distinguished by `language`.

Unavailable elements are returned as an empty string, never `null`. ECAF carries no coordinates, so `longitude` and `latitude` are always empty strings - use `EcadAddress` for geolocated Irish addresses.

**Schema name:** `EcafAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | `ecaf` | Source of address |  |
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
| `ecaf_id` | yes | string | The unique identifier in the ECAF is the `ecaf_id`. This unique identifier allows each address in the ECAF to be uniquely identified. It can also be used as index once the data has been imported into a relational database. This is a numeric field that can store values from 0 to 2,147,483,647. It is represented as a number up to 10 digits long. All other fields in ECAF are alphanumeric. |  |

## Example

```json
{
  "id": "ecaf_1700000000|en",
  "dataset": "ecaf",
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
  "ecaf_id": "1700000000",
  "department": "",
  "organisation": "",
  "sub_building_name": "Apartment 4",
  "building_name": "",
  "building_number": "",
  "building_group": "The Mall",
  "primary_thoroughfare": "Riverside Way",
  "secondary_thoroughfare": "",
  "primary_locality": "Midleton",
  "secondary_locality": "",
  "tertiary_locality": "",
  "post_county": "Cork",
  "eircode": "P25 PR28",
  "address_reference": "4065432740654331",
  "longitude": "",
  "latitude": ""
}
```
