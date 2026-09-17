# France BAN Address

Address from France's Base Adresse Nationale (BAN), the official open national
address database published via Etalab.

BAN reaches house-number level only (`numero` + street + commune) - it carries
no sub-premise (unit, floor, building) data.

**Schema name:** `BanAddress`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `id` | yes | string | Global unique internally generated identifier for an address |  |
| `dataset` | yes | `ban` |  |  |
| `country` | yes | `France` | Full country names (ISO 3166) |  |
| `country_iso` | yes | `FRA` | 3 letter country code (ISO 3166-1) |  |
| `country_iso_2` | yes | `FR` | 2 letter country code (ISO 3166-1) |  |
| `language` | yes | `fr` | Language represented by 2 letter ISO Code (639-1) |  |
| `address` | yes | string | The house number of the address (`numero`), without any suffix. |  |
| `line_1` | yes | string | First address line (house number, suffix, and street name). |  |
| `line_2` | yes | string | Second address line (postcode and municipality name). |  |
| `latitude` | yes | string \| number | The latitude of the address or postcode (WGS84). |  |
| `longitude` | yes | string \| number | The longitude of the address or postcode (WGS84). |  |
| `id_fantoir` | yes | string | FANTOIR street identifier |  |
| `numero` | yes | integer | House number |  |
| `rep` | yes | string | House number suffix / répétition (`bis`, `ter`, `quater`, etc.) |  |
| `nom_voie` | yes | string | Street name |  |
| `code_postal` | yes | string | 5-digit postal code |  |
| `code_insee` | yes | string | INSEE commune code (2-digit département + 3-digit commune) |  |
| `nom_commune` | yes | string | Municipality name |  |
| `code_insee_ancienne_commune` | yes | string | INSEE code of the pre-fusion commune (for merged municipalities) |  |
| `nom_ancienne_commune` | yes | string | Name of the pre-fusion commune (for merged municipalities) |  |
| `x` | yes | string | Lambert 93 easting coordinate |  |
| `y` | yes | string | Lambert 93 northing coordinate |  |
| `lon` | yes | string | Longitude (WGS84) as returned from source data |  |
| `lat` | yes | string | Latitude (WGS84) as returned from source data |  |
| `type_position` | yes | string | Positional accuracy type (`entrée`, `bâtiment`, `parcelle`, `délivrance postale`, etc.) |  |
| `alias` | yes | string | Address alias |  |
| `nom_ld` | yes | string | Lieu-dit (named place) label |  |
| `libelle_acheminement` | yes | string | Postal routing label |  |
| `nom_afnor` | yes | string | AFNOR-normalised street name |  |
| `source_position` | yes | string | Source of position data (`commune`, `IGN`, etc.) |  |
| `source_nom_voie` | yes | string | Source of street name data |  |
| `certification_commune` | yes | boolean | Whether the municipality has certified this address |  |
| `cad_parcelles` | yes | string | Cadastral parcel reference(s) |  |

## Example

```json
{
  "id": "ban_01002_w4ld4h_00006",
  "dataset": "ban",
  "country": "France",
  "country_iso": "FRA",
  "country_iso_2": "FR",
  "language": "fr",
  "address": "6",
  "line_1": "6 place du Pese Lait",
  "line_2": "01640 L'Abergement-de-Varey",
  "latitude": 46.005447,
  "longitude": 5.425179,
  "id_fantoir": null,
  "numero": 6,
  "rep": null,
  "nom_voie": "Place du Pese Lait",
  "code_postal": "01640",
  "code_insee": "01002",
  "nom_commune": "L'Abergement-de-Varey",
  "code_insee_ancienne_commune": null,
  "nom_ancienne_commune": null,
  "x": "887643.67",
  "y": "6547960.53",
  "lon": "5.425179",
  "lat": "46.005447",
  "type_position": "entrée",
  "alias": null,
  "nom_ld": null,
  "libelle_acheminement": "ABERGEMENT-DE-VAREY (L )",
  "nom_afnor": "PLACE DU PESE LAIT",
  "source_position": "commune",
  "source_nom_voie": "commune",
  "certification_commune": true,
  "cad_parcelles": "01002000AE0005"
}
```
