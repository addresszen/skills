# Licensee

**Schema name:** `Licensee`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `name` | yes | string | Licensee individual or organisation name | `Qwerty Widgets Limited` |
| `address` | yes | string | Licensee's first, second and third line address as well as post town concatenated by commas | `12 High Street, Manchester` |
| `postcode` | yes | string | Licensee's postcode | `ID1 1QD` |
| `whitelist` | yes | array<string> | A list of allowed URLs. An empty list means that whitelisting is disabled |  |
| `daily` | yes | object |  |  |
| `id` | yes | string | An immutable ID provided for every licensee. Primarily used for paginated list requests. | `56a11209ebe230380bf104c3` |
| `key` | yes | string | Uniquely identifies a licensee for a key. | `sl_ijoiqsxeQgXW2gkiE0X94` |
| `createdAt` | yes | string | Timestamp for when the licensee was created | `2016-01-21T17:14:49.971Z` |

## Used By

- [ListLicensees](../endpoints/list-licensees.md)
- [CreateLicensee](../endpoints/create-licensee.md)
- [RetrieveLicensee](../endpoints/retrieve-licensee.md)
- [UpdateLicensee](../endpoints/update-licensee.md)
