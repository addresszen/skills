# Norway Kartverket Address

An address from Matrikkelen, Norway's official cadastre and address register, published by Kartverket (the Norwegian Mapping Authority).

Covers Norway (`NOR`) and Svalbard and Jan Mayen (`SJM`). Records come from the cadastre address, apartment level and road address files, so the fields available depend on which file the address came from. Any field which is not present is returned as an empty string `""`.

**Schema name:** `KartverketAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | `kartverket` |  |  |
| `country` | yes | `Norway` \| `Svalbard and Jan Mayen` | Full country names (ISO 3166) |  |
| `country_iso` | yes | `NOR` \| `SJM` | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | `NO` \| `SJ` | 2 letter country code (ISO 3166-1) |  |
| `line_1` | yes | string | First address line. `adressetilleggsnavn` where present, otherwise the official address text without it. |  |
| `line_2` | yes | string | Second address line. The official address text without `adressetilleggsnavn`, where line 1 carries that name. |  |
| `language` | yes | `no` | Language represented by 2 letter ISO Code (639-1) |  |
| `address` | yes | string | Number uniquely identifying the address within its street or farm. `nummer` and `bokstav` for a vegadresse, otherwise the cadastral `gardsnummer`/`bruksnummer`. Any `bruksenhetsnummer_tekst` is appended after a hyphen. |  |
| `latitude` | yes | string \| number | The latitude of the address or postcode (WGS84). |  |
| `longitude` | yes | string \| number | The longitude of the address or postcode (WGS84). |  |
| `lokal_id` | yes | string | Local identifier assigned by the data supplier. |  |
| `kommunenummer` | yes | string | Kommune (municipality) number. |  |
| `kommunenavn` | yes | string | Kommune (municipality) name. |  |
| `adressetype` | yes | string | `vegadresse` = street address, `matrikkeladresse` = land registry address |  |
| `adressetilleggsnavn` | yes | string | A local place name used in a road address. |  |
| `adressetilleggsnavn_kilde` | yes | string | Code for adressetilleggsnavn origin. |  |
| `adressekode` | yes | string \| integer |  |  |
| `adressenavn` | yes | string | Name of street, road, path, place or area entered in the land register. |  |
| `nummer` | yes | string \| integer |  |  |
| `bokstav` | yes | string | A subsequent letter that may be used in addition to a number. |  |
| `gardsnummer` | yes | integer | The number of a farm unit in the land register, unique within each municipality. |  |
| `bruksnummer` | yes | integer | A unique identification number automatically assigned to each individual unit within a farm. |  |
| `festenummer` | yes | string \| integer |  |  |
| `seksjonsnummer` | yes | string \| integer |  |  |
| `undernummer` | yes | string \| integer |  |  |
| `adresse_tekst` | yes | string | Official address text without bruksenhetsnummer, unique within a kommune. |  |
| `adresse_tekst_uten_adressetilleggsnavn` | yes | string | Official address text without bruksenhetsnummer and adressetilleggsnavn, unique within a kommune. |  |
| `bruksenhet_id` | yes | string | Local identifier for a unit within a building. |  |
| `bruksenhetsnummer_tekst` | yes | string | Unit number, e.g. an apartment in a multi-dwelling building. |  |
| `offisiell_adresse_tekst` | yes | string | Official address text with bruksenhetsnummer, unique within a kommune. |  |
| `offisiell_adresse_tekst_uten_adressetilleggsnavn` | yes | string | Official address text with bruksenhetsnummer and without adressetilleggsnavn, unique within a kommune. |  |
| `epsg_kode` | yes | integer | EPSG code of the coordinate reference system used by `nord` and `oest`. `25833` = EUREF89 UTM zone 33. |  |
| `nord` | yes | string | Northward (northing) coordinate of address, in the coordinate reference system given by `epsg_kode`. |  |
| `oest` | yes | string | Eastward (easting) coordinate of address, in the coordinate reference system given by `epsg_kode`. |  |
| `postnummer` | yes | string | Postal code. |  |
| `poststed` | yes | string | Name of postal town according to Posten. |  |
| `grunnkretsnummer` | yes | string | Identifier consisting of 8 digits, where the first four are the kommunenummer, the next two are the delområdenummer and the last two indicate the grunnkrets. |  |
| `grunnkretsnavn` | yes | string | Official grunnkrets name from Statistics Norway (SSB). |  |
| `soknenummer` | yes | string | Unique 8 digit identifier of a parish. |  |
| `soknenavn` | yes | string | Parish name. |  |
| `organisasjonsnummer` | yes | string | Unique identifier of organisation in the Brønnøysund Register. |  |
| `tettstednummer` | yes | string | 4 digit code for tettsted (urban settlement). |  |
| `tettstednavn` | yes | string | Name of tettsted (urban settlement). |  |
| `valgkretsnummer` | yes | string \| integer |  |  |
| `valgkretsnavn` | yes | string | Name of constituency. |  |
| `oppdateringsdato` | yes | string | Date of last change to the object data. |  |
| `datauttaksdato` | yes | string | Date of extraction from database. |  |
| `adresse_id` | yes | string | Address local identifier assigned by the data supplier. |  |
| `uuid_adresse` | yes | string | Address identifier realised as UUID managed by the cadastral system. |  |
| `uuid_bruksenhet` | yes | string | Unit of usage identifier realised as UUID managed by the cadastral system. |  |
| `atkomst_id` | yes | string | Local identifier for means of access to a property. |  |
| `uuid_atkomst` | yes | string | Identifier of the means of access to a property realised as UUID in the cadastral system. |  |
| `atkomst_nord` | yes | string | Northward coordinate of the means of access to a property. |  |
| `atkomst_oest` | yes | string | Eastward coordinate of the means of access to a property. |  |
| `sommeratkomst_id` | yes | string | Local identifier for means of access to a property in summer. |  |
| `uuid_sommeratkomst` | yes | string | Identifier of the means of access to a property in summer realised as UUID in the cadastral system. |  |
| `sommeratkomst_nord` | yes | string | Northward coordinate of the means of access to a property in summer. |  |
| `sommeratkomst_oest` | yes | string | Eastward coordinate of the means of access to a property in summer. |  |
| `vinteratkomst_id` | yes | string | Local identifier for means of access to a property in winter. |  |
| `uuid_vinteratkomst` | yes | string | Identifier of the means of access to a property in winter realised as UUID in the cadastral system. |  |
| `vinteratkomst_nord` | yes | string | Northward coordinate of the means of access to a property in winter. |  |
| `vinteratkomst_oest` | yes | string | Eastward coordinate of the means of access to a property in winter. |  |
| `fylke` | yes | string | Name of county. Derived from `kommunenummer`. |  |
| `landsdel` | yes | string | Name of region. Derived from `fylke`. |  |

## Example

```json
{
  "id": "kartverket_12204178!",
  "dataset": "kartverket",
  "country": "Norway",
  "country_iso": "NOR",
  "country_iso_2": "NO",
  "line_1": "Skollerud",
  "line_2": "278/177",
  "language": "no",
  "address": "278/177",
  "latitude": 60.31858180575511,
  "longitude": 10.03680377688277,
  "lokal_id": "12204178",
  "kommunenummer": "3305",
  "kommunenavn": "Ringerike",
  "adressetype": "matrikkeladresse",
  "adressetilleggsnavn": "Skollerud",
  "adressetilleggsnavn_kilde": "matrikkeladressenavn",
  "adressekode": "",
  "adressenavn": "",
  "nummer": "",
  "bokstav": "",
  "gardsnummer": 278,
  "bruksnummer": 177,
  "festenummer": "",
  "seksjonsnummer": "",
  "undernummer": "",
  "adresse_tekst": "Skollerud, 278/177",
  "adresse_tekst_uten_adressetilleggsnavn": "278/177",
  "bruksenhet_id": "",
  "bruksenhetsnummer_tekst": "",
  "offisiell_adresse_tekst": "",
  "offisiell_adresse_tekst_uten_adressetilleggsnavn": "",
  "epsg_kode": 25833,
  "nord": "6697211.61",
  "oest": "226005.30",
  "postnummer": "3516",
  "poststed": "Hønefoss",
  "grunnkretsnummer": "33050801",
  "grunnkretsnavn": "Skollerud",
  "soknenummer": "04070402",
  "soknenavn": "Hval",
  "organisasjonsnummer": "976989880",
  "tettstednummer": "",
  "tettstednavn": "",
  "valgkretsnummer": 11,
  "valgkretsnavn": "Hallingby",
  "oppdateringsdato": "2024-01-01T00:00:00.000Z",
  "datauttaksdato": "2024-04-15T07:59:32.000Z",
  "adresse_id": "12204178",
  "uuid_adresse": "3db4e8f2-fc63-5abe-9e0d-f53045166412",
  "uuid_bruksenhet": "",
  "atkomst_id": "",
  "uuid_atkomst": "",
  "atkomst_nord": "",
  "atkomst_oest": "",
  "sommeratkomst_id": "",
  "uuid_sommeratkomst": "",
  "sommeratkomst_nord": "",
  "sommeratkomst_oest": "",
  "vinteratkomst_id": "",
  "uuid_vinteratkomst": "",
  "vinteratkomst_nord": "",
  "vinteratkomst_oest": "",
  "fylke": "Buskerud",
  "landsdel": "Østlandet"
}
```
