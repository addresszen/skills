# Japan UPU Address

A Japanese address from the Universal Postal Union's address file for Japan. Each address carries its postal code, prefecture, city, district and neighbourhood, a block or house number range and, where present, a building and an organisation name, in kanji, hiragana and Hepburn romanisation.

- Records are number ranges, not delivery points. One record covers `str_from_num` to `str_to_num` under the `str_evenodd` scheme, so a single record can stand for many premises. `address` is the one number selected from that range for the query, and `id` carries it after a `|`.
- There is no sub-premise detail. The finest elements are the block or house number and a building name. There is no unit, floor or sub-building field.
- The dataset carries no coordinates. `latitude` and `longitude` are always the empty string.
- The API indexes every address once per script, so the same address comes back as separate records with separate `id`s. `script` is `Hani` (kanji), `Hira` (hiragana) or `Latn` (Hepburn romanisation), and `language` is `ja` on all three. `en` is reserved for English building name synonyms and is not expected in practice.

Conventions:

- `line_1` is the block or house number alone and repeats `address`. There is no `line_2` or `line_3`. Build the rest of the address from `prefecture`, `city`, `district`, `neighbourhood` and `building_name`.
- A kanji or hiragana address is written as `〒`, the postcode, a space, then prefecture, city, district, neighbourhood, number and building name run together with no separators: `〒070-8006 北海道旭川市神楽六条十三丁目12-2`. A romanised address is the same elements comma separated after a bare postcode: `070-8006, Hokkaido, Asahikawa-shi, Kagura 6jo 13-Chome, 12-2`.
- On the romanised variant the API title cases the display fields and lower cases the Latin locality suffix before joining it on, giving `Asahikawa-shi` and `Nasu-machi`. The raw source fields are as supplied, so every `*_trans` field stays upper case.
- No field is null. A value the source does not carry is the empty string, and every field is present on every record.
- `id` is `upujp_` followed by a URL-safe base64 MD5 of the address line, suffixed `|` and the number when the record covers a range and one number has been resolved (`upujp_2ry6tOmv4gOAWU2v5CVxBw|12-2`).
- Alongside the resolved fields the record carries the source columns under their original names: `org_*` (organisation), `str_*` (street, number range and building), `sub_*` (district and neighbourhood) and `loc_*` (locality and administrative divisions 1 to 3). Most are empty for a typical residential address.

