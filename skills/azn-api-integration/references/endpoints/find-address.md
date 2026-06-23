# Find Address

**Endpoint:** `GET /autocomplete/addresses`

**Operation ID:** `FindAddress`

**Tags:** Address Search

The Address Autocomplete API delivers address suggestions in order of relevance based on a provided query. It aids real-time address autofill implementations.

Consider using our Address Autocomplete JavaScript libraries to add address lookup to a form in moments rather than interacting with this API directly.

## API Usage

Implementing our Address Autocomplete API involves:

1. Fetch address suggestions with `/autocomplete/addresses`
2. Acquire the complete address using the ID from the suggestion

Step 2 will decrement your lookup balance.

Note that step 1 is not a free standalone resource. Integrations that consistently make autocomplete requests without a paid Step 2 request will be rate limited and then suspended.

## Query Filters

Refine results by appending filters to your querystring, e.g., `postcode=sw1a2aa` for postcode `SW1A 2AA`. Invalid filters return an empty set without affecting your lookup count.

To apply multiple filter terms, use a comma-separated list, e.g., `postcode_outward=e1,e2,e3` combines result sets for E1, E2, and E3. Unless otherwise specified, all filters support multiple terms.

Combine filters by `AND` logic, for instance, `su_organisation_indicator=Y&postcode_area=n`. The maximum allowed filter terms is **10**.

## Address Bias

Preface bias searches with `bias_` to boost certain address results. Unlike filters, biasing allows unmatched addresses to appear with lower priority.

For example, use `bias_postcode_area=SW,SE` to favor addresses in the `SW` and `SE` postcode areas. Invalid bias terms have no effect.

Multiple bias terms are allowed unless stated otherwise, with a combined maximum of **5**.

## Suggestion Format

The suggestion format is subject to change. We recommend using the suggestion as-is to prevent potential integration issues.

## Rate Limiting and Cost

The rate limit for the Autocomplete API is 3000 requests per 5 minutes. HTTP Headers inform about the current rate limit.

Autocomplete API usage does not impact your balance, but resolving a suggestion to a full address requires a paid request. Autocomplete requests without subsequent paid requests may result in rate limitation or suspension.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `query` | query | no | string | The partial address string entered by the user to autocomplete. |
| `dataset` | query | no | array | Comma-separated list of datasets to search within. |
| `context` | query | no | string | Limits search results, typically within a country. |
| `limit` | query | no | integer | Specifies the maximum number of records to retrieve. |
| `bias_lonlat` | query | no | string | Bias search to a geospatial circle determined by an origin and radius in meters. Max radius is `50000`. |
| `bias_ip` | query | no | `true` | Biases search based on approximate geolocation of IP address. |
| `box` | query | no | string | Restrict search to a geospatial box determined by the "top-left" and "bottom-right" gelocations. |
| `postcode_outward` | query | no | string | Restrict result set to addresses with a matching outward code. |
| `postcode` | query | no | string | Restrict result set to matching postcodes only. |
| `postcode_area` | query | no | string | Postcode area represents the first one or two non-numeric characters of a postcode. E.g. the postcode area of `SW1A 2AA` is `SW`. |
| `postcode_sector` | query | no | string | Postcode sector is the outward code plus first numeric of the inward code. E.g. postcode sector of `SW1A 2AA` is `SW1A 2` |
| `post_town` | query | no | string | Restrict addresses to matching town, city or other locality identifier. |
| `uprn` | query | no | integer | Does not accept comma separated terms. Only a single term is permitted |
| `country` | query | no | string | Filters by country name. |
| `postcode_type` | query | no | string | Filter by Postcode Type. Useful for separating organisational and residential addresses |
| `su_organisation_indicator` | query | no | string | Useful for separating organisational and residential addresses |
| `bias_postcode_outward` | query | no | string | Boosts addresses with a matching outward code. |
| `bias_postcode` | query | no | string | Boost addresses which match postcode. |
| `bias_postcode_area` | query | no | string | Boosts if the first one or two non-numeric characters of a postcode match |
| `bias_postcode_sector` | query | no | string | Boost postcode sector matches. The postcode sector comprises the outward code plus first numeric of the inward code. |
| `bias_post_town` | query | no | string | Biases results to matching town, city or other locality name. |
| `bias_thoroughfare` | query | no | string | Bias by street or thoroughfare name. |
| `bias_country` | query | no | string | Possible values are England, Scotland, Wales, Northern Ireland, Jersey, Guernsey and Isle of Man. |

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `result` | yes | object |  |
| `code` | yes | integer |  |
| `message` | yes | string |  |

## Response Example

```json
{
  "result": {
    "hits": [
      {
        "id": "paf_23747771",
        "suggestion": "Prime Minister & First Lord Of The Treasury, 10 Downing Street, London, SW1A",
        "udprn": 23747771,
        "urls": {
          "udprn": "/v1/udprn/23747771"
        }
      },
      "… 1 more items …"
    ]
  },
  "code": 2000,
  "message": "Success"
}
```

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 400 |  | Bad Request |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/find-address)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
