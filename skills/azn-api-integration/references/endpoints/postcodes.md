# Lookup Postcode

**Endpoint:** `GET /postcodes/{postcode}`

**Operation ID:** `Postcodes`

**Tags:** UK

Returns the complete list of addresses for a postcode. Postcode searches are space and case insensitive.

The Postcode Lookup API provides a JSON interface to search UK addresses from a postcode. It can be used to power Address Lookup driven address searches, like [Address Lookup](/docs/address-lookup/).

## Postcode Not Found

Lookup balance is unaffected by invalid postcodes. The API returns a `404` response with response body:

```json
{
  "code": 4040,
  "message": "Postcode not found",
  "suggestions": ["SW1A 0AA"]
}
```

### Suggestions

If a postcode cannot be found, the API will provide up to 5 closest matching postcodes. Common errors will be corrected first (e.g. mixing up `O` and `0` or `I` and `1`).

If the suggestion list is small (fewer than 3), there is a high probability the correct postcode is there. You may notify the user or immediately trigger new searches.

The suggestion list will be empty if the postcode has deviated too far from a valid postcode format.

## Multiple Residence

A small number of postcodes will return more than 100 premises. These may require pagination. Use `page` to paginate the result set.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `postcode` | path | yes | string | Postcode to retrieve |
| `filter` | query | no | string | Comma separated whitelist of address elements to return. |
| `page` | query | no | integer | 0 indexed indicator of the page of results to receive. Virtually all postcode results are returned on page 0. |
| `tags` | query | no | string | A comma separated list of tags to query over. |

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | array<oneOf> | All addresses listed at the postcode. |
| `code` | yes | integer |  |
| `message` | yes | string |  |
| `page` | yes | integer |  |
| `limit` | yes | integer |  |
| `total` | yes | integer |  |

## Response Example

```json
{
  "result": [
    {
      "postcode": "SW1A 2AA",
      "postcode_inward": "2AA",
      "postcode_outward": "SW1A",
      "post_town": "London",
      "dependant_locality": "",
      "double_dependant_locality": "",
      "thoroughfare": "Downing Street",
      "dependant_thoroughfare": "",
      "building_number": "10",
      "building_name": "",
      "sub_building_name": "",
      "po_box": "",
      "department_name": "",
      "organisation_name": "Prime Minister & First Lord Of The Treasury",
      "udprn": 23747771,
      "postcode_type": "L",
      "su_organisation_indicator": "",
      "delivery_point_suffix": "1A",
      "line_1": "Prime Minister & First Lord Of The Treasury",
      "line_2": "10 Downing Street",
      "line_3": "",
      "premise": "10",
      "longitude": -0.12767,
      "latitude": 51.503541,
      "eastings": 530047,
      "northings": 179951,
      "country": "England",
      "traditional_county": "Greater London",
      "administrative_county": "",
      "postal_county": "London",
      "county": "London",
      "district": "Westminster",
      "ward": "St. James's",
      "uprn": "100023336956",
      "id": "paf_23747771",
      "country_iso": "GBR",
      "country_iso_2": "GB",
      "county_code": "",
      "language": "en",
      "umprn": "",
      "dataset": "paf"
    }
  ],
  "code": 2000,
  "message": "Success",
  "limit": 100,
  "page": 0,
  "total": 1
}
```

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 400 |  | Bad Request |
| 404 | 4040 | Postcode not found |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/postcodes)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
