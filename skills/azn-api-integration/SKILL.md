---
name: azn-api-integration
description: |
  Use when integrating the AddressZen API directly via HTTP.
  Covers authentication (header + query forms), address autocomplete (find
  and retrieve), address verification against USPS CASS, places, email and
  phone validation, key/licensee/config admin, the US-shaped Address model
  with its `dataset` and `native` (raw dataset record) fields, the `context`
  country parameter, filters and biases, error codes, rate limits, and common
  gotchas around allowed URLs.
license: SEE LICENSE IN LICENSE
metadata:
  author: addresszen
  version: "0.1.0"
  homepage: https://addresszen.com
  source: https://github.com/addresszen/skills
  openclaw:
    primaryEnv: ADDRESSZEN_API_KEY
    envVars:
      - name: ADDRESSZEN_API_KEY
        required: true
        description: API key. Get one at addresszen.com
inputs:
  - name: ADDRESSZEN_API_KEY
    description: API key for the AddressZen API
    required: true
references:
  - authentication.md
  - error-codes.md
  - endpoints/
  - data/
---

# AddressZen API

Direct HTTP integration with the AddressZen API. Supports multiple client libraries and language SDKs. Defaults to US addresses, with worldwide coverage selected per request.

## Quick Start (fetch)

```javascript
const key = process.env.ADDRESSZEN_API_KEY;
const base = 'https://api.addresszen.com/v1';
const headers = { Authorization: `api_key="${key}"` };

// Autocomplete step 1 (free): suggestions as the user types (US by default)
const query = encodeURIComponent('1600 Pennsylvania Ave');
const find = await fetch(`${base}/autocomplete/addresses?query=${query}`, { headers });
const { result: { hits } } = await find.json(); // [{ id, suggestion, urls }]

// Autocomplete step 2 (one lookup): retrieve a suggestion id as an Address
const id = encodeURIComponent(hits[0].id);
const retrieve = await fetch(`${base}/autocomplete/addresses/${id}/usa`, { headers });
const { result: address } = await retrieve.json();
console.log(address.line_1, address.city, address.state, address.zip_code);
```

Alternatively, pass `?api_key=...` in the query string instead of the header.

## Quick Start (verify)

```javascript
// Verify a typed address against USPS CASS; only a match is charged
const response = await fetch(`${base}/verify/addresses`, {
  method: 'POST',
  headers: { ...headers, 'Content-Type': 'application/json' },
  body: JSON.stringify({ query: '1600 Pennsylvania Ave NW, Washington, DC 20500' }),
});
const { result } = await response.json();
if (result.count === 0) {
  // No match: result.match is null and the address fields are empty
} else {
  console.log(result.fit, result.confidence, result.match.zip_plus_4_code);
}
```

## Quick Start (axios)

```javascript
import axios from 'axios';

const client = axios.create({
  baseURL: 'https://api.addresszen.com/v1',
  headers: {
    Authorization: `api_key="${process.env.ADDRESSZEN_API_KEY}"`,
  },
});

const { data } = await client.get('/autocomplete/addresses', {
  params: { query: '1600 Pennsylvania Ave' },
});
console.log(data.result.hits);
```

## Core Endpoints

- `GET /autocomplete/addresses` - Typeahead address search. Free; the retrieve step is the paid lookup
- `GET /autocomplete/addresses/{address}/usa` - Retrieve a suggestion `id` as a full `Address`. Every address, whatever its country or dataset, comes back in the same US-shaped format
- `POST /verify/addresses` - Verify and standardize an address against USPS CASS
- `GET /places` / `GET /places/{place}` - Place search and resolve
- `GET /emails`, `GET /phone_numbers` - Email and phone validation

See [`endpoints/`](./references/endpoints/) for one reference per operation, including key, licensee and config admin.

## Filters, Biases and Context

