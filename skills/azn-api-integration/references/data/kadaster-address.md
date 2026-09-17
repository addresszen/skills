# Netherlands Kadaster Address

A Netherlands address as recorded in the Kadaster BAG (Basisregistratie Adressen en Gebouwen), the Dutch national register of addresses and buildings.

Fields are grouped by the BAG object they originate from: the verblijfsobject (unprefixed) and the related `nummeraanduidingen_`, `pand_`, `openbare_ruimte_` and `woonplaats_` objects.

**Schema name:** `KadasterAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | `kadaster` | Dataset the address originates from. |  |
| `country` | yes | `Netherlands` | Full country names (ISO 3166) |  |
| `country_iso` | yes | `NLD` | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | `NL` | 2 letter country code (ISO 3166-1) |  |
| `line_1` | yes | string | First address line: street name followed by house number. |  |
| `language` | yes | `nl` | Language represented by 2 letter ISO Code (639-1) |  |
| `address` | yes | string | House number, uniquely identifying the address along the specified street. Combines huisnummer, huisletter and huisnummertoevoeging. |  |
| `identificatie` | yes | string | The unique identifier of a BAG verblijfsobject. |  |
| `latitude` | yes | string \| number | The latitude of the address or postcode (WGS84). |  |
| `longitude` | yes | string \| number | The longitude of the address or postcode (WGS84). |  |
| `gebruiksdoel` | yes | string | The purpose of use of the verblijfsobject. E.g. `woonfunctie` (residential), `kantoorfunctie` (office), `winkelfunctie` (retail). |  |
| `oppervlakte` | yes | integer | The floor area of the verblijfsobject in square metres. |  |
| `status` | yes | string | Verblijfsobject status. E.g. `Verblijfsobject in gebruik` (in use). |  |
| `geconstateerd` | yes | boolean | Indicates that a verblijfsobject has been included in the registry as a result of an observation, without there being a regular source document for this inclusion at the time of registration. |  |
| `documentdatum` | yes | string | Date on which the verblijfsobject source document was created. |  |
| `documentnummer` | yes | string | The unique identifier of the verblijfsobject source document. |  |
| `voorkomenidentificatie` | yes | `""` \| integer |  |  |
| `begin_geldigheid` | yes | string | The time at which a version of a verblijfsobject is valid in reality in accordance with the effective date in the source document. ISO 8601 timestamp. |  |
| `eind_geldigheid` | yes | string | The time at which a version of a verblijfsobject is no longer valid in reality. ISO 8601 timestamp. |  |
| `tijdstip_registratie` | yes | string | The time at which a version of a verblijfsobject is registered by the bronhouder. ISO 8601 timestamp. |  |
| `eind_registratie` | yes | string | The time at which a version of a verblijfsobject is no longer valid according to the bronhouder. ISO 8601 timestamp. |  |
| `tijdstip_registratie_lv` | yes | string | The time at which a version of a verblijfsobject is registered in the Landelijke Voorziening BAG. ISO 8601 timestamp. |  |
| `tijdstip_eind_registratie_lv` | yes | string | The time at which a version of a verblijfsobject is no longer valid in the Landelijke Voorziening BAG. ISO 8601 timestamp. |  |
| `nummeraanduidingen_identificatie` | yes | string | The unique identifier of a BAG nummeraanduidingen object. |  |
| `nummeraanduidingen_huisnummer` | yes | string | The house number assigned to a nummeraanduiding object by or on behalf of the municipal council. |  |
| `nummeraanduidingen_huisnummertoevoeging` | yes | string | A further addition to a house number, or to a combination of house number and house letter, granted by or on behalf of the municipal council with regard to a nummeraanduiding object. |  |
| `nummeraanduidingen_huisletter` | yes | string | An addition to a house number in the form of an alphanumeric character assigned by or on behalf of the municipal council with regard to a nummeraanduiding object. |  |
| `nummeraanduidingen_postcode` | yes | string | A code determined by PostNL associated with a specific combination of a street name and a house number. Normalised to `1234 AB`. |  |
| `nummeraanduidingen_type_adresseerbaar_object` | yes | string | The nature of the nummeraanduiding object. Currently always `Verblijfsobject`. |  |
| `nummeraanduidingen_status` | yes | string | The status of the nummeraanduiding object. E.g. `Naamgeving uitgegeven` (name issued), `Naamgeving ingetrokken` (name withdrawn). |  |
| `nummeraanduidingen_geconstateerd` | yes | boolean | Indicates that a nummeraanduidingen object has been included in the registry as a result of an observation, without there being a regular source document for this inclusion at the time of registration. |  |
| `nummeraanduidingen_documentdatum` | yes | string | Date on which the nummeraanduidingen object source document was created. ISO 8601 timestamp. |  |
| `nummeraanduidingen_documentnummer` | yes | string | The unique identifier of the nummeraanduidingen object source document. |  |
| `nummeraanduidingen_voorkomenidentificatie` | yes | `""` \| integer |  |  |
| `nummeraanduidingen_begin_geldigheid` | yes | string | The time at which a version of a nummeraanduidingen object is valid in reality in accordance with the effective date in the source document. ISO 8601 timestamp. |  |
| `nummeraanduidingen_eind_geldigheid` | yes | string | The time at which a version of a nummeraanduidingen object is no longer valid in reality. ISO 8601 timestamp. |  |
| `nummeraanduidingen_tijdstip_registratie` | yes | string | The time at which a version of a nummeraanduidingen object is registered by the bronhouder. ISO 8601 timestamp. |  |
| `nummeraanduidingen_eind_registratie` | yes | string | The time at which a version of a nummeraanduidingen object is no longer valid according to the bronhouder. ISO 8601 timestamp. |  |
| `nummeraanduidingen_tijdstip_registratie_lv` | yes | string | The time at which a version of a nummeraanduidingen object is registered in the Landelijke Voorziening BAG. ISO 8601 timestamp. |  |
| `nummeraanduidingen_tijdstip_eind_registratie_lv` | yes | string | The time at which a version of a nummeraanduidingen object is no longer valid in the Landelijke Voorziening BAG. ISO 8601 timestamp. |  |
| `pand_identificatie` | yes | string | The unique identifier of a BAG pand object. |  |
| `pand_oorspronkelijk_bouwjaar` | yes | `""` \| integer |  |  |
| `pand_status` | yes | string | The status of the pand object. E.g. `Pand in gebruik` (building in use). |  |
| `pand_geconstateerd` | yes | boolean | Indicates that a pand object has been included in the registry as a result of an observation, without there being a regular source document for this inclusion at the time of registration. |  |
| `pand_documentdatum` | yes | string | Date on which the pand object source document was created. ISO 8601 timestamp. |  |
| `pand_documentnummer` | yes | string | The unique identifier of the pand object source document. |  |
| `pand_voorkomenidentificatie` | yes | `""` \| integer |  |  |
| `pand_begin_geldigheid` | yes | string | The time at which a version of a pand object is valid in reality in accordance with the effective date in the source document. ISO 8601 timestamp. |  |
| `pand_eind_geldigheid` | yes | string | The time at which a version of a pand object is no longer valid in reality. ISO 8601 timestamp. |  |
| `pand_tijdstip_registratie` | yes | string | The time at which a version of a pand object is registered by the bronhouder. ISO 8601 timestamp. |  |
| `pand_eind_registratie` | yes | string | The time at which a version of a pand object is no longer valid according to the bronhouder. ISO 8601 timestamp. |  |
| `pand_tijdstip_registratie_lv` | yes | string | The time at which a version of a pand object is registered in the Landelijke Voorziening BAG. ISO 8601 timestamp. |  |
| `pand_tijdstip_eind_registratie_lv` | yes | string | The time at which a version of a pand object is no longer valid in the Landelijke Voorziening BAG. ISO 8601 timestamp. |  |
| `openbare_ruimte_identificatie` | yes | string | The unique identifier of a BAG openbare ruimte object. |  |
| `openbare_ruimte_naam` | yes | string | The name assigned to an openbare ruimte object by or on behalf of the municipal council. Usually the street name. |  |
| `openbare_ruimte_type` | yes | string | The nature of the openbare ruimte object. E.g. `Weg` (road), `Water`, `Spoorbaan` (railway). |  |
| `openbare_ruimte_status` | yes | string | The status of the openbare ruimte object. E.g. `Naamgeving uitgegeven` (name issued). |  |
| `openbare_ruimte_geconstateerd` | yes | boolean | Indicates that an openbare ruimte object has been included in the registry as a result of an observation, without there being a regular source document for this inclusion at the time of registration. |  |
| `openbare_ruimte_documentdatum` | yes | string | Date on which the openbare ruimte object source document was created. ISO 8601 timestamp. |  |
| `openbare_ruimte_documentnummer` | yes | string | The unique identifier of the openbare ruimte object source document. |  |
| `openbare_ruimte_voorkomenidentificatie` | yes | `""` \| integer |  |  |
| `openbare_ruimte_begin_geldigheid` | yes | string | The time at which a version of an openbare ruimte object is valid in reality in accordance with the effective date in the source document. ISO 8601 timestamp. |  |
| `openbare_ruimte_eind_geldigheid` | yes | string | The time at which a version of an openbare ruimte object is no longer valid in reality. ISO 8601 timestamp. |  |
| `openbare_ruimte_tijdstip_registratie` | yes | string | The time at which a version of an openbare ruimte object is registered by the bronhouder. ISO 8601 timestamp. |  |
| `openbare_ruimte_eind_registratie` | yes | string | The time at which a version of an openbare ruimte object is no longer valid according to the bronhouder. ISO 8601 timestamp. |  |
| `openbare_ruimte_tijdstip_registratie_lv` | yes | string | The time at which a version of an openbare ruimte object is registered in the Landelijke Voorziening BAG. ISO 8601 timestamp. |  |
| `openbare_ruimte_tijdstip_eind_registratie_lv` | yes | string | The time at which a version of an openbare ruimte object is no longer valid in the Landelijke Voorziening BAG. ISO 8601 timestamp. |  |
| `openbare_ruimte_verkorte_naam` | yes | string | An abbreviated name assigned to an openbare ruimte object if its name is longer than 24 characters. |  |
| `woonplaats_identificatie` | yes | string | The unique identifier of a BAG woonplaats object. |  |
| `woonplaats_naam` | yes | string | The name assigned to a woonplaats object by or on behalf of the municipal council. The town or city name. |  |
| `woonplaats_status` | yes | string | The status of the woonplaats object. E.g. `Woonplaats aangewezen` (place of residence designated). |  |
| `woonplaats_geconstateerd` | yes | boolean | Indicates that a woonplaats object has been included in the registry as a result of an observation, without there being a regular source document for this inclusion at the time of registration. |  |
| `woonplaats_documentdatum` | yes | string | Date on which the woonplaats object source document was created. ISO 8601 timestamp. |  |
| `woonplaats_documentnummer` | yes | string | The unique identifier of the woonplaats object source document. |  |
| `woonplaats_voorkomenidentificatie` | yes | `""` \| integer |  |  |
| `woonplaats_begin_geldigheid` | yes | string | The time at which a version of a woonplaats object is valid in reality in accordance with the effective date in the source document. ISO 8601 timestamp. |  |
| `woonplaats_eind_geldigheid` | yes | string | The time at which a version of a woonplaats object is no longer valid in reality. ISO 8601 timestamp. |  |
| `woonplaats_tijdstip_registratie` | yes | string | The time at which a version of a woonplaats object is registered by the bronhouder. ISO 8601 timestamp. |  |
| `woonplaats_eind_registratie` | yes | string | The time at which a version of a woonplaats object is no longer valid according to the bronhouder. ISO 8601 timestamp. |  |
| `woonplaats_tijdstip_registratie_lv` | yes | string | The time at which a version of a woonplaats object is registered in the Landelijke Voorziening BAG. ISO 8601 timestamp. |  |
| `woonplaats_tijdstip_eind_registratie_lv` | yes | string | The time at which a version of a woonplaats object is no longer valid in the Landelijke Voorziening BAG. ISO 8601 timestamp. |  |
| `provincie` | yes | string | Province the address falls in, derived from the postcode. |  |

## Example

```json
{
  "id": "kadaster_1742010000016637|1742200000045935",
  "dataset": "kadaster",
  "country": "Netherlands",
  "country_iso": "NLD",
  "country_iso_2": "NL",
  "line_1": "Oude Veemarkt 25",
  "language": "nl",
  "address": "25",
  "identificatie": "1742010000016637",
  "latitude": 52.309501578434144,
  "longitude": 6.524052774641579,
  "gebruiksdoel": "bijeenkomstfunctie",
  "oppervlakte": 532,
  "status": "Verblijfsobject in gebruik",
  "geconstateerd": false,
  "documentdatum": "2023-11-09T00:00:00.000Z",
  "documentnummer": "D2023167157",
  "voorkomenidentificatie": 2,
  "begin_geldigheid": "2023-11-09T00:00:00.000Z",
  "eind_geldigheid": "",
  "tijdstip_registratie": "2023-11-09T14:42:11.635Z",
  "eind_registratie": "",
  "tijdstip_registratie_lv": "2023-11-09T14:55:36.476Z",
  "tijdstip_eind_registratie_lv": "",
  "nummeraanduidingen_identificatie": "1742200000045935",
  "nummeraanduidingen_huisnummer": "25",
  "nummeraanduidingen_huisnummertoevoeging": "",
  "nummeraanduidingen_huisletter": "",
  "nummeraanduidingen_postcode": "7461 GJ",
  "nummeraanduidingen_type_adresseerbaar_object": "Verblijfsobject",
  "nummeraanduidingen_status": "Naamgeving uitgegeven",
  "nummeraanduidingen_geconstateerd": false,
  "nummeraanduidingen_documentdatum": "2009-05-13T00:00:00.000Z",
  "nummeraanduidingen_documentnummer": "D2009021777",
  "nummeraanduidingen_voorkomenidentificatie": 1,
  "nummeraanduidingen_begin_geldigheid": "2009-05-13T00:00:00.000Z",
  "nummeraanduidingen_eind_geldigheid": "",
  "nummeraanduidingen_tijdstip_registratie": "2010-10-22T16:46:11.000Z",
  "nummeraanduidingen_eind_registratie": "",
  "nummeraanduidingen_tijdstip_registratie_lv": "2010-10-25T10:37:53.434Z",
  "nummeraanduidingen_tijdstip_eind_registratie_lv": "",
  "pand_identificatie": "1742100000015838",
  "pand_oorspronkelijk_bouwjaar": 1920,
  "pand_status": "Pand in gebruik",
  "pand_geconstateerd": false,
  "pand_documentdatum": "1920-05-18T00:00:00.000Z",
  "pand_documentnummer": "2475-000V",
  "pand_voorkomenidentificatie": 1,
  "pand_begin_geldigheid": "1920-05-18T00:00:00.000Z",
  "pand_eind_geldigheid": "",
  "pand_tijdstip_registratie": "2010-10-22T16:04:09.000Z",
  "pand_eind_registratie": "",
  "pand_tijdstip_registratie_lv": "2010-10-25T10:34:22.804Z",
  "pand_tijdstip_eind_registratie_lv": "",
  "openbare_ruimte_identificatie": "1742300000000446",
  "openbare_ruimte_naam": "Oude Veemarkt",
  "openbare_ruimte_type": "Weg",
  "openbare_ruimte_status": "Naamgeving uitgegeven",
  "openbare_ruimte_geconstateerd": false,
  "openbare_ruimte_documentdatum": "1994-11-22T00:00:00.000Z",
  "openbare_ruimte_documentnummer": "RSN_STR_1937-2000",
  "openbare_ruimte_voorkomenidentificatie": 1,
  "openbare_ruimte_begin_geldigheid": "1994-11-22T00:00:00.000Z",
  "openbare_ruimte_eind_geldigheid": "",
  "openbare_ruimte_tijdstip_registratie": "2010-10-22T15:40:31.000Z",
  "openbare_ruimte_eind_registratie": "",
  "openbare_ruimte_tijdstip_registratie_lv": "2010-10-25T10:32:44.940Z",
  "openbare_ruimte_tijdstip_eind_registratie_lv": "",
  "openbare_ruimte_verkorte_naam": "",
  "woonplaats_identificatie": "1566",
  "woonplaats_naam": "Rijssen",
  "woonplaats_status": "Woonplaats aangewezen",
  "woonplaats_geconstateerd": false,
  "woonplaats_documentdatum": "2008-12-15T00:00:00.000Z",
  "woonplaats_documentnummer": "Raad 15-12-2008/17",
  "woonplaats_voorkomenidentificatie": 1,
  "woonplaats_begin_geldigheid": "2008-12-15T00:00:00.000Z",
  "woonplaats_eind_geldigheid": "",
  "woonplaats_tijdstip_registratie": "2010-10-22T15:40:19.000Z",
  "woonplaats_eind_registratie": "",
  "woonplaats_tijdstip_registratie_lv": "2010-10-25T10:32:43.439Z",
  "woonplaats_tijdstip_eind_registratie_lv": "",
  "provincie": "Overijssel"
}
```
