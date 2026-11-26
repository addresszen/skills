# AddressZen Skills

A collection of skills for AI coding agents (Claude Code, Cursor, Codex) providing guidance for integrating AddressZen APIs and widgets.

## Skills

- **`azn-address-lookup`** — integrating `@addresszen/address-lookup`, the vanilla JS address autocomplete widget.
- **`azn-api-integration`** — integrating the AddressZen API directly over HTTP.
- **`azn-react`** — integrating `@addresszen/react`, the React component for AddressZen Address Lookup.
- **`azn-cli`** - driving the API from the terminal with the `azn` CLI (`@addresszen/cli`).
- **`azn-js-sdk`** - integrating `@addresszen/sdk`, the fetch-based TypeScript SDK: typed API calls, autocomplete, error handling and React or Preact Query adapters.
- **`azn-python-sdk`** - integrating `addresszen` on PyPI, the Python SDK: typed methods and Pydantic models for every API operation: US address verification, email and phone validation, autocomplete, keys and licensees.
- **`azn-php-sdk`** - integrating `addresszen/sdk` on Packagist, the PHP SDK, and its Symfony bundle and Laravel package: one typed method and read-only response class for every API operation: US address verification, autocomplete, email and phone validation, keys and licensees.
- **`azn-ruby-sdk`** - integrating `addresszen` on RubyGems, the Ruby SDK: one method with keyword arguments and a response class with a reader per field for every API operation: US address verification, autocomplete, email and phone validation, keys and licensees.

## Install

```bash
npx skills add addresszen/skills
```

## Source

Authored in a private upstream monorepo at `packages/skills-zen/` and mirrored to this public repo. To contribute:

1. Report issues here on GitHub
2. Submit PRs here; maintainers will cherry-pick into atlas
3. Reach out at support@addresszen.com if you have questions

## License

See LICENSE in LICENSE