- **`context`** - each search runs in one country. A missing or unrecognized `context` falls back to your account default. Example: `context=USA`
- **`dataset`** - narrows the search where a key has more than one dataset for a country
- **Filters** restrict results: `postal_code` (full ZIP+4), `postal_code_2` (three digit ZIP prefix), `postal_code_3` (five digit ZIP), `city`, `state`, `state_code`, `is_pobox`, `is_business`. Filters combine with `AND`; a comma-separated value accepts any of its terms (`postal_code_3=11225,11226`). At most 10 filter terms. An unmatched filter returns an empty set and an unknown filter name is ignored, neither costs a lookup
- **Biases** promote rather than restrict: prefix a filter name with `bias_` (`bias_state_code=NY,NJ`), or use `bias_lonlat` for proximity to a point. Unmatched addresses still appear, lower down. At most 5 bias terms

## Address Shape

- Every address is returned as `Address`, whatever dataset it came from: `line_1`, `line_2`, `last_line`, `city`, `state`, `state_abbreviation`, `zip_code`, `zip_plus_4_code` and the USPS delivery fields. See [`data/address.md`](./references/data/address.md)
- **`dataset`** names the source (`usps` by default). Fields a dataset does not carry are returned as empty strings (`""`), never `null`
- **`native`** is the raw dataset record, returned by Retrieve Address. Its shape depends on `dataset`: a `usps` address carries a [`UspsAddress`](./references/data/usps-address.md). Every record type has a reference under [`data/`](./references/data/), each with a field table and an example
- A suggestion's `suggestion` string is for display and may change format. Do not parse it; retrieve the address instead

## Verify Address

- Send `query` alone (the whole address), or the first line in `query` plus either `zip_code`, or `city` and `state`
- A match returns the standardized lines, `city`, `state`, ZIP+4, a `fit` and `confidence` score (0 to 1) and the CASS record in `match`: delivery point, DPV flags, carrier route, county, congressional district, coordinates. See [`data/usa-verify-match.md`](./references/data/usa-verify-match.md) and [`data/usa-cass-verified-address.md`](./references/data/usa-cass-verified-address.md)
- No match is still `200`, with `count: 0`, `match: null` and empty address fields. See [`data/usa-verify-no-match.md`](./references/data/usa-verify-no-match.md)
- Only a match draws on your balance
- `401` means verification is not enabled on the key. `429` means the verification ran past 9.5 seconds and was aborted

## Critical Gotchas

- **Auth header format** - `Authorization: api_key="<your-key>"` (with double quotes around the key). Not `Bearer`, not `ApiKey <key>`. Query-string `?api_key=...` also works
- **API key restrictions** - default keys are restricted to specific domains. Ensure your domain is in the key's allowed list
- **Rate limits** - each IP is rate limited at 30 requests per second. Tripping the limit returns a 503. Autocomplete adds its own limit of 3,000 requests per 5 minutes per key and IP, reported in the `X-RateLimit-Limit`, `X-RateLimit-Remaining` and `X-RateLimit-Reset` headers. Code `4021` (HTTP 402) is different: the key's own daily or per-IP lookup limit, set in your key settings
- **Free find, paid retrieve** - suggestions cost nothing; retrieving one costs a lookup. Keys that find without ever retrieving are rate limited, then suspended
- **Retrieve by `id`** - pass the suggestion's `id` to the retrieve endpoint. An `id` that resolves to no address returns `404` (code `4048`)
- **Error responses** - all errors are JSON with a numeric `code` and human-readable `message`. Check codes before retrying - see [`error-codes.md`](./references/error-codes.md)

## Reference Layout

- [`authentication.md`](./references/authentication.md) - header and query auth, key restrictions
- [`error-codes.md`](./references/error-codes.md) - error code catalogue with fixes
- [`endpoints/`](./references/endpoints/) - one reference per API operation: parameters, request body, curl samples, response schema, response example, status codes
- [`data/`](./references/data/) - one reference per data model (`Address`, the verify match, every `native` dataset record, suggestions, key admin) with field tables, an example and "used by" cross-links

## Full Spec

The complete OpenAPI spec is available at:

- npm: `@addresszen/openapi`
- web: <https://openapi.addresszen.com/openapi.yaml>

Reach for it when you need exhaustive parameter detail beyond what's in the endpoint references.

## Full documentation

The full AddressZen documentation - every guide, API reference, and integration - is available as a single file at [llms.txt](https://docs.addresszen.com/llms.txt). Point your agent there for anything this skill doesn't cover.
