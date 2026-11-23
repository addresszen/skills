# MCP server

The API is a Model Context Protocol server at `https://api.addresszen.com/mcp`. Connect an agent to it to give the model address, email and phone tools directly, with no integration code.

## When to use MCP, when to use HTTP

- **MCP** - a model needs to verify or find an address, email or phone number while it works: a support agent checking a customer's address, a data-cleaning agent, an assistant filling a form.
- **HTTP** - you are writing application code that calls the API. Use the endpoints in [`endpoints/`](./endpoints/), or an SDK.
- **Widget** - end users type an address into a web form. Use Address Lookup.

## Requirements

- **Protocol revision `2026-07-28` only.** The server is stateless: no `initialize` handshake, no `Mcp-Session-Id`. Clients that stop at `2025-11-25` or earlier are refused with JSON-RPC error `-32022`. Clients that connect, as of November 2026: Claude Code; Codex CLI with `[features] mcp_2026_07_28 = true`; the `@modelcontextprotocol/client` v2 library with `versionNegotiation: { mode: { pin: "2026-07-28" } }` (`mode: "auto"` falls back to the older handshake and is refused). Cursor and VS Code stop at `2025-11-25` and cannot connect
- **Bearer auth on every request**: `Authorization: Bearer ak_...`. A licensee sends its own key, `Bearer sl_...`. Never put the key in the URL
- **A backend key.** A key with Allowed URLs is a browser key and is refused on every tool call with `4011`. Create a key with no Allowed URLs for MCP
- **No OAuth.** The server publishes no OAuth or Protected Resource Metadata. Configure the key as a static header
- **No streaming.** Every response is a single JSON body

## Tools

| Tool | Mirrors | Use it for |
| --- | --- | --- |
| `verify_address` | `POST /v1/verify/addresses` | Verify and correct one whole address. US addresses against USPS CASS, with ZIP+4. Optional `zip_code`, `city`, `state`, `country` (defaults to `USA`) |
| `find_address` | `GET /v1/autocomplete/addresses` | Fast, fuzzy candidates for a partial or messy `query`, each with an `id`. Optional `country` (defaults to `USA`), `limit`, `near` and `filter` |
| `retrieve_address` | `GET /v1/autocomplete/addresses/{id}/usa` | The full address for a chosen suggestion `id`, in the US format. Optional `remove_firm` |
| `validate_email` | `GET /v1/emails` | Whether an email address can receive mail |
| `validate_phone` | `GET /v1/phone_numbers` | Whether a phone number is reachable, its formats, country, line type and network. Optional `current_carrier` |

**Reach for `verify_address` first.** You usually hold the whole address already. Pass it as given, without tidying it, in `query`, or the first line in `query` plus `zip_code`, or `city` and `state`, when those are known separately and known to be right. Pass `country` for any address outside the United States. It returns one verified address, or no confident match.

**Use `find_address` then `retrieve_address` when confidence is low**: the address is partial, garbled or did not verify. Find is low latency and tolerates typos and missing parts, and returns several candidates. Narrow them with `filter` (filters and biases) or `near` and call again, then choose a candidate or ask the user, and retrieve the one chosen. Finds are free; each retrieve is billed.

`filter` is an object of any other filter or bias `GET /v1/autocomplete/addresses` takes, by its REST name: `{"state_code": "NM", "bias_city": "alamogordo"}`. A filter excludes non-matches; a `bias_` name only ranks matches first. Unsupported names for the country are ignored. Typed arguments win over the same name in `filter`. At most 10 entries, names matching `^[a-z0-9_]+$`, values up to 128 characters. See [`endpoints/find-address.md`](./endpoints/find-address.md) for the names.

The tool list is identical for every key. `tools/list` never refuses a valid key.

## Billing

Each tool runs the same key checks and billing as the endpoint it mirrors. `verify_address` in the United States costs one lookup for every address CASS answers, matched or not; a query that cannot be parsed costs nothing. Elsewhere only a match costs a lookup. `find_address` is free but needs a positive balance. `retrieve_address` costs one lookup.

## Errors

- **Missing or unknown key** - HTTP `401`, JSON-RPC error `4010`. The only failure that fails the request
- **Protocol failures** - negative JSON-RPC codes: `-32022` unsupported protocol version, `-32020` `Mcp-Method`/`Mcp-Name` header does not match the body, `-32602` unknown tool or malformed `tools/call` params, `-32700` invalid JSON, `-32600` body too large (`413`) or not UTF-8 (`415`)
- **Invalid tool arguments** - a tool result with `isError: true` and `Input validation error: <field>: <issue>`. Fix the argument and call again
- **API refusals** - an ordinary tool result with `isError: true` and the API's own code: `4011` key restricted to Allowed URLs, `4013` sublicensed key without its licensee, `4020` no balance, `4021` lookup limit reached, `4048` unknown suggestion `id`. The full list is in [`error-codes.md`](./error-codes.md). Read the message and tell the user; do not retry
- **No match** - an ordinary result with no suggestions, or no confident match from `verify_address`, not an error

## Raw request

```bash
curl -s https://api.addresszen.com/mcp \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json, text/event-stream' \
  -H "Authorization: Bearer $ADDRESSZEN_API_KEY" \
  -H 'MCP-Protocol-Version: 2026-07-28' \
  -H 'Mcp-Method: tools/call' \
  -H 'Mcp-Name: verify_address' \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "tools/call",
    "params": {
      "name": "verify_address",
      "arguments": { "query": "1010 cauthn ln, alamogordo nm 88310" },
      "_meta": {
        "io.modelcontextprotocol/protocolVersion": "2026-07-28",
        "io.modelcontextprotocol/clientCapabilities": {}
      }
    }
  }'
```

Full guide: <https://docs.addresszen.com/docs/guides/mcp>
