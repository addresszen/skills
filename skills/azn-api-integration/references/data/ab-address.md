# AddressBase Core Address

An address from Ordnance Survey's AddressBase Core, a flat cut of the approved addresses in Great Britain. Each record is one UPRN drawn from the local authority gazetteers: the National Land and Property Gazetteer for England and Wales, the One Scotland Address Gazetteer for Scotland. It carries the Royal Mail delivery point where one has been matched, property level coordinates, a classification (`classification_code`), the key identifiers (`uprn`, `parent_uprn`, `udprn`, `usrn`, `toid`), the contributing authority (`gss_code`), coordinate quality (`rpc`) and the change the latest supply applied (`change_code`). Ordnance Survey publishes around 35 million records and refreshes them weekly.

How it differs from the neighbouring datasets:

- **AddressBase Premium** (`abp`) is the full gazetteer: around 40 million UPRNs including historic and provisional records, the local authority address breakdown (`pao_*`, `sao_*`), lifecycle (`logical_status`, `blpu_state`), Welsh alternatives, the street record and cross references to the Valuation Office Agency and ONS, refreshed every six weeks. AddressBase Core carries none of these. Use it when one approved address per UPRN, with coordinates and a classification, is enough.
- **Royal Mail PAF** (`paf`) lists delivery points only, keyed by UDPRN. AddressBase Core keys on UPRN and also holds non-postal objects (substations, car parks, land parcels, parent shells) with no delivery point. On those records `udprn` is `0` and `delivery_point_suffix` is empty. Where a record matches PAF, `ab` renders the same `line_1` to `line_3` as `paf` for that UDPRN, bar a handful of records with a trailing range in the building name, which AddressBase Core keeps whole.
- The Ordnance Survey end of life notice for autumn 2027 covers AddressBase and AddressBase Plus, not AddressBase Core.