**Schema name:** `UpujpAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | `upujp` | Indicates the provenance of an address |  |
| `country` | yes | `Japan` | Full country names (ISO 3166) |  |
| `country_iso` | yes | `JPN` | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | `JP` | 2 letter country code (ISO 3166-1) |  |
| `language` | yes | `ja` \| `en` | Language represented by 2 letter ISO Code (639-1) |  |
| `script` | yes | `Hani` \| `Hira` \| `Latn` | ISO 15924 script of the address elements. |  |
| `address` | yes | string | Address / House Number uniquely identifying the address along the specified street. |  |
| `line_1` | yes | string | The block or house number alone, identical to `address`. There is no `line_2` or `line_3`; build the rest of the address from `prefecture`, `city`, `district`, `neighbourhood` and `building_name`. |  |
| `building_name` | yes | string | Preferred building name. |  |
| `neighbourhood` | yes | string | Preferred neighbourhood name. |  |
| `district` | yes | string | Preferred district name. |  |
| `city` | yes | string | Preferred city name. |  |
| `prefecture` | yes | string | Preferred prefecture name. |  |
| `postcode` | yes | string | Preferred postal code. |  |
| `latitude` | yes | string \| number | The latitude of the address or postcode (WGS84). |  |
| `longitude` | yes | string \| number | The longitude of the address or postcode (WGS84). |  |
| `org_id` | yes | string | The unique identifier of an organisation. |  |
| `org_type_ind` | yes | string \| number | Indicates the type of organisation. |  |
| `org_sub_type_ind` | yes | string \| number | Indicates the sub-type of the organisation. |  |
| `org_loc_id` | yes | string | Locality identifier for the organisation. |  |
| `org_dis_id` | yes | string | District identifier for the organisation. |  |
| `org_nei_id` | yes | string | Neighbourhood identifier for the organisation. |  |
| `org_org_id` | yes | string | Associated organisation identifier for the organisation. |  |
| `org_name` | yes | string | Name of the organisation. |  |
| `org_name_trans` | yes | string | Translated name of the organisation in Latin script. |  |
| `org_loc_sfx` | yes | string | Suffix of the locality for the organisation. |  |
| `org_loc_sfx_trans` | yes | string | Translated suffix of the locality for the organisation in Latin script. |  |
| `org_adr` | yes | string | Address of the organisation. |  |
| `org_adr_trans` | yes | string | Translated address of the organisation in Latin script. |  |
| `org_po_ind` | yes | string \| number | Indicates whether the organisation has a post office box. |  |
| `org_po_start` | yes | string | Post office box number or start of the post office box range associated with the organisation. |  |
| `org_po_end` | yes | string | End of the post office box range associated with the organisation. |  |
| `org_dsc` | yes | string | Additional information about the organisation. |  |
| `org_dsc_trans` | yes | string | Translated additional information about the organisation in Latin script. |  |
| `org_pcode` | yes | string | Postal code for the organisation. |  |
| `org_pcode_fin` | yes | string | Final postal code for the organisation. |  |
| `org_script` | yes | string | Script used for the organisation name. |  |
| `org_language` | yes | string | Language used for the organisation name. |  |
| `str_id` | yes | string | Identifier of the street (not unique). |  |
| `str_key` | yes | string | Permanent identifier of the street. |  |
| `str_loc_id` | yes | string | Locality identifier for the street. |  |
| `str_dis_id` | yes | string | District identifier for the street. |  |
| `str_nei_id` | yes | string | Neighbourhood identifier for the street. |  |
| `str_org_id` | yes | string | Associated organisation identifier for the street. |  |
| `str_pfx` | yes | string | Prefix of the street name. |  |
| `str_pfx_trans` | yes | string | Translated prefix of the street name in Latin script. |  |
| `str_qlf_pre` | yes | string | Preceding qualifier of the street name. |  |
| `str_qlf_pre_trans` | yes | string | Translated preceding qualifier of the street name in Latin script. |  |
| `str_qlf_suc` | yes | string | Succeeding qualifier of the street name. |  |
| `str_qlf_suc_trans` | yes | string | Translated succeeding qualifier of the street name in Latin script. |  |
| `str_name` | yes | string | Name of the street. |  |
| `str_name_trans` | yes | string | Translated name of the street in Latin script. |  |
| `str_loc_sfx` | yes | string | Suffix of the locality for the street. |  |
| `str_loc_sfx_trans` | yes | string | Translated suffix of the locality for the street in Latin script. |  |
| `str_type` | yes | string | Type of the street. |  |
| `str_type_trans` | yes | string | Translated type of the street in Latin script. |  |
| `str_type_abv` | yes | string | Abbreviation of the street type. |  |
| `str_type_abv_trans` | yes | string | Translated abbreviation of the street type in Latin script. |  |
| `str_adr_num_key` | yes | string | Permanent identifier of the address. |  |
| `str_from_num` | yes | string \| number | Lowest address number on the street. |  |
| `str_from_unit` | yes | string | Lowest unit number on the street. |  |
| `str_from_alph` | yes | string | Extension of the lowest address number on the street. |  |
| `str_to_num` | yes | string \| number | Highest address number on the street. |  |
| `str_to_unit` | yes | string | Highest unit number on the street. |  |
| `str_to_alph` | yes | string | Extension of the highest address number on the street. |  |
| `str_evenodd` | yes | string \| number | Indicates whether the address range for this street contains even numbers, odd numbers, or both. |  |
| `str_dsc` | yes | string | Additional information about the street. |  |
| `str_dsc_trans` | yes | string | Translated additional information about the street in Latin script. |  |
| `str_blg_id` | yes | string | Identifier of the building for the street. |  |
| `str_blg_name` | yes | string | Name of the building for the street. |  |
| `str_blg_name_trans` | yes | string | Translated name of the building for the street in Latin script. |  |
| `str_blg_type` | yes | string | Type of the building for the street. |  |
| `str_blg_type_trans` | yes | string | Translated type of the building for the street in Latin script. |  |
| `str_blg_dsc` | yes | string | Additional information about the building for the street. |  |
| `str_blg_dsc_trans` | yes | string | Translated additional information about the building for the street in Latin script. |  |
| `str_ref_str_id` | yes | string | Identifier of the associated street. |  |
| `str_pcode` | yes | string | Postal code for the street. |  |
| `str_script` | yes | string | Script used for the street name. |  |
| `str_language` | yes | string | Language used for the street name. |  |
| `sub_dis_id` | yes | string | Unique identifier of the district. |  |
| `sub_dis_key` | yes | string | Permanent identifier of the district. |  |
| `sub_loc_id` | yes | string | Locality identifier for the subdivision. |  |
| `sub_loc_sfx` | yes | string | Suffix of the locality for the subdivision. |  |
| `sub_loc_sfx_trans` | yes | string | Translated suffix of the locality for the subdivision in Latin script. |  |
| `sub_dis_name` | yes | string | Name of the district. |  |
| `sub_dis_name_trans` | yes | string | Translated name of the district in Latin script. |  |
| `sub_dis_sfx` | yes | string | Suffix of the district. |  |
| `sub_dis_sfx_trans` | yes | string | Translated suffix of the district in Latin script. |  |
| `sub_dis_dsc` | yes | string | Additional information about the district. |  |
| `sub_dis_dsc_trans` | yes | string | Translated additional information about the district in Latin script. |  |
| `sub_dis_pcode` | yes | string | Postal code for the district. |  |
| `sub_dis_pcode_fin` | yes | string | Final postal code for the district. |  |
| `sub_nei_id` | yes | string | Identifier of the neighbourhood. |  |
| `sub_nei_key` | yes | string | Permanent identifier of the neighbourhood. |  |
| `sub_nei_name` | yes | string | Name of the neighbourhood. |  |
| `sub_nei_name_trans` | yes | string | Translated name of the neighbourhood in Latin script. |  |
| `sub_nei_sfx` | yes | string | Suffix of the neighbourhood. |  |
| `sub_nei_sfx_trans` | yes | string | Translated suffix of the neighbourhood in Latin script. |  |
| `sub_nei_zone_from` | yes | string | Start of the range of zone numbers to which the neighbourhood postal code corresponds. |  |
| `sub_nei_zone_to` | yes | string | End of the range of zone numbers to which the neighbourhood postal code corresponds. |  |
| `sub_nei_dsc` | yes | string | Additional information about the neighbourhood. |  |
| `sub_nei_dsc_trans` | yes | string | Translated additional information about the neighbourhood in Latin script. |  |
| `sub_nei_pcode` | yes | string | Postal code for the neighbourhood. |  |
| `sub_script` | yes | string | Script used for the subdivision names. |  |
| `sub_language` | yes | string | Language used for the subdivision names. |  |
| `loc_id` | yes | string | Unique identifier of the locality. |  |
| `loc_key` | yes | string | Permanent identifier of the locality. |  |
| `loc_adm1_id` | yes | string | Identifier of administrative division 1. |  |
| `loc_adm1_key` | yes | string | Permanent identifier of administrative division 1. |  |
| `loc_adm1_name` | yes | string | Name of administrative division 1. |  |
| `loc_adm1_name_trans` | yes | string | Translated name of administrative division 1 in Latin script. |  |
| `loc_adm1_sfx` | yes | string | Suffix of administrative division 1. |  |
| `loc_adm1_sfx_trans` | yes | string | Translated suffix of administrative division 1 in Latin script. |  |
| `loc_adm1_abv` | yes | string | Abbreviation of administrative division 1. |  |
| `loc_adm1_abv_trans` | yes | string | Translated abbreviation of administrative division 1 in Latin script. |  |
| `loc_adm2_id` | yes | string | Identifier of administrative division 2. |  |
| `loc_adm2_key` | yes | string | Permanent identifier of administrative division 2. |  |
| `loc_adm2_name` | yes | string | Name of administrative division 2. |  |
| `loc_adm2_name_trans` | yes | string | Translated name of administrative division 2 in Latin script. |  |
| `loc_adm2_sfx` | yes | string | Suffix of administrative division 2. |  |
| `loc_adm2_sfx_trans` | yes | string | Translated suffix of administrative division 2 in Latin script. |  |
| `loc_adm2_abv` | yes | string | Abbreviation of administrative division 2. |  |
| `loc_adm2_abv_trans` | yes | string | Translated abbreviation of administrative division 2 in Latin script. |  |
| `loc_adm3_id` | yes | string | Identifier of administrative division 3. |  |
| `loc_adm3_key` | yes | string | Permanent identifier of administrative division 3. |  |
| `loc_adm3_name` | yes | string | Name of administrative division 3. |  |
| `loc_adm3_name_trans` | yes | string | Translated name of administrative division 3 in Latin script. |  |
| `loc_adm3_sfx` | yes | string | Suffix of administrative division 3. |  |
| `loc_adm3_sfx_trans` | yes | string | Translated suffix of administrative division 3 in Latin script. |  |
| `loc_adm3_abv` | yes | string | Abbreviation of administrative division 3. |  |
| `loc_adm3_abv_trans` | yes | string | Translated abbreviation of administrative division 3 in Latin script. |  |
| `loc_name` | yes | string | Name of the locality. |  |
| `loc_name_trans` | yes | string | Translated name of the locality in Latin script. |  |
| `loc_sfx` | yes | string | Suffix of the locality. |  |
| `loc_sfx_trans` | yes | string | Translated suffix of the locality in Latin script. |  |
| `loc_pcode` | yes | string | Postal code of the locality. |  |
| `loc_pcode_fin` | yes | string | Final postal code of the locality. |  |
| `loc_dsc` | yes | string | Additional information about the locality. |  |
| `loc_dsc_trans` | yes | string | Translated additional information about the locality in Latin script. |  |
| `loc_script` | yes | string | Script used for the locality names. |  |
| `loc_language` | yes | string | Language used for the locality names. |  |

## Example

```json
{
  "id": "upujp_2ry6tOmv4gOAWU2v5CVxBw|12-2",
  "dataset": "upujp",
  "country": "Japan",
  "country_iso": "JPN",
  "country_iso_2": "JP",
  "language": "ja",
  "script": "Hani",
  "address": "12-2",
  "line_1": "12-2",
  "building_name": "",
  "neighbourhood": "神楽六条十三丁目",
  "district": "",
  "city": "旭川市",
  "prefecture": "北海道",
  "postcode": "070-8006",
  "latitude": "",
  "longitude": "",
  "org_id": "",
  "org_type_ind": "",
  "org_sub_type_ind": "",
  "org_loc_id": "",
  "org_dis_id": "",
  "org_nei_id": "",
  "org_org_id": "",
  "org_name": "",
  "org_name_trans": "",
  "org_loc_sfx": "",
  "org_loc_sfx_trans": "",
  "org_adr": "",
  "org_adr_trans": "",
  "org_po_ind": "",
  "org_po_start": "",
  "org_po_end": "",
  "org_dsc": "",
  "org_dsc_trans": "",
  "org_pcode": "",
  "org_pcode_fin": "",
  "org_script": "",
  "org_language": "",
  "str_id": "0",
  "str_key": "",
  "str_loc_id": "914161",
  "str_dis_id": "",
  "str_nei_id": "194855",
  "str_org_id": "",
  "str_pfx": "",
  "str_pfx_trans": "",
  "str_qlf_pre": "",
  "str_qlf_pre_trans": "",
  "str_qlf_suc": "",
  "str_qlf_suc_trans": "",
  "str_name": "",
  "str_name_trans": "",
  "str_loc_sfx": "",
  "str_loc_sfx_trans": "",
  "str_type": "",
  "str_type_trans": "",
  "str_type_abv": "",
  "str_type_abv_trans": "",
  "str_adr_num_key": "",
  "str_from_num": 2,
  "str_from_unit": "12",
  "str_from_alph": "",
  "str_to_num": 2,
  "str_to_unit": "12",
  "str_to_alph": "",
  "str_evenodd": 6,
  "str_dsc": "",
  "str_dsc_trans": "",
  "str_blg_id": "49928324",
  "str_blg_name": "",
  "str_blg_name_trans": "",
  "str_blg_type": "番",
  "str_blg_type_trans": "BAN",
  "str_blg_dsc": "",
  "str_blg_dsc_trans": "",
  "str_ref_str_id": "",
  "str_pcode": "070-8006",
  "str_script": "",
  "str_language": "",
  "sub_dis_id": "",
  "sub_dis_key": "",
  "sub_loc_id": "914161",
  "sub_loc_sfx": "",
  "sub_loc_sfx_trans": "",
  "sub_dis_name": "",
  "sub_dis_name_trans": "",
  "sub_dis_sfx": "",
  "sub_dis_sfx_trans": "",
  "sub_dis_dsc": "",
  "sub_dis_dsc_trans": "",
  "sub_dis_pcode": "",
  "sub_dis_pcode_fin": "",
  "sub_nei_id": "194855",
  "sub_nei_key": "",
  "sub_nei_name": "神楽六条十三丁目",
  "sub_nei_name_trans": "KAGURA 6JO 13-CHOME",
  "sub_nei_sfx": "",
  "sub_nei_sfx_trans": "G",
  "sub_nei_zone_from": "",
  "sub_nei_zone_to": "",
  "sub_nei_dsc": "",
  "sub_nei_dsc_trans": "",
  "sub_nei_pcode": "070-8006",
  "sub_script": "Hani",
  "sub_language": "ja",
  "loc_id": "914161",
  "loc_key": "3265925806",
  "loc_adm1_id": "12010",
  "loc_adm1_key": "JP.HK",
  "loc_adm1_name": "北海道",
  "loc_adm1_name_trans": "HOKKAIDO",
  "loc_adm1_sfx": "",
  "loc_adm1_sfx_trans": "",
  "loc_adm1_abv": "",
  "loc_adm1_abv_trans": "",
  "loc_adm2_id": "",
  "loc_adm2_key": "",
  "loc_adm2_name": "",
  "loc_adm2_name_trans": "",
  "loc_adm2_sfx": "",
  "loc_adm2_sfx_trans": "",
  "loc_adm2_abv": "",
  "loc_adm2_abv_trans": "",
  "loc_adm3_id": "",
  "loc_adm3_key": "",
  "loc_adm3_name": "",
  "loc_adm3_name_trans": "",
  "loc_adm3_sfx": "",
  "loc_adm3_sfx_trans": "",
  "loc_adm3_abv": "",
  "loc_adm3_abv_trans": "",
  "loc_name": "旭川市",
  "loc_name_trans": "ASAHIKAWA",
  "loc_sfx": "",
  "loc_sfx_trans": "-SHI",
  "loc_pcode": "070-0000",
  "loc_pcode_fin": "",
  "loc_dsc": "",
  "loc_dsc_trans": "",
  "loc_script": "Hani",
  "loc_language": "ja"
}
```
