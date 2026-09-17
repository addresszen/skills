# Denmark SDFI Address

An address from Danmarks Adresseregister (DAR), the official Danish address register maintained by the municipalities and distributed by Styrelsen for Dataforsyning og Infrastruktur (SDFI).

Covers both access addresses (`adgangsadresser`, a building entrance) and unit addresses (`adresser`, a flat or office within a building). Access addresses carry no floor, door, `kvh` or `adgangsadresse_*` values, which the API returns as empty strings.

Field names follow the Danish source. Fields the source spells with ASCII substitutions (`aendret`, `dor`) are returned with their Danish characters (`ændret`, `dør`).

**Schema name:** `SdfiAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | `sdfi` |  |  |
| `country` | yes | `Denmark` | Full country names (ISO 3166) |  |
| `country_iso` | yes | `DNK` | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | `DK` | 2 letter country code (ISO 3166-1) |  |
| `address` | yes | string | House number uniquely identifying the address along the street. Same value as `husnr`. |  |
| `line_1` | yes | string | First address line: street name and house number, followed by floor and door for a unit address. |  |
| `line_2` | yes | string | Second address line: the supplementary city name (`supplerendebynavn`) where present. |  |
| `language` | yes | `da` | Language represented by 2 letter ISO Code (639-1) |  |
| `latitude` | yes | string \| number | The latitude of the address or postcode (WGS84). |  |
| `longitude` | yes | string \| number | The longitude of the address or postcode (WGS84). |  |
| `adresse_id` | yes | string | Unique address identifier assigned by the data supplier. |  |
| `kvhx` | yes | string | Unique composite key for the address, containing codes for the municipality, road section, house number, floor and door. |  |
| `kvh` | yes | string | Composite key for the address, containing codes for the municipality, road section and house number. |  |
| `adgangsadresse` | yes | boolean | Indicates whether the address is an access address. |  |
| `status` | yes | string | `1` = final address, `3` = provisional address. |  |
| `darstatus` | yes | string | Status of the address indicated by the status code in Danmarks Adresseregister (DAR): `2` = provisional, `3` = valid, `4` = retired, `5` = suspended. |  |
| `oprettet` | yes | string | Date and time of address creation in Danmarks Adresseregister (DAR). |  |
| `ændret` | yes | string | Date and time of the last change to the address in Danmarks Adresseregister (DAR). |  |
| `ikrafttrædelse` | yes | string | Date and time at which the address became valid. |  |
| `nedlagt` | yes | string | Date and time from which the address is retired or suspended (may be in the future). |  |
| `vejkode` | yes | string | Four digit street identifier. |  |
| `vejnavn` | yes | string | Street name. |  |
| `adresseringsvejnavn` | yes | string | A possibly shortened version of the street name of no more than 20 characters, used where there is no space for the full street name. |  |
| `husnr` | yes | string | House number. |  |
| `etage` | yes | string | Floor designation. |  |
| `dør` | yes | string | Door designation. |  |
| `supplerendebynavn_dagi_id` | yes | string | Unique identifier in Danmarks Administrative Geografiske Inddeling (DAGI) of the supplementary town or city name. |  |
| `supplerendebynavn` | yes | string | Supplementary city name. |  |
| `postnr` | yes | string | Postal code. |  |
| `postnrnavn` | yes | string | The city or district name associated with the postal code. |  |
| `stormodtagerpostnr` | yes | string | Bulk recipient postal code (company postal code) which is associated with the address. |  |
| `stormodtagerpostnrnavn` | yes | string | The city or district name associated with the bulk recipient postal code. |  |
| `betegnelse` | yes | string | Full text of postal address. |  |
| `adressepunktændringsdato` | yes | string | Date and time of the last change to the address point. |  |
| `etrs89koordinat_øst` | yes | string | Easting coordinate for the address in the ETRS89 system. |  |
| `etrs89koordinat_nord` | yes | string | Northing coordinate for the address in the ETRS89 system. |  |
| `wgs84koordinat_bredde` | yes | string \| number | Latitude of the address in the WGS84 system. |  |
| `wgs84koordinat_længde` | yes | string \| number | Longitude of the address in the WGS84 system. |  |
| `højde` | yes | string | Height in metres from the mean water level in the seas on Denmark's coasts to ground level at the address, calculated according to the Danish Vertical Reference 1990 (DVR90). |  |
| `nøjagtighed` | yes | string | Code indicating the accuracy of the address point. `A` = accurate to within 2 metres, `B` = accurate to within 100 metres, `U` = no address point. |  |
| `kilde` | yes | string | Code indicating the source of the address point. |  |
| `tekniskstandard` | yes | string | Technical classification code for the location of an address point. |  |
| `tekstretning` | yes | string | Orientation for an address in gons, where a full circle is divided into 400 gons. |  |
| `ddkn_m100` | yes | string | Identifier of the 100m cell in which the address is located in Det Danske Kvadratnet (DDKN). |  |
| `ddkn_km1` | yes | string | Identifier of the 1km cell in which the address is located in Det Danske Kvadratnet (DDKN). |  |
| `ddkn_km10` | yes | string | Identifier of the 10km cell in which the address is located in Det Danske Kvadratnet (DDKN). |  |
| `kommunekode` | yes | string | Four digit identifier of the municipality in which the address is located. |  |
| `kommunenavn` | yes | string | Name of the municipality in which the address is located. |  |
| `landsdelsnuts3` | yes | string | NUTS 3 code of the province in which the address is located. |  |
| `landsdelsnavn` | yes | string | Name of the province in which the address is located. |  |
| `regionskode` | yes | string | Four digit identifier of the region in which the address is located. |  |
| `regionsnavn` | yes | string | Name of the region in which the address is located. |  |
| `afstemningsområdenummer` | yes | string | Identifier of the polling district in which the address is located. |  |
| `afstemningsområdenavn` | yes | string | Unique name of the polling district in which the address is located. |  |
| `menighedsrådsafstemningsområdenummer` | yes | string | Identifier of the parish council polling district in which the address is located. |  |
| `menighedsrådsafstemningsområdenavn` | yes | string | Name of the parish council polling district in which the address is located. |  |
| `opstillingskredskode` | yes | string | Identifier of the local electoral district in which the address is located. |  |
| `opstillingskredsnavn` | yes | string | Name of the local electoral district in which the address is located. |  |
| `storkredsnummer` | yes | string | Identifier of the regional electoral district in which the address is located. |  |
| `storkredsnavn` | yes | string | Name of the regional electoral district in which the address is located. |  |
| `valglandsdelsbogstav` | yes | string | Letter identifier of the national electoral district in which the address is located: `A`, `B` or `C`. |  |
| `valglandsdelsnavn` | yes | string | Name of the national electoral district in which the address is located. |  |
| `sognekode` | yes | string | Identifier of the parish in which the address is located. |  |
| `sognenavn` | yes | string | Name of the parish in which the address is located. |  |
| `politikredskode` | yes | string | Identifier of the police district in which the address is located. |  |
| `politikredsnavn` | yes | string | Name of the police district in which the address is located. |  |
| `retskredskode` | yes | string | Four digit identifier of the judicial district in which the address is located. |  |
| `retskredsnavn` | yes | string | Name of the judicial district in which the address is located. |  |
| `jordstykke_ejerlavkode` | yes | string | Identifier of a cadastral unit with a single owner. |  |
| `jordstykke_ejerlavnavn` | yes | string | Name of a cadastral unit with a single owner. |  |
| `jordstykke_matrikelnr` | yes | string | Cadastre identifier for the plot of land on which the address is located, consisting of up to 7 characters. |  |
| `jordstykke_esrejendomsnr` | yes | string | Identifier for the property from the Ejendomsstamregisteret (ESR) property register, corresponding to the plot of land associated with the address, consisting of up to 7 characters. |  |
| `ejerlavkode` | yes | string | Identifier of a cadastral unit with a single owner (deprecated). |  |
| `ejerlavnavn` | yes | string | Name of a cadastral unit with a single owner (deprecated). |  |
| `matrikelnr` | yes | string | Cadastre identifier for the plot of land on which the address is located, consisting of up to 7 characters. |  |
| `esrejendomsnr` | yes | string | Identifier for the property from the Ejendomsstamregisteret (ESR) property register, corresponding to the plot of land associated with the address, consisting of up to 7 characters. |  |
| `zone` | yes | string | Status of the address zone: `Byzone`, `Sommerhusområde` or `Landzone`. |  |
| `brofast` | yes | boolean | Indicates whether the address is connected by a bridge. |  |
| `adgangsadresseid` | yes | string | Identifier of the access address associated with the address. |  |
| `adgangspunktid` | yes | string | Identifier of the access point for the address. |  |
| `navngivenvej_id` | yes | string | Identifier of the named road on which the access address is located. |  |
| `adgangsadresse_status` | yes | string | Status of the access address associated with the address: `1` = final address, `3` = provisional address. |  |
| `adgangsadresse_darstatus` | yes | string | Status of the access address indicated by the status code in Danmarks Adresseregister (DAR): `2` = provisional, `3` = valid, `4` = retired, `5` = suspended. |  |
| `adgangsadresse_oprettet` | yes | string | Date and time of the creation of the access address associated with the address. |  |
| `adgangsadresse_ændret` | yes | string | Date and time of the last change to the access address associated with the address. |  |
| `adgangsadresse_ikrafttrædelse` | yes | string | Date and time at which the access address became valid. |  |
| `adgangsadresse_nedlagt` | yes | string | Date and time from which the access address is retired or suspended (may be in the future). |  |
| `vejpunkt_id` | yes | string | Unique identifier of the geographic point on the road network that represents the starting point of the access route leading to the access point for the address. |  |
| `vejpunkt_ændret` | yes | string | Date and time of the last change in Danmarks Adresseregister (DAR) to the geographic point on the road network that represents the starting point of the access route leading to the access point for the address. |  |
| `vejpunkt_kilde` | yes | string | Source of the geographic point on the road network that represents the starting point of the access route leading to the access point for the address. |  |
| `vejpunkt_nøjagtighed` | yes | string | Accuracy of the geographic point on the road network that represents the starting point of the access route leading to the access point for the address: `A` = exact, `B` = approximate. |  |
| `vejpunkt_tekniskstandard` | yes | string | Technical classification code for the geographic point on the road network that represents the starting point of the access route leading to the access point for the address. |  |
| `vejpunkt_x` | yes | string | Longitude in the WGS84 system of the geographic point on the road network that represents the starting point of the access route leading to the access point for the address. |  |
| `vejpunkt_y` | yes | string | Latitude in the WGS84 system of the geographic point on the road network that represents the starting point of the access route leading to the access point for the address. |  |

## Example

```json
{
  "id": "sdfi_0a3f50a5-1d3e-32b8-e044-0003ba298018",
  "dataset": "sdfi",
  "country": "Denmark",
  "country_iso": "DNK",
  "country_iso_2": "DK",
  "address": "3",
  "line_1": "Bakkevej 3, 2. tv",
  "line_2": "Pindstrup",
  "language": "da",
  "latitude": 56.3086,
  "longitude": 10.4917,
  "adresse_id": "0a3f50a5-1d3e-32b8-e044-0003ba298018",
  "kvhx": "07060092___3__2__tv",
  "kvh": "07060092___3",
  "adgangsadresse": false,
  "status": "1",
  "darstatus": "3",
  "oprettet": "2000-02-05T20:34:00.000Z",
  "ændret": "2018-11-02T12:15:00.000Z",
  "ikrafttrædelse": "2000-02-05T00:00:00.000Z",
  "nedlagt": "",
  "vejkode": "0092",
  "vejnavn": "Bakkevej",
  "adresseringsvejnavn": "Bakkevej",
  "husnr": "3",
  "etage": "2",
  "dør": "tv",
  "supplerendebynavn_dagi_id": "580362",
  "supplerendebynavn": "Pindstrup",
  "postnr": "8550",
  "postnrnavn": "Ryomgård",
  "stormodtagerpostnr": "",
  "stormodtagerpostnrnavn": "",
  "betegnelse": "Bakkevej 3, 2. tv, Pindstrup, 8550 Ryomgård",
  "adressepunktændringsdato": "2010-05-12T00:00:00.000Z",
  "etrs89koordinat_øst": "592180.45",
  "etrs89koordinat_nord": "6256980.12",
  "wgs84koordinat_bredde": 56.3086,
  "wgs84koordinat_længde": 10.4917,
  "højde": "40.5",
  "nøjagtighed": "A",
  "kilde": "5",
  "tekniskstandard": "TN",
  "tekstretning": "200.00",
  "ddkn_m100": "100m_62569_5921",
  "ddkn_km1": "1km_6256_592",
  "ddkn_km10": "10km_625_59",
  "kommunekode": "0706",
  "kommunenavn": "Syddjurs",
  "landsdelsnuts3": "DK042",
  "landsdelsnavn": "Østjylland",
  "regionskode": "1082",
  "regionsnavn": "Region Midtjylland",
  "afstemningsområdenummer": "05",
  "afstemningsområdenavn": "Pindstrup",
  "menighedsrådsafstemningsområdenummer": "",
  "menighedsrådsafstemningsområdenavn": "",
  "opstillingskredskode": "0058",
  "opstillingskredsnavn": "Djurs",
  "storkredsnummer": "10",
  "storkredsnavn": "Østjyllands",
  "valglandsdelsbogstav": "C",
  "valglandsdelsnavn": "Midtjylland-Nordjylland",
  "sognekode": "8271",
  "sognenavn": "Marie Magdalene",
  "politikredskode": "1461",
  "politikredsnavn": "Østjyllands Politi",
  "retskredskode": "1174",
  "retskredsnavn": "Retten i Randers",
  "jordstykke_ejerlavkode": "1230651",
  "jordstykke_ejerlavnavn": "Pindstrup By, Marie Magdalene",
  "jordstykke_matrikelnr": "7ab",
  "jordstykke_esrejendomsnr": "",
  "ejerlavkode": "1230651",
  "ejerlavnavn": "Pindstrup By, Marie Magdalene",
  "matrikelnr": "7ab",
  "esrejendomsnr": "",
  "zone": "Byzone",
  "brofast": true,
  "adgangsadresseid": "0a3f508e-1c2b-32b8-e044-0003ba298018",
  "adgangspunktid": "0a3f7001-3b2c-32b8-e044-0003ba298018",
  "navngivenvej_id": "0a3f7002-4c3d-32b8-e044-0003ba298018",
  "adgangsadresse_status": "1",
  "adgangsadresse_darstatus": "3",
  "adgangsadresse_oprettet": "2000-02-05T20:34:00.000Z",
  "adgangsadresse_ændret": "2018-11-02T12:15:00.000Z",
  "adgangsadresse_ikrafttrædelse": "2000-02-05T00:00:00.000Z",
  "adgangsadresse_nedlagt": "",
  "vejpunkt_id": "0a3f7003-5d4e-32b8-e044-0003ba298018",
  "vejpunkt_ændret": "2019-03-14T09:20:00.000Z",
  "vejpunkt_kilde": "Ekstern",
  "vejpunkt_nøjagtighed": "A",
  "vejpunkt_tekniskstandard": "V0",
  "vejpunkt_x": "10.49141",
  "vejpunkt_y": "56.30833"
}
```
