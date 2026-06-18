# Cleanse Address

**Endpoint:** `POST /cleanse/addresses`

**Operation ID:** `AddressCleanse`

**Tags:** UK

The address cleanse API attempts to return the closest matching address for any given address inputs. We also return a number of Match Level indicators that describe the degree to which the suggested address matches the input address. The more impaired the input address, the harder it is to cleanse.

## Confidence Score

The confidence score is a number ranging between 0 and 1. Where 1 implies a full match and 0 implies no major elements completely match. Each incorrect, missing or misspelled element will subtract from the overall confidence score.

### Deciding on an Acceptable Confidence Score Threshold

Different address cleanse projects can have radically different inputs. However, within each project, the inputs tend to repeat the same errors. For instance, some input datasets may be exclusively inputted manually and be prone to typos. Others may have a persistently missing datapoint such as organization name or postcode. For this reason, it is important to understand that there is no absolute Confidence Score threshold. Instead, the acceptable confidence score must be determined on a project by project basis based on systematic errors present in the data and business goals.

When determining an acceptable Confidence Score threshold you should load a subset of the dataset into a spreadsheet application like Excel and sort on the score. Scrolling from top-to-bottom you will be able to observe matches from best to worst. As you start to hit the lower quality searches, you will be able to roughly determine:
 - Which confidence scores indicate ambiguous matches (i.e. up to building level only)
- Which confidence scores indicate a poor or no match (i.e. the nearest matching address is too far from the input address)

Depending on your business goals, you can also use the Match Levels to determine an acceptable match. For instance, do you need to match up to the thoroughfare or building name only? Are accurate organization names an important feature?

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `tags` | query | no | string | A comma separated list of tags to query over. |
| `context` | query | no | string | Identify the country of the address to cleanse. Defaults to UK (GBR) |

## Request Body

Content-Type: `application/json` (required)

| Field | Required | Type | Description |
|---|---|---|---|
| `query` | yes | string | Freeform address input to cleanse |
| `postcode` | no | string | Optionally specify postal code for the address. |
| `post_town` | no | string | Optionally specify the city or town of the address. |
| `county` | no | string | Optionally specify the county or state of the address. |

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `code` | yes | integer |  |
| `message` | yes | string |  |
| `result` | yes |  |  |

## Error Status Codes

| HTTP | Code | Message |
|---|---|---|
| 400 |  | Bad Request |
| 401 |  | Unauthorized |
| 429 |  | Rate Limited |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/address-cleanse)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
