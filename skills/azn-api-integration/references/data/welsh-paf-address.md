# Welsh PAF Address

Welsh language alternative for a PAF Address

**Schema name:** `WelshPafAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address | `paf_8387729` |
| `dataset` | yes | string | Indicates the provenance of an address |  |
| `country_iso` | yes | string | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | string | 2 letter country code (ISO 3166-1) |  |
| `country` | yes | string | Full country names (ISO 3166) | `England` |
| `language` | yes | string | Language represented by 2 letter ISO Code (639-1) |  |
| `line_1` | yes | string | First Address Line. Often contains premise and thoroughfare information. In the case of a commercial premise, the first line is always the full name of the registered organisation. Never empty. | `Prime Minister &amp; First Lord of Treasury` |
| `line_2` | yes | string | Second Address Line. Often contains thoroughfare and locality information. May be empty | `10 Downing Street` |
| `line_3` | yes | string | Third address line. May be empty. | `` |
| `post_town` | yes | string | **Filter by Town or City" | `London` |
| `postcode` | yes | string | Correctly formatted postcode. Capitalised and spaced. | `SW1A 2AA` |
| `county` | yes | string | Since postal, administrative or traditional counties may not apply to some addresses, the county field is designed to return whatever county data is available. Normally, the postal county is returned. If this is not present, the county field will fall back to the administrative county. If the administrative county is also not present, the county field will fall back to the traditional county. May be empty in cases where no administrative, postal or traditional county present. | `London` |
| `county_code` | yes | string | Short code representing the county or province. May be empty (`""`) | `` |
| `uprn` | yes | string | UPRN stands for Unique Property Reference Number and is maintained by the Ordnance Survey (OS). Local governments in the UK have allocated a unique number for each land or property. |  |
| `udprn` | yes | integer | UDPRN stands for ‘Unique Delivery Point Reference Number’. Royal Mail assigns a unique UDPRN code for each premise on PAF. Simple, unique reference number for each Delivery Point. Unlikely to be reused when an address expires. | `23747771` |
| `umprn` | yes |  | A small minority of individual premises (as identified by a UDPRN) may have multiple occupants behind the same letterbox. These are known as Multiple Residence occupants and can be queried via the Multiple Residence dataset. Simple, unique reference number for each Multiple Residence occupant. |  |
| `postcode_outward` | yes | string | The first part of a postcode is known as the outward code. e.g. The outward code of ID1 1QD is ID1. Enables mail to be sorted to the correct local area for delivery. This part of the code contains the area and the district to which the mail is to be delivered, e.g. ‘PO1’, ‘SW1A’ or ‘B23’. | `SW1A` |
| `postcode_inward` | yes | string | The second part of a postcode is known as the inward code. e.g. The inward code of ID1 1QD is 1QD. | `2AA` |
| `dependant_locality` | yes | string | When the same thoroughfare name reoccurs in a Post town, it may not be possible to make it dependant on a dependant thoroughfare. In this case the thoroughfare is dependant on a locality. For example if we want to find 1 Back Lane in Huddersfield we see that there are three. | `` |
| `double_dependant_locality` | yes | string | Used to supplement Dependant Locality. A Double Dependant Locality supplied along with a Dependant Locality if the Dependant Locality exists twice in the same locality. | `` |
| `thoroughfare` | yes | string | Also known as the street or road name. In general each Thoroughfare Name will have a separate Postcode. Longer Thoroughfares with high number ranges often have multiple Postcodes covering the entire length of the road, with breaks at suitable points e.g. junctions or natural breaks in the road. | `Downing Street` |
| `dependant_thoroughfare` | yes | string | Used to supplement thoroughfare. When a thoroughfare name is used twice in the same Post Town, the dependant thoroughfare is added to uniquely indentify a delivery point. | `` |
| `building_number` | yes | string | Number to identify premise on a thoroughfare or dependant thoroughfare. | `10` |
| `building_name` | yes | string | Name of residential or commercial premise. | `` |
| `sub_building_name` | yes | string | When a premise is split into individual units such as flats, apartments or business units. Cannot be present without either building_name or building_number. E.g. Flat 1, A, 10B | `Flat 1` |
| `po_box` | yes | string | When the PO Box Number field is populated it will contain PO BOX nnnnnn where n represents the PO Box number. Note that the PO Box details can occasionally consist of a combination of numbers and letters. PO Box Numbers are only allocated to Large Users. | `100` |
| `department_name` | yes | string | Used to supplement Organisation Name to identify a department within the organisation. | `` |
| `organisation_name` | yes | string | Name of the business or organisation receiving mail at this delivery point | `Prime Minister &amp; First Lord Of The Treasury` |
| `postcode_type` | yes |  | This indicates the type of user. It can only take the values 'S' or 'L' indicating small or large respectively. Large User Postcodes. These are assigned to one single address either due to the large volume of mail received at that address, or because a PO Box or Selectapost service has been set up. Small User Postcodes. These identify a group of Delivery Points. |  |
| `su_organisation_indicator` | yes | string | Small User Organisation Indicator can have the values 'Y' or space. A value of 'Y' indicates that a Small User Organisation is present at this address. | `Y` |
| `delivery_point_suffix` | yes | string | A unique Royal Mail 2-character code (the first numeric & the second alphabetical), which, when added to the Postcode, enables each live Delivery Point to be uniquely identified. Once the Delivery Point is deleted from PAF the DPS may be reused (although they aren’t reused until all remaining Delivery Points in the range have been allocated). The DPS for a Large User is always '1A' as each Large User has its own Postcode. | `1A` |
| `premise` | yes | string | A pre-computed string which sensibly combines building_number, building_name and sub_building_name. building_number, building_name and sub_building_name represent raw data from Royal Mail's and can be difficult to parse if you are unaware of how the Postcode Address File premise fields work together. For this reason, we also provide a pre-computed premise field which intelligently gathers these points into a single, simple premise string. This field is ideal if you want to pull premise information and thoroughfare information separately instead of using our address lines data. | `10` |
| `administrative_county` | yes | string | The current administrative county to which the postcode has been assigned. | `` |
| `postal_county` | yes | string | Postal counties were used for the distribution of mail before the Postcode system was introduced in the 1970s. The Former Postal County was the Administrative County at the time. This data rarely changes. May be empty. | `London` |
| `traditional_county` | yes | string | Traditional counties are provided by the Association of British Counties. It is historical data, and can date from the 1800s. May be empty. | `Greater London` |
| `district` | yes | string | The current district/unitary authority to which the postcode has been assigned. | `Westminster` |
| `ward` | yes | string | The current administrative/electoral area to which the postcode has been assigned. May be empty for a small number of addresses. | `St. James'` |
| `longitude` | yes |  | The longitude of the postcode (WGS84/ETRS89). |  |
| `latitude` | yes |  | The latitude of the postcode (WGS84/ETRS89). |  |
| `eastings` | yes |  | Eastings reference using the [Ordnance Survey National Grid reference system](https://en.wikipedia.org/wiki/Ordnance_Survey_National_Grid). |  |
| `northings` | yes |  | Northings reference using the [Ordnance Survey National Grid reference system](https://en.wikipedia.org/wiki/Ordnance_Survey_National_Grid) |  |

## Used By

- [Postcodes](../endpoints/postcodes.md)
- [ResolveAddress](../endpoints/resolve-address.md)
