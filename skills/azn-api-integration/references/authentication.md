# Authentication

Every API request needs an API key. Keys are minted in your AddressZen account at <https://addresszen.com>. Test keys have free balance and bypass URL restrictions.

## Header (recommended for server-side)

```
Authorization: api_key="ak_yourkey"
```

The key value **must be wrapped in double quotes**.

Multiple parameters can be combined in the same header, comma-separated:

```
Authorization: api_key="ak_yourkey", user_token="..."
```

## Query string

```
GET /v1/autocomplete/addresses?query=1600+Pennsylvania+Ave&api_key=ak_yourkey
```

Use the query form when calling from the browser via a JSONP-style integration or when the request runs through a redirect that strips headers. Both forms accept the same key; pick one per request — they don't merge.

## Key restrictions

Live keys are typically locked down with one or both of:

- **Allowed URLs** — the request's `Origin` or `Referer` header must match an entry on the key's allowlist. Server-side requests don't send these headers and so bypass the check; browser requests must use a key with the calling page's URL on the allowlist
- **Daily lookup limit** — caps per-day spend at the configured threshold

`localhost` is allowed by default for development. Production domains must be added explicitly.

A request rejected by Allowed URL matching returns HTTP 401 with code `4011` (URL not on whitelist). See [`error-codes.md`](./error-codes.md).

## Inspecting and managing keys

The Keys endpoints let you check balance, usage, and configuration without the dashboard:

- [`endpoints/key-availability.md`](./endpoints/key-availability.md) — is the key live and within its limits
- [`endpoints/key-details.md`](./endpoints/key-details.md) — full configuration
- [`endpoints/key-usage.md`](./endpoints/key-usage.md) — usage stats
- [`endpoints/key-logs.md`](./endpoints/key-logs.md) — request logs

Mutating key details (allowed URLs, limits) requires a `user_token` — your account's secret key, separate from `api_key`. Available from your AddressZen account settings.

## Test keys

A test key always returns the same canned responses and never consumes balance. Use it in integration tests and CI; switch to your live key for production.
