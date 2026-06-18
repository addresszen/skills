---
name: azn-api-integration
description: |
  Use when integrating the AddressZen API directly via HTTP.
  Covers authentication (header + query forms), the core lookup endpoints
  (postcodes, autocomplete, places, cleanse), key/licensee/config admin,
  data models (PafAddress, MrAddress, AddressSuggestion, etc.), error
  codes, rate limits, and common gotchas around CORS and allowed URLs.
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

Direct HTTP integration with the AddressZen API. Supports multiple client libraries and language SDKs. Defaults to US addresses, with worldwide coverage.

## Quick Start (fetch)

```javascript
const key = process.env.ADDRESSZEN_API_KEY;

// Autocomplete: address suggestions as the user types (US by default)
const response = await fetch(
  'https://api.addresszen.com/v1/autocomplete/addresses?query=' +
    encodeURIComponent('1600 Pennsylvania Ave'),
  {
    headers: {
      Authorization: `api_key="${key}"`,
    },
  }
);

const { result } = await response.json();
console.log(result.hits); // [{ id, suggestion, ... }]
```

Resolve a chosen suggestion to a full address with `GET /autocomplete/addresses/{id}/{country}` — see the resolve-address reference under [`endpoints/`](./references/endpoints/). That second request is the paid lookup. Alternatively, pass `?api_key=...` in the query string instead of the header.

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

- `GET /autocomplete/addresses` — Typeahead address search
- `GET /autocomplete/addresses/{address}/{country}` — Resolve an autocomplete suggestion
- `GET /places` / `GET /places/{place}` — Place search and resolve
- `GET /postcodes/{postcode}` — Lookup all addresses for a UK postcode
- `POST /cleanse/addresses` — Cleanse a freeform address string
- `GET /emails`, `GET /phone_numbers` — Email and phone validation

See [`endpoints/`](./references/endpoints/) for the full list (23 operations).

## Critical Gotchas

- **Auth header format** — `Authorization: api_key="<your-key>"` (with double quotes around the key). Not `Bearer`, not `ApiKey <key>`. Query-string `?api_key=...` also works
- **API key restrictions** — default keys are restricted to specific domains. Ensure your domain is in the key's allowed list
- **CORS in browsers** — the API sets CORS headers for `http://localhost` in development. Production domains must be explicitly added to your key
- **Rate limits** — each IP is rate limited per second. Tripping the limit returns a 4021 (HTTP 402)
- **Error responses** — all errors are JSON with a numeric `code` and human-readable `message`. Check codes before retrying — see [`error-codes.md`](./references/error-codes.md)

## Reference Layout

- [`authentication.md`](./references/authentication.md) — header and query auth, key restrictions
- [`error-codes.md`](./references/error-codes.md) — error code catalogue with fixes
- [`endpoints/`](./references/endpoints/) — one reference per API operation (parameters, request body, response schema, examples, status codes)
- [`data/`](./references/data/) — one reference per data model (PafAddress, MrAddress, AddressSuggestion, etc.) with field tables and "used by" cross-links

## Full Spec

The complete OpenAPI spec is available at:

- npm: `@addresszen/openapi`
- web: <https://openapi.addresszen.com/openapi.yaml>

Reach for it when you need exhaustive parameter detail beyond what's in the endpoint references.

## Full documentation

The full AddressZen documentation — every guide, API reference, and integration — is available as a single file at [llms.txt](https://docs.addresszen.com/llms.txt). Point your agent there for anything this skill doesn't cover.
