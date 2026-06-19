---
name: azn-cli
description: >
  Drive the AddressZen API from the terminal — manage API keys (balance, usage,
  allowed-URL configs, lookup logs), verify US addresses, validate email
  addresses and phone numbers, and resolve specific addresses from partial
  queries via the `azn` CLI.
  Use when the user wants to inspect or update an AddressZen account, verify US
  addresses in bulk, validate emails or phone numbers, or pin down a specific
  address from a partial query. Always load this skill before running `azn` — it
  defines the non-interactive flag contract and output shape that keep agent
  runs deterministic.
license: SEE LICENSE IN LICENSE
metadata:
  author: addresszen
  source: https://github.com/addresszen/skills
  envVars:
    - name: AZN_API_KEY
      required: true
      description: AddressZen API key
    - name: AZN_USER_TOKEN
      required: false
      description: Required for private key endpoints (details, usage, logs, configs)
references:
  - auth.md
  - keys.md
  - verify.md
  - email.md
  - phone.md
  - find.md
---

# AddressZen CLI (`azn`)

## Installation

```bash
npm install -g @addresszen/cli
azn --version
```

## Agent Protocol

The CLI auto-detects non-TTY environments and emits JSON — no `--json` flag needed when piping or running headless.

**Rules for agents:**

- Supply ALL required flags. The CLI will NOT prompt when stdin is not a TTY.
- `-q / --quiet` suppresses any status output and implies `--json`.
- Exit `0` = success, `1` = error.
- Both success and error JSON go to **stdout** — parse it uniformly, then check for an `error` key and the exit code:
  ```json
  {"error":{"code":"...","message":"...","details":{}}}
  ```
- Destructive commands (e.g. `keys configs delete`) require `--yes` in non-TTY.
- Use env vars or flags. Never rely on `azn auth login` from an agent.

## Authentication

Two credentials: `api_key` (required) and `user_token` (required for `/keys/*` reads, configs, updates). Resolution precedence — per credential:

| Priority | Source |
|---|---|
| 1 (highest) | `--api-key <k>` / `--user-token <t>` |
| 2 | `AZN_API_KEY` / `AZN_USER_TOKEN` env var |
| 3 (lowest) | `~/.config/addresszen/credentials.json` (written by `azn auth login`) |

Missing api_key → error code `missing_api_key`. Missing user_token on a command that needs it → `missing_user_token`.

## Global Flags

| Flag | Description |
|------|-------------|
| `--api-key <k>` | Override API key for this invocation |
| `--user-token <t>` | Override user token |
| `--json` | Force JSON (auto in non-TTY) |
| `-q, --quiet` | Suppress status, implies `--json` |
| `--base-url <url>` | Override API base (diagnostics only) |

## Available Commands

| Group | Subcommands |
|---|---|
| `azn auth` | `login`, `logout`, `whoami` |
| `azn keys` | `get`, `details`, `update`, `usage`, `logs`, `configs {list,get,create,update,delete}` |
| `azn verify` | Verify one US address, a file, or stdin |
| `azn email` | Validate one email, a file, or stdin |
| `azn phone` | Validate one phone number, a file, or stdin |
| `azn find` / `resolve` | Autocomplete then resolve a suggestion id to a full address (paired; see `find.md`) |
| `azn doctor` | Env + connectivity check |

Read the matching reference file for flags and example output.

## Common Pitfalls

- **`user_token` is separate from `api_key`.** `keys details`, `keys usage`, `keys logs`, `keys update`, and all `configs` writes require both.
- **`verify`, `email`, and `phone` cost paid lookups.**
- **`verify` / `email` / `phone` batch mode emits CSV** unless `--json` is passed; a single query always emits JSON.
- **`find` without a query in non-TTY errors.** Always pass a query when scripting.
- **`keys logs` emits raw CSV**, not JSON, and rejects `--json` / `-q` with `invalid_input`. Redirect to a file or pipe into your CSV tooling.
- **Credentials file is `0600`.** If your umask is unusual, `azn auth login` may fail with `write_failed`.

## Quick Examples

```bash
# Verify one US address (JSON to stdout)
azn verify "1600 Amphitheatre Pkwy, Mountain View, CA 94043"

# Batch verify
cat addresses.txt | azn verify --stdin

# Validate an email or phone number
azn email "support@example.com"
azn phone "+12025550173" --carrier

# Batch validate emails to a CSV
cat emails.txt | azn email --stdin > emails.csv

# Find a specific address and resolve it
ID=$(azn find "1600 amphitheatre" | jq -r '.suggestions[0].id')
azn resolve "$ID"

# Inspect a key
azn keys details
```
