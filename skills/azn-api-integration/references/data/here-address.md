# HERE Address

An address from HERE Technologies' map data, covering 230 countries and territories across twelve regional datasets named in `dataset`. Each address carries its address lines, house number (`address`), street name, HERE's administrative hierarchy (`order1_name`, `order2_name`, `order8_name`, `builtup_name`), a postal code where the country has one, display and delivery coordinates and, where HERE holds them, the building, unit, level and unit name. Depth varies by country, from building level down to region level only. HERE refreshes the data quarterly.

Conventions:

- A record is one of four kinds, named after the dataset in `id`: `ap` an address point, `ar` an address range, `poi` a point of interest, `loc` a locality. Postal Addressing records are `pap` and `par`.
- `id` is the dataset, the kind, HERE's key and the language code. A range id carries a further segment holding the interpolated house number (`herewe_ar|74024700!27769096|8|de`).
- Text fields are empty strings, never null. Coordinates are empty strings when absent.
- Only `line_1` and `line_2` are ever populated. `line_1` is the building name line where the record has one, otherwise the street line. Ranges, points of interest and localities produce at most one line.
- Casing is as HERE ships it. Only the Postal Addressing fields are title cased.
- `language` is the ISO 639-1 code for the record. A street named in more than one language yields one record per language, identical but for the language segment of `id`.

**Schema name:** `HereAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `country_iso` | yes | string | Three character country code based on ISO Standard 3166. |  |
| `dataset` | yes | string | HERE regional dataset the address was sourced from. |  |
| `language` | yes | string | ISO 639-1 language code of the record, mapped down from HERE's three-letter code. Taken from the address point, the road for a range, the point of interest or the administrative place for a locality. |  |
| `line_1` | yes | string | First address line. |  |
| `line_2` | yes | string | Second address line. |  |
| `line_3` | yes | string | Third address line. Always the empty string `""` for HERE records, which produce at most two lines. |  |
| `line_4` | yes | string | Fourth address line. Always the empty string `""` for HERE records, which produce at most two lines. |  |
| `line_5` | yes | string | Fifth address line. Always the empty string `""` for HERE records, which produce at most two lines. |  |
| `address` | yes | string | Address / House Number uniquely identifying the address along the specified road link. |  |
| `delivery_latitude` | yes | string \| number |  |  |
| `delivery_longitude` | yes | string \| number |  |  |
| `building_name` | yes | string | Name of the Building to which the Point Address is associated. |  |
| `latitude` | yes | string \| number |  |  |
| `longitude` | yes | string \| number |  |  |
| `street_name` | yes | string | The full spelling of the street name, including Prefix, Base Name, Suffix, Street Type, and Direction on Sign. |  |
| `postal_code` | yes | string | Full postal code; could be numeric or alphanumeric postal code. |  |
| `order1_name` | yes | string | Identifies the highest administrative level in which a country can be subdivided. |  |
| `order2_name` | yes | string | Identifies an intermediate administrative level of a country and is a sub-division of an Order-1 area. Only countries with a five (or more) level administrative hierarchy have Order-2 administrative levels defined. This feature can be used for destination selection and map display. |  |
| `order8_name` | yes | string | Identifies the lowest level of the country's administrative hierarchy that is present country-wide. (No gaps exist in the coverage.) |  |
| `builtup_name` | yes | string | Identifies the lowest administrative level for a country. This level does not cover the entire country, (as opposed to the Order-8 Area level which does cover the entire country). This feature should be used in conjunction with Zone and Order-8 Area for destination selection. The Built-up Area polygon, as published in RDF_CARTO, can also be used for map display. |  |
| `poi_name` | yes | string | Name of the point of interest. Populated for point of interest records only. |  |
| `building_unit_name` | yes | string | Name of the Building associated with a Micro Point Address. |  |
| `level_name` | yes | string | Name of floor or level within a building associated with a Micro Point Address. |  |
| `unit_name` | yes | string | Name of the unit (suite, etc) associated with a Micro Point Address. |  |
| `suppl_address_info` | yes | string | Additional address or building information. |  |
| `building_grp_name` | yes | string | Name of the group of buildings with which the address is associated. |  |

## Example

```json
{
  "id": "herewe_ap|365553439|it",
  "dataset": "herewe",
  "country_iso": "ITA",
  "line_1": "16 Via Giuseppe Garibaldi",
  "line_2": "",
  "line_3": "",
  "line_4": "",
  "line_5": "",
  "language": "it",
  "address": "16",
  "building_name": "",
  "delivery_latitude": 45.28441,
  "delivery_longitude": 12.00825,
  "latitude": 45.28441,
  "longitude": 12.00825,
  "street_name": "Via Giuseppe Garibaldi",
  "postal_code": "35020",
  "order1_name": "Veneto",
  "order2_name": "Padova",
  "order8_name": "Brugine",
  "builtup_name": "",
  "poi_name": "",
  "building_unit_name": "",
  "level_name": "",
  "unit_name": "",
  "suppl_address_info": "",
  "building_grp_name": ""
}
```
