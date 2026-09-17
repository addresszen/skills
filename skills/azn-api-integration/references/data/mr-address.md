# Multiple Residence Address

Raw Royal Mail Multiple Residence record backing an `mr` address.

Multiple Residence holds sub-premises (flats, rooms) that share a parent PAF delivery point. `umprn` keys the residence, `udprn` the parent delivery point. The record has no `po_box`.

**Schema name:** `MrAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `dataset` | yes | `mr` | Dataset the record belongs to. The only field not taken from the Royal Mail record |  |
| `postcode` | yes | string | Postcode, space separated |  |
| `post_town` | yes | string | Royal Mail post town, title cased |  |
| `dependant_locality` | yes | string | Dependant locality. Empty string when not present |  |
| `double_dependant_locality` | yes | string | Double dependant locality. Empty string when not present |  |
| `thoroughfare` | yes | string | Street name |  |
| `dependant_thoroughfare` | yes | string | Dependant street name. Empty string when not present |  |
| `building_number` | yes | string | Building number. Empty string when not present, or when PAF merges it into the building name |  |
| `building_name` | yes | string | Building name. Empty string when not present |  |
| `sub_building_name` | yes | string | Sub building name. Empty string when not present |  |
| `department_name` | yes | string | Department name within an organisation. Empty string when not present |  |
| `organisation_name` | yes | string | Organisation name. Empty string when not present |  |
| `udprn` | yes | integer | Unique Delivery Point Reference Number |  |
| `postcode_type` | yes | `S` \| `L` \| `""` | Postcode type. |  |
| `su_organisation_indicator` | yes | string | Small user organisation indicator. `Y` where the small user postcode is held by an organisation |  |
| `delivery_point_suffix` | yes | string | Royal Mail delivery point suffix |  |
| `umprn` | yes | integer | Unique Multiple Residence Reference Number |  |

## Example

```json
{
  "dataset": "mr",
  "postcode": "SW1A 2AA",
  "post_town": "London",
  "dependant_locality": "",
  "double_dependant_locality": "",
  "thoroughfare": "Downing Street",
  "dependant_thoroughfare": "",
  "building_number": "10",
  "building_name": "",
  "sub_building_name": "Flat 1",
  "department_name": "",
  "organisation_name": "",
  "udprn": 23747771,
  "postcode_type": "S",
  "su_organisation_indicator": "",
  "delivery_point_suffix": "1A",
  "umprn": 50906058
}
```
