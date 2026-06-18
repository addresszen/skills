# Email Validation

**Endpoint:** `GET /emails`

**Operation ID:** `EmailValidation`

**Tags:** Emails

Query for and validate email addresses.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `query` | query | yes | string | Specifies the email address to validate |
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
    "result": "deliverable",
    "deliverable": true,
    "catchall": false,
    "free": false,
    "role": true,
    "disposable": false,
    "suggestions": []
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

## See also

- [Live docs](https://docs.addresszen.com/docs/api/email-validation)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
