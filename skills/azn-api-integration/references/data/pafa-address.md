# PAF Alias Address

The Royal Mail PAF record backing a `pafa` address, with the alias applied. Alias data holds alternative address details the public uses when addressing mail, which are not required for delivery.

This is the parent delivery point, not the alias row: the alias text replaces the building name, organisation name or department name, so those three fields carry the alias and the rest is the parent PAF record. The alias row's own columns (`alias_text`, `category`, `currency`) are not yet returned. `id` is the parent UDPRN plus a hash of the alias text, since a delivery point can carry several aliases.

**Schema name:** `PafaAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `dataset` | yes | `pafa` | Dataset the record belongs to. The only field not taken from the Royal Mail record |  |
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
  "dataset": "pafa",
  "postcode": "SW1A 1AA",
  "post_town": "London",
  "dependant_locality": "",
  "double_dependant_locality": "",
  "thoroughfare": "The Mall",
  "dependant_thoroughfare": "",
  "building_number": "1",
  "building_name": "The Old Post Office",
  "sub_building_name": "",
  "po_box": "",
  "department_name": "",
  "organisation_name": "",
  "udprn": 90000001,
  "postcode_type": "S",
  "su_organisation_indicator": "",
  "delivery_point_suffix": "1A"
}
```
