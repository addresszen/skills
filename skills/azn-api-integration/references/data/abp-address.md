# AddressBase Premium

Address from Ordnance Survey AddressBase Premium dataset.

Please contact us to have this enabled on your account.

All AddressBase Premium addresses have a UPRN and a rooftop geolocation available however they may not have a UDPRN.

**Schema name:** `AbpAddress`

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
| `native` | yes | object | A flat, consolidated row from the `abp.addresses` materialised view of | `{"uprn":"49020496","parent_uprn":"49020495","logical_status":1,"blpu_state":"2","blpu_state_date":"2011-10-06T00:00:00.000Z","country":"W","latitude":52.4121999,"longitude":-4.0883772,"x_coordinate":258053.87,"y_coordinate":281405.95,"rpc":2,"local_custodian_code":6820,"addressbase_postal":"D","postcode_locator":"SY23 1JT","multi_occ_count":4,"blpu_start_date":"2007-10-24T00:00:00.000Z","blpu_end_date":null,"blpu_last_update_date":"2025-10-13T00:00:00.000Z","blpu_entry_date":"2006-11-24T00:00:00.000Z","udprn":"24255522","organisation_name":null,"legal_name":null,"department_name":null,"sub_building_name":null,"building_name":null,"building_number":1,"dependent_thoroughfare":"CASTLE TERRACE","thoroughfare":"SOUTH ROAD","double_dependent_locality":null,"dependent_locality":null,"post_town":"ABERYSTWYTH","postcode":"SY23 1JT","postcode_type":"S","delivery_point_suffix":"1A","po_box_number":null,"welsh_dependent_thoroughfare":"HEOL Y CASTELL","welsh_thoroughfare":"TAN Y CAE","welsh_double_dependent_locality":null,"welsh_dependent_locality":null,"welsh_post_town":"ABERYSTWYTH","dpa_process_date":"2016-01-18T00:00:00.000Z","dpa_start_date":"2012-04-23T00:00:00.000Z","dpa_end_date":null,"dpa_last_update_date":"2016-02-10T00:00:00.000Z","dpa_entry_date":"2012-03-19T00:00:00.000Z","classification_code":"RD04","class_scheme":"AddressBase Premium Classification Scheme","scheme_version":1,"classification_start_date":"2007-10-24T00:00:00.000Z","classification_end_date":null,"classification_last_update_date":"2018-09-23T00:00:00.000Z","classification_entry_date":"2006-11-24T00:00:00.000Z","organisation_start_date":null,"organisation_end_date":null,"organisation_last_update_date":null,"organisation_entry_date":null,"lpi_key":"6820L000054880","lpi_language":"CYM","lpi_logical_status":1,"lpi_start_date":"2007-10-24T00:00:00.000Z","lpi_end_date":null,"lpi_last_update_date":"2025-09-26T00:00:00.000Z","lpi_entry_date":"2007-09-04T00:00:00.000Z","sao_start_number":null,"sao_start_suffix":null,"sao_end_number":null,"sao_end_suffix":null,"sao_text":null,"pao_start_number":1,"pao_start_suffix":null,"pao_end_number":null,"pao_end_suffix":null,"pao_text":"HEOL Y CASTELL","usrn":"47114724","usrn_match_indicator":"1","area_name":null,"level":null,"official_flag":"Y","street_record_type":1,"swa_org_ref_naming":6820,"street_state":"2","street_state_date":"1990-01-01T00:00:00.000Z","street_surface":"1","street_classification":null,"street_start_date":"2007-10-24T00:00:00.000Z","street_last_update_date":"2022-01-14T00:00:00.000Z","street_record_entry_date":"1998-07-14T00:00:00.000Z","street_start_x":257968,"street_start_y":281400,"street_start_lat":52.4121241,"street_start_long":-4.0896363,"street_end_x":258266,"street_end_y":281393,"street_end_lat":52.4121386,"street_end_long":-4.0852551,"street_tolerance":10,"street_description":"SOUTH ROAD","street_locality":null,"street_town":"ABERYSTWYTH","adminstrative_area":"CEREDIGION","sd_language":"ENG","sd_start_date":"2007-10-24T00:00:00.000Z","sd_end_date":null,"sd_last_update_date":"2016-02-06T00:00:00.000Z","sd_entry_date":"1998-07-14T00:00:00.000Z","toid":"osgb1000020592167","toid_address":"osgb1000002175099422","toid_highways":"osgb5000005181786114","council_tax_ref":null,"ndr_ref":null,"ons_ward_code":"W05001302","ons_parish_code":"W04000359"}` |

## Used By

- [Postcodes](../endpoints/postcodes.md)
- [ResolveAddress](../endpoints/resolve-address.md)