**Schema name:** `AbAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `country_iso` | yes | string | 3 letter country code (ISO 3166-1) |  |
| `dataset` | yes | `ab` | Indicates the provenance of an address |  |
| `language` | yes | string | Language represented by 2 letter ISO Code (639-1) |  |
| `line_1` | yes | string | First Address Line. Often contains premise and thoroughfare information. In the case of a commercial premise, the first line is always the full name of the registered organisation. Never empty. |  |
| `line_2` | yes | string | Second Address Line. Often contains thoroughfare and locality information. May be empty |  |
| `line_3` | yes | string | Third address line. Takes the address elements left after `line_1` and `line_2` are filled; where the address needs more than three lines the remaining elements are joined into `line_3`, comma separated. May be empty. |  |
| `premise` | yes | string | A pre-computed string which sensibly combines the building name, sub-building and building number fields into a single, simple premise string. Ideal if you want to pull premise information and thoroughfare information separately instead of using the address lines. |  |
| `uprn` | yes | string | Unique Property Reference Number (UPRN) assigned by the LLPG Custodian or Ordnance Survey. |  |
| `udprn` | yes | integer | Royal Mail's Unique Delivery Point Reference Number (UDPRN). `0` where the record has no matching PAF delivery point. |  |
| `parent_uprn` | yes | string | UPRN of the parent record where a parent-child relationship exists. Empty where the record has no parent. |  |
| `usrn` | yes | integer | Unique Street Reference Number assigned by the Street Name and Numbering Custodian or by Ordnance Survey, depending on the address record. |  |
| `toid` | yes | string | The Topographic Identifier taken from OS MasterMap Topography Layer. This TOID is assigned to the UPRN by performing a spatial intersection between the two identifiers. It consists of the letters 'osgb' followed by up to sixteen digits. May be empty. |  |
| `classification_code` | yes | string | A code that describes the classification of the address record to a maximum of a secondary level. The first letter is the primary class (e.g. `R` residential, `C` commercial, `L` land), the second the secondary class (e.g. `RD` dwelling). |  |
| `eastings` | yes | number | A value in metres defining the x location in accordance with the British National Grid. |  |
| `northings` | yes | number | A value in metres defining the y location in accordance with the British National Grid. |  |
| `latitude` | yes | number | A value defining the Latitude location in accordance with the ETRS89 coordinate reference system. |  |
| `longitude` | yes | number | A value defining the Longitude location in accordance with the ETRS89 coordinate reference system. |  |
| `single_address_line` | yes | string | A single attribute containing text concatenation of the address elements separated by a comma. |  |
| `street_name` | yes | string | Street / Road name for the address record. |  |
| `locality` | yes | string | A locality defines an area or geographical identifier within a town, village or hamlet. Locality represents the lower level geographical area. The locality field should be used in conjunction with the town name and street description fields to uniquely identify geographic area where there may be more than one within an administrative area. |  |
| `town_name` | yes | string | Geographical town name assigned by the Local Authority. Note this can differ from the post town assigned by Royal Mail. |  |
| `delivery_point_suffix` | yes | string | A two-character code uniquely identifying an individual delivery point within a postcode, assigned by Royal Mail. May be empty. |  |
| `post_town` | yes | string | The town or city in which the Royal Mail sorting office servicing this address record is located. |  |
| `gss_code` | yes | string | The Office for National Statistics Governmental Statistical Service (GSS) code representing the contributing Local Authority. |  |
| `rpc` | yes | integer | Representative Point Code describes the accuracy of the coordinate that has been allocated to the UPRN as indicated by the Local Authority and enhanced using large scale OS data. |  |
| `last_update_date` | yes | string | The latest date on which any of the attributes on this record were last changed. |  |
| `island` | yes | string | Third level of geographic area name to record island names where appropriate. May be empty. |  |
| `change_code` | yes | `I` \| `U` \| `D` | The type of change last applied to the record. `I` insert, `U` update, `D` delete. |  |
| `building_name` | yes | string | The building name is a description applied to a single address or a group of addresses. May be empty. |  |
| `building_number` | yes | string | The building number is a number or range of numbers given to a single address or a group of addresses. May be empty. |  |
| `sub_building` | yes | string | The sub-building name and/or number for the address record. May be empty. |  |
| `postcode` | yes | string | A postcode assigned by Royal Mail for the address record. |  |
| `po_box` | yes | string | Text concatenation of 'PO BOX' and the Post Office Box (PO Box) number or 'BFPO' and the British Forces Post Office number. May be empty. |  |
| `organisation` | yes | string | The organisation name is the business name given, when appropriate, to an address record. May be empty. |  |
| `country` | yes | string | Full country names (ISO 3166) |  |
| `county` | yes | string | Since postal, administrative or traditional counties may not apply to some addresses, the county field is designed to return whatever county data is available. Normally, the postal county is returned. If this is not present, the county field will fall back to the administrative county. If the administrative county is also not present, the county field will fall back to the traditional county. May be empty in cases where no administrative, postal or traditional county present. |  |
| `district` | yes | string | The current district/unitary authority to which the postcode has been assigned. |  |
| `ward` | yes | string | The current administrative/electoral area to which the postcode has been assigned. May be empty for a small number of addresses. |  |
| `traditional_county` | yes | string | Traditional counties are provided by the Association of British Counties. It is historical data, and can date from the 1800s. May be empty. |  |
| `administrative_county` | yes | string | The current administrative county to which the postcode has been assigned. |  |
| `postal_county` | yes | string | Postal counties were used for the distribution of mail before the Postcode system was introduced in the 1970s. The Former Postal County was the Administrative County at the time. This data rarely changes. May be empty. |  |

## Example

```json
{
  "id": "ab_10070014461",
  "country_iso": "GBR",
  "dataset": "ab",
  "language": "en",
  "line_1": "Flat 27",
  "line_2": "Henry House",
  "line_3": "Ringers Road",
  "premise": "Flat 27, Henry House",
  "uprn": "10070014461",
  "udprn": 53705246,
  "parent_uprn": "10070014435",
  "usrn": 20301384,
  "toid": "osgb5000005186746874",
  "classification_code": "RD",
  "eastings": 540291,
  "northings": 168873,
  "latitude": 51.4015451,
  "longitude": 0.0154405,
  "single_address_line": "Flat 27, Henry House, Ringers Road, Bromley, BR1 1AA",
  "street_name": "Ringers Road",
  "locality": "",
  "town_name": "Bromley",
  "delivery_point_suffix": "2H",
  "post_town": "Bromley",
  "gss_code": "E09000006",
  "rpc": 2,
  "last_update_date": "2020-01-06T00:00:00.000Z",
  "island": "",
  "change_code": "I",
  "building_name": "Henry House",
  "building_number": "",
  "sub_building": "Flat 27",
  "postcode": "BR1 1AA",
  "po_box": "",
  "organisation": "",
  "country": "England",
  "county": "Kent",
  "district": "Bromley",
  "ward": "Bromley Town",
  "traditional_county": "Kent",
  "administrative_county": "",
  "postal_county": "Kent"
}
```
