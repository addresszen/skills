# Welsh PAF Address

Raw Royal Mail Welsh language record backing a `pafw` address.

Welsh alternatives for addresses in the sectors Royal Mail defines as part of the Welsh principality. Same shape as a PAF record, keyed on the same UDPRN.

**Schema name:** `PafwAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `dataset` | yes | `pafw` | Dataset the record belongs to. The only field not taken from the Royal Mail record |  |
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
| `po_box` | yes | string | PO Box number. Empty string when not present |  |

## Example

```json
{
  "dataset": "pafw",
  "postcode": "CF10 1EP",
  "post_town": "Caerdydd",
  "dependant_locality": "",
  "double_dependant_locality": "",
  "thoroughfare": "Heol Eglwys Fair",
  "dependant_thoroughfare": "",
  "building_number": "1",
  "building_name": "",
  "sub_building_name": "",
  "po_box": "",
  "department_name": "",
  "organisation_name": "",
  "udprn": 90000003,
  "postcode_type": "S",
  "su_organisation_indicator": "",
  "delivery_point_suffix": "1A"
}
```
