# azn auth

Manage stored credentials at `~/.config/addresszen/credentials.json` (or `%APPDATA%\addresszen\credentials.json` on Windows, or `$XDG_CONFIG_HOME/addresszen/...` if set). The file is written with mode `0600`.

## `azn auth login`

Store an `api_key` (required) and `user_token` (optional) for later reuse. The `api_key` is verified against `GET /keys/{key}`, and a supplied `user_token` against `GET /keys/{key}/details`, before either is written.

| Flag | Description |
| --- | --- |
| `--api-key <k>` | **Required** in non-interactive mode; prompted interactively. |
| `--user-token <t>` | Optional. Unlocks `/keys/*` reads when present. |

Non-interactive (no TTY or `--json`): `--api-key` is required; missing it returns `invalid_input`. `--user-token` is optional and stored only if supplied.

Interactive: prompts for the api_key (required) then the user_token (press enter to skip). Both inputs are masked.

### Output

```json
{
  "success": true,
  "config_path": "/home/you/.config/addresszen/credentials.json",
  "available": true
}
```

### Error codes

- `invalid_input`: non-interactive mode missing `--api-key`
- `auth_failed`: API rejected the supplied credentials during verification
- `write_failed`: unable to write credentials file

## `azn auth logout`

Remove the credentials file.

### Output

```json
{ "success": true, "removed": true, "config_path": "..." }
```

`removed: false` means there was no file to remove, not an error.

## `azn auth whoami`

Show where each credential was resolved from and call `GET /keys/{key}` to verify the api_key is live.

### Output

```json
{
  "api_key": { "source": "env", "preview": "ak_mpl…" },
  "user_token": { "source": "config", "preview": "uk_jc6…" },
  "live": true,
  "available": true
}
```

`source` is `flag`, `env`, or `config`. `preview` is the first 6 characters of the credential followed by `…`.

Either credential may be `null` if it isn't configured. When `api_key` is `null`, the API check is skipped; output omits `available` and reports `"live": false`.
