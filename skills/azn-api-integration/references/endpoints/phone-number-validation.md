# Phone Number Validation

**Endpoint:** `GET /phone_numbers`

**Operation ID:** `PhoneNumberValidation`

**Tags:** Phone Numbers

Query for and validate phone numbers.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `query` | query | yes | string | Specifies the phone number to validate. Phone number must include a country code in acceptable format. For instance, UK phone numbers should be suffixed `+44`, `44` or `0044`. |
| `current_carrier` | query | no | `true` | When set to `true` the current network of the phone number will be retrieved and populated. |
| `tags` | query | no | string | A comma separated list of tags to query over. |

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `code` | yes | integer |  |
| `message` | yes | string |  |
| `result` | yes |  |  |

## Response Example

```json
{
  "result": {
    "valid": true,
    "national_format": "020 7112 8019",
    "international_format": "+44 20 7112 8019",
    "iso_country": "GBR",
    "iso_country_2": "GB",
    "country": "United Kingdom",
    "current_carrier": {
      "network_code": null,
      "name": "Invomo Ltd",
      "country": "GB",
      "network_type": "landline"
    },
    "original_carrier": {
      "network_code": null,
      "name": "Invomo Ltd",
      "country": "GB",
      "network_type": "landline"
    }
  },
  "code": 2000,
  "message": "Success"
}
```

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 400 |  | Bad Request |
| 401 |  | Unauthorized |
| 429 |  | Rate Limit Timeout |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/phone-number-validation)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
