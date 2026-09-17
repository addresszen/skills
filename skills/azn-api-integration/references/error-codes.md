# Error Codes and Common Fixes

Every error the API can return, with the cause and the fix. The four most common are first. The full list follows, grouped by HTTP status.

## Response shape

Every response carries a numeric `code` and a `message`. A successful request returns HTTP 200 with `code` 2000. An error returns the matching HTTP status and a code that starts with that status.

```json
{
  "code": 4010,
  "message": "Invalid Key"
}
```

Check `code`, not the message text. Request validation failures (`code` 4000 on the validated endpoints) add `errors`, an array of `{ path, message }` naming each invalid field.

With a JSONP `callback` parameter the API returns every error with HTTP 200, so read `code` from the body rather than relying on the status.

## Summary

| Code | HTTP | Meaning |
|---|---|---|
| [4000](#4000) | 400 | Invalid syntax or failed request validation |
| [4001](#4001) | 400 | Submitted data failed validation |
| [4005](#4005) | 400 | Invalid end date |
| [4006](#4006) | 400 | Invalid start date |
| [4007](#4007) | 400 | Start date is after end date |
| [4008](#4008) | 400 | Date range over 90 days |
| [4009](#4009) | 400 | More than 3 tags queried |
| [40010](#40010) | 400 | Invalid source IP address |
| [40011](#40011) | 400 | Invalid search query |
| [40012](#40012) | 400 | Pagination beyond 10,000 results |
| [40013](#40013) | 400 | Too many biases |
| [40014](#40014) | 400 | Too many filters |
| [40016](#40016) | 400 | Invalid filter or bias value |
| [40017](#40017) | 400 | Email query too long |
| [40018](#40018) | 400 | Missing query |
| [4010](#4010) | 401 | Invalid key |
| [4011](#4011) | 401 | URL or IP not on allowed list, or missing user token |
| [4012](#4012) | 401 | Key not owned by user token |
| [4013](#4013) | 401 | Sub-licensee key required |
| [4014](#4014) | 401 | Licensee belongs to another key |
| [4015](#4015) | 401 | Key not licensed for this data |
| [4020](#4020) | 402 | Balance depleted |
| [4021](#4021) | 402 | Lookup limit reached |
| [404](#404) | 404 | Page not found |
| [4042](#4042) | 404 | Key not found |
| [4045](#4045) | 404 | Licensee not found |
| [4047](#4047) | 404 | Config not found |
| [4048](#4048) | 404 | Address not found |
| [4100](#4100) | 410 | Signup link expired |
| [4150](#4150) | 415 | Unsupported media type |
| [4290](#4290) | 429 | Request timed out |
| [4291](#4291) | 429 | Too many requests |
| [5001](#5001) | 500 | Uncatalogued error |
| [5002](#5002) | 500 | Internal timeout |

## Common fixes

### 4010 - Invalid Key {#4010}

**Message:** `Invalid Key`
**HTTP Status:** 401

Your API Key was not recognised. The key may be incorrect or malformed.

#### Potential Fixes

1. **Check for typos** - copy the key directly from your AddressZen account.
2. **Check querystring parameter name** - ensure the key is passed as `api_key` and not `api-key`.
3. **Check Authorization header format** - ensure the header is formatted as `Authorization: api_key="ak_yourkey"` (key wrapped in double quotes).
4. **Check the key still exists** - a regenerated or deleted key stops working immediately.

### 4011 - URL Not on Allowed List {#4011}

**Message:** `Requesting URL not on whitelist` or `Forbidden`
**HTTP Status:** 401

`Requesting URL not on whitelist` means the request's `Referer` or `Origin` header did not match any URL on your key's allowed URL list. Sub-licensee keys apply their own allowed URLs in the same way.

`Forbidden` means one of two things. The request came from an IP address that is not on the key's IP allow list. Or a key management endpoint (`/v1/keys/:key/details`, `/usage`, `/lookups`, `/licensees`, `/configs`) received no `user_token`, or one it did not recognise.

#### Potential Fixes

1. **Check if you need Allowed URLs** - non-browser requests won't contain the `Referer` or `Origin` headers needed for matching. Remove Allowed URLs if the key is kept private (server-side).
2. **Review your Allowed URL configuration** - in your AddressZen account, confirm each allowed URL matches scheme + host exactly (e.g. `https://example.com`, no trailing slash, no path). `localhost` is allowed by default.
3. **Check the IP allow list** - if your key restricts IP addresses, add the address your servers send from.
4. **Send a valid user token** - key management endpoints need `user_token` as well as the key.

### 4020 - Balance Depleted {#4020}

**Message:** `Key balance depleted`
**HTTP Status:** 402

Your API Key has no remaining lookup balance.

#### Potential Fixes

1. **Top up your balance** - purchase more lookups from your AddressZen account.
2. **Enable automated top-ups** - prevent this from recurring by [enabling automated top-ups](https://docs.addresszen.com/docs/guides/automated-topups).

### 4021 - Lookup Limit Reached {#4021}

**Message:** `Lookup Limit Reached`
**HTTP Status:** 402

Your API Key has a daily or IP rate limit configured, and it has been reached. Four limits raise this error: the daily lookup limit, the monthly lookup limit, the individual (per IP address) daily limit and a sub-licensee's daily limit.

#### Potential Fixes

1. **Disable the rate limit** - remove the responsible limit in your key settings for an immediate fix.
2. **Increase the limit** - adjust the daily, monthly or individual limit in your key settings.
3. **Forward the end user's IP** - if requests reach us through a proxy, one address absorbs every user's lookups and trips the individual limit early. Enable IP address forwarding on the key and send `AZ-Source-IP`.
4. **Check the licensee's limit** - a sub-licensee key carries its own daily limit, separate from the parent key.

## 400 Bad Request

### 4000 - Invalid Syntax {#4000}

**Message:** `Invalid syntax submitted`, or a validation message such as `request/body/query must be string`
**HTTP Status:** 400

The API could not parse the request or the request failed validation. Causes:

- A POST or PUT body that is not valid JSON.
- Malformed percent-encoding in the URL.
- A failed schema check on `/v1/verify/addresses`, `/v1/emails`, `/v1/phone_numbers`, `/v1/sign_up` or the `/v1/keys/:key/details` and `/v1/keys/:key/configs` endpoints. These responses include an `errors` array naming each invalid field.

Fix the request body or parameter named in `message` or `errors`.

### 4001 - Validation Failed {#4001}

**Message:** `Validation failed on your submitted data` or a field-specific message
**HTTP Status:** 400

A write to your key failed validation. Raised by `PUT /v1/keys/:key/details`, the licensee create and update endpoints and the config create and update endpoints. An invalid monthly limit value also raises it. Check the field named in the message against the [API reference](https://docs.addresszen.com/docs/api/key-details).

### 4005 - Invalid End Date {#4005}

**Message:** `Invalid end date`
**HTTP Status:** 400

The `end` parameter on `/v1/keys/:key/usage` or `/v1/keys/:key/lookups` could not be parsed. Send an ISO 8601 date.

### 4006 - Invalid Start Date {#4006}

**Message:** `Invalid start date`
**HTTP Status:** 400

The `start` parameter on `/v1/keys/:key/usage` or `/v1/keys/:key/lookups` could not be parsed. Send an ISO 8601 date.

### 4007 - Start After End {#4007}

**Message:** `Invalid Date Range: start date is after end date`
**HTTP Status:** 400

On `/v1/keys/:key/usage` or `/v1/keys/:key/lookups`, `start` is later than `end`. Swap them.

### 4008 - Range Too Wide {#4008}

**Message:** `Invalid Date Range: range specified needs to be 90 days or less`
**HTTP Status:** 400

The `start` to `end` window on `/v1/keys/:key/usage` or `/v1/keys/:key/lookups` exceeds 90 days. Split the query into 90-day windows.

### 4009 - Too Many Tags {#4009}

**Message:** `Too Many Tags Queried: please specify no more than 3 tags to query`
**HTTP Status:** 400

`/v1/keys/:key/usage` accepts at most three `tags`. Query fewer tags per request.

### 40010 - Invalid Source IP {#40010}

**Message:** `Invalid source IP address provided`
**HTTP Status:** 400

The `AZ-Source-IP` header does not contain a valid IP address and your key has an individual lookup limit configured. Send a single valid IP address, or drop the header.

### 40011 - Invalid Search Query {#40011}

**Message:** `Invalid search query received`
**HTTP Status:** 400

The search backend rejected the query. On `/v1/emails` it means `query` was not a string. On the address search endpoints it means the query could not be executed. Simplify the query and retry.

### 40012 - Pagination Limit {#40012}

**Message:** `It is not possible to paginate beyond the first 10,000 results. Please contact support if you need to extract an exhaustive list of addresses`
**HTTP Status:** 400

`page` multiplied by `limit` reached 10,000 on a paginated search. Narrow the query with filters, or contact support for a bulk extract.

### 40013 - Too Many Biases {#40013}

**Message:** `Too many query biases requested. You may set up to 5 biases`
**HTTP Status:** 400

`/v1/autocomplete/addresses` accepts at most five bias terms. Remove the extras.

### 40014 - Too Many Filters {#40014}

**Message:** `Too many filters specified`
**HTTP Status:** 400

`/v1/autocomplete/addresses` accepts at most ten filter terms. Remove the extras.

### 40016 - Invalid Filter or Bias {#40016}

**Message:** `Invalid search query provided. Please review your inputs`
**HTTP Status:** 400

A filter or bias value could not be turned into a query, for example a malformed `bias_lonlat`. Check each filter and bias value against the [address search reference](https://docs.addresszen.com/docs/api/find-address).

### 40017 - Email Query Too Long {#40017}

**Message:** `Invalid email query string. Email string length is too long. Max length 320`
**HTTP Status:** 400

The `query` on `/v1/emails` is longer than 320 characters. Trim the input before sending it.

### 40018 - Missing Query {#40018}

**Message:** `Invalid query. The q or query parameter is required`
**HTTP Status:** 400

A search endpoint received no `query`, or a `query` that is not a string. Send the query as a string.

## 401 Unauthorized

Codes 4010 and 4011 are covered under [Common fixes](#common-fixes).

### 4012 - Key Not Owned {#4012}

**Message:** `Forbidden`
**HTTP Status:** 401

`GET /v1/keys/:key` received a `user_token` that does not own the key. Check both values against your AddressZen account.

### 4013 - Sub-licensee Key Required {#4013}

**Message:** `A Sub Licensee Key is required to perform this action`
**HTTP Status:** 401

The `/v1/keys/:key/licensees` endpoints were called on a key without sub-licensing, or a sub-licensed key made a lookup without a `licensee` parameter.

### 4014 - Licensee Belongs to Another Key {#4014}

**Message:** `Invalid API Key provided for licensee`
**HTTP Status:** 401

The `licensee` parameter names a licensee created under a different key. Send the licensee with its parent key.

### 4015 - Not Licensed for This Data {#4015}

**Message:** `Inadequate licence to access data. Your API Key is not licensed to access the data you attempted to query`
**HTTP Status:** 401

Your key has no dataset or service enabled for this endpoint. Raised by the address search endpoints when no address dataset is enabled, `/v1/verify/addresses` when address verification is off, `/v1/emails` when email validation is off and `/v1/phone_numbers` when phone validation is off. Enable the dataset or service in your key settings, or contact support if it is not available on your account.

## 402 Payment Required

Codes 4020 and 4021 are covered under [Common fixes](#common-fixes).

## 404 Not Found

### 404 - Page Not Found {#404}

**Message:** `404 Page not found`
**HTTP Status:** 404

No route matched the request. The code is `404`, not `4040`. Check the path and the HTTP method against the [API reference](https://docs.addresszen.com/docs/api/api-reference).

### 4042 - Key Not Found {#4042}

**Message:** `Key not found`
**HTTP Status:** 404

The key in a `/v1/keys/:key` path, or the licensee key it names, does not exist or has been deleted. Check the key against your AddressZen account.

### 4045 - Licensee Not Found {#4045}

**Message:** `No licensee found`
**HTTP Status:** 404

The `licensee` parameter, or the licensee id in a `/v1/keys/:key/licensees/:licensee` path, does not exist under this key. List licensees with `GET /v1/keys/:key/licensees`.

### 4047 - Config Not Found {#4047}

**Message:** `Config not found`
**HTTP Status:** 404

No config with that name exists under `/v1/keys/:key/configs/:config`. List configs with `GET /v1/keys/:key/configs`.

### 4048 - Address Not Found {#4048}

**Message:** `Address not found`
**HTTP Status:** 404

`/v1/autocomplete/addresses/:id/usa` or `/v1/places/:id` found nothing for the id. Ids come from a preceding autocomplete or places search. Check the id was copied in full.

## 410 Gone

### 4100 - Signup Link Expired {#4100}

**Message:** `Signup link has expired or has already been claimed. Please re-run signup`
**HTTP Status:** 410

The CLI signup link at `/v1/sign_up/:cli_token` has expired or was already used. Run the signup again to get a fresh link.

## 415 Unsupported Media Type

### 4150 - Unsupported Media Type {#4150}

**Message:** `Unsupported Media Type. Our POST, PATCH and PUT endpoints only support application/json`
**HTTP Status:** 415

A POST, PUT or PATCH request arrived without `Content-Type: application/json`. Set the header and send a JSON body.

## 429 Too Many Requests

### 4290 - Request Timed Out {#4290}

**Message:** `Request timed out. Please wait and try again later`
**HTTP Status:** 429

`/v1/verify/addresses` ran past 9.5 seconds, or `/v1/phone_numbers` waited too long for an upstream response. Retry after a short delay.

### 4291 - Too Many Requests {#4291}

**Message:** `Too many requests. Please contact support`
**HTTP Status:** 429

The request was flagged as high risk and the key is less than two days old. This protects new accounts from abuse. Contact support if it blocks a legitimate integration.

## 500 Internal Server Error

### 5001 - Uncatalogued Error {#5001}

**Message:** `Uncatalogued Error`
**HTTP Status:** 500

An error the API does not recognise. Retry once. If it persists, contact support with the request and the time it was made.

### 5002 - Internal Timeout {#5002}

**Message:** `Search request reached internal timeout limits`
**HTTP Status:** 500

A database query exceeded its time limit. Retry after a short delay. If it persists, contact support.
