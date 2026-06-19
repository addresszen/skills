# azn keys

Inspect and manage API keys.

Every subcommand accepts `[key]` as an optional first positional. If omitted, the resolved api_key is used — so `azn keys details` and `azn keys details ak_xxx` behave the same when your own key is configured.

All subcommands except `keys get` **require a user_token**. The CLI preflights this before any HTTP call: if no user_token is found via `--user-token`, `AZN_USER_TOKEN`, or `azn auth login`, the command exits with `code: missing_user_token` and a hint pointing to those three sources.

## `azn keys get [key]`

Public availability info — `GET /keys/{key}`. No user_token is attached (the response shape changes if one is present, so the CLI explicitly omits it even when available).

## `azn keys details [key]`

Private key details — `GET /keys/{key}/details`. **Requires user_token.**

## `azn keys update [key]`

Update key details — `PUT /keys/{key}/details`. **Requires user_token.**

| Flag | Description |
|---|---|
| `--json-body <json>` | **Required.** Raw JSON body of fields to update. |

```bash
azn keys update --json-body '{"notifications":{"email":"ops@example.com"}}'
```

## `azn keys usage [key]`

Lookup counts over a date range — `GET /keys/{key}/usage`. **Requires user_token.**

| Flag | Description |
|---|---|
| `--start <date>` | Start date (YYYY-MM-DD or ISO) |
| `--end <date>` | End date |
| `--tags <csv>` | Comma-separated tag filter |
| `--licensee <id>` | Filter by licensee id |

## `azn keys logs [key]`

Paid lookup logs — `GET /keys/{key}/lookups`. Emits **raw CSV to stdout**. **Requires user_token.**

| Flag | Description |
|---|---|
| `--start <date>` | Start date |
| `--end <date>` | End date |
| `--licensee <id>` | Filter by licensee id |

This command is CSV-only and does not support `--json` / `-q` — passing either errors with `invalid_input`. Redirect to a file or pipe into CSV tooling:

```bash
azn keys logs --start 2026-01-01 --end 2026-01-31 > lookups.csv
```

## `azn keys configs`

All subcommands **require user_token** (including `get` and `list`).

A config's `payload` is an opaque serialised-JSON **string** (matching the API's `ConfigNewParam` / `ConfigUpdateParam`). The CLI validates that it parses as JSON but does not interpret its contents.

### `list [key]`

`GET /keys/{key}/configs` — list all configs.

### `get <config> [key]`

`GET /keys/{key}/configs/{config}` — retrieve one.

### `create <name> [key]`

`POST /keys/{key}/configs` — create a new config.

| Flag | Description |
|---|---|
| `--payload <json>` | **Required.** Serialised config payload (JSON string). |

```bash
azn keys configs create my-site --payload '{"allowedUrls":["https://example.com"]}'
```

### `update <config> [key]`

`POST /keys/{key}/configs/{config}` — update in place.

| Flag | Description |
|---|---|
| `--payload <json>` | **Required.** Serialised config payload (JSON string). Replaces the existing payload. |

### `delete <config> [key]`

`DELETE /keys/{key}/configs/{config}`. Requires `--yes` in non-TTY (or `--json`).

| Flag | Description |
|---|---|
| `-y, --yes` | Skip confirmation |
