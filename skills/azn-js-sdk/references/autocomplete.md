# Autocomplete

The autocomplete helper turns a partial address into suggestions, then a chosen suggestion into a full address. It debounces keystrokes, drops stale requests and caches recent suggestions. Each search runs in one country, set with `context`.

```ts title="autocomplete.ts"
import { createZenClient } from "@addresszen/sdk";
import { createAutocomplete } from "@addresszen/sdk/autocomplete";

const client = createZenClient({ apiKey: "ak_test" });
const autocomplete = createAutocomplete({ client });

const suggest = async (query: string, context: string) => {
  const hits = await autocomplete.find({ query, context });
  if (!hits) return; // superseded by a newer find, or cancelled
  const hit = hits[0];
  if (!hit) return; // no matches
  const address = await autocomplete.retrieve({ hit });
  console.log(address.country_iso, address.line_1);
};

await suggest("123 Main St", "USA");
await suggest("1425 James St", "CAN");

// Call when the input is removed or the component unmounts.
autocomplete.cancel();
```

## How do I find suggestions?

Call `find` with `query` and any other [`findAddress`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/find-address) parameter, such as `context` or `limit`, in one object. It waits for typing to pause, then resolves to an array of hits. An empty array means nothing matched.

Set `context` to a three-letter ISO 3166-1 code, such as `USA`, `CAN` or `JPN`. Without it, the search uses your account's default country. To narrow results by ZIP or postal code, state, area or address type, see [filter and bias](https://docs.addresszen.com/docs/sdks/typescript/filter-and-bias).

A newer `find` resolves the previous pending call with `undefined` and aborts its request. `cancel()` does the same without starting another. Superseded calls never reject, so check for `undefined` and return early.

Show each hit's `suggestion` as it arrives. The API may change the suggestion format, so do not parse it.

## How do I let users switch country?

Load the countries your key can search with [`keyAvailability`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/key-availability), show them in a picker, then pass the chosen code as `context`. Each key is licensed for its own set of countries. The check needs only the API key, so it can run in the browser.

```ts title="country-switch.ts"
import { createZenClient, keyAvailability } from "@addresszen/sdk";
import { createAutocomplete } from "@addresszen/sdk/autocomplete";

const apiKey = "ak_test";
const client = createZenClient({ apiKey });
const autocomplete = createAutocomplete({ client });

const { data } = await keyAvailability({ client, path: { key: apiKey } });
const { contexts, context } = data.result;
for (const country of contexts) console.log(country.emoji, country.description, country.iso_3);

// Start with the country that matches the user's IP address, if any.
let country = context || contexts[0]?.iso_3;
await autocomplete.find({ query: "123 Main St", context: country });

// When the user picks another country, search again with its code.
country = "CAN";
await autocomplete.find({ query: "100 Queen St W, Toronto", context: country });
```

Each entry in `contexts` has `iso_3` (the `context` code), `iso_2`, `description` and `emoji`. `context` is the licensed country that best matches the caller's IP address, or an empty string when none does.

## How do I retrieve an address?

Pass a hit from `find` to `retrieve`, which calls [`retrieveAddress`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/retrieve-address) at once, without a debounce. Finding suggestions does not draw on your balance. Retrieving an address costs one lookup. The API rate limits, then suspends, keys that find suggestions without retrieving any.

## What does a retrieved address look like in each country?

`retrieve` returns every address in one US-shaped format, whatever the country: up to two address lines and US field names such as `zip_code`, `state` and `city`. A field the country's dataset does not carry is an empty string. `dataset` names the source, and `native` carries the dataset's raw record for every dataset except `usps`.

| Country | `dataset` | Source | Differences |
| --- | --- | --- | --- |
| United States | `usps` | [USPS ZIP+4](https://docs.addresszen.com/docs/data/usps) | No `native`. The USPS fields, such as `zip_plus_4_code` and `carrier_route_id`, are on the address itself |
| Canada | `cannar` | [Statistics Canada National Address Register](https://docs.addresszen.com/docs/data/cannar) | `language` is `en` or `fr`. Each address appears in one language only |
| Japan | `upujp` | [Universal Postal Union address file for Japan](https://docs.addresszen.com/docs/data/upujp) | The API indexes each address once per script, so one address can return three hits: kanji, hiragana and Hepburn romanization. `native.script` is `Hani`, `Hira` or `Latn` |

Narrow `native` on `dataset` to read a country's own fields, such as the prefecture of a Japanese address or the province of a Canadian one:

```ts title="native.ts"
import type { Address } from "@addresszen/sdk";

const region = (address: Address): string => {
  const native = address.native;
  if (native?.dataset === "upujp") return native.prefecture;
  if (native?.dataset === "cannar") return native.mail_prov_abvn;
  return address.state;
};
```

[Supported countries](https://docs.addresszen.com/docs/data/supported-countries) lists every country and its `context` code.

## Which options does the helper take?

| Option | Default | Effect |
| --- | --- | --- |
| `debounceMs` | `100` | Milliseconds of quiet before `find` sends a request |
| `cache` | `{ max: 50, ttlMs: 60_000 }` | Size and lifetime of the suggestions cache. `false` disables it |

The cache belongs to one helper instance. Create a new client and helper when credentials change.

## Which types does it export?

`@addresszen/sdk/autocomplete` exports `CreateAutocompleteOptions`, `Autocomplete`, `Hit`, `RetrievedAddress`, `FindInput` and `RetrieveInput` for typing your own wrappers.

## How does it report errors?

HTTP errors reject with [`ApiError`](https://docs.addresszen.com/docs/sdks/typescript/errors). Network failures reject with the runtime's native error. The helper does not cache failed requests. Pass `signal` to `find` or `retrieve` to abort a request yourself. The call then rejects with `AbortError`.

Framework consumers can use [TanStack Query](https://docs.addresszen.com/docs/sdks/typescript/react#how-do-i-use-tanstack-query) for query caching instead.

## Try it

Select **Find** to run the search. Edit the query in the code to try another.

```html
<button>Find</button>
<pre></pre>
```

```javascript
  import { createZenClient } from "@addresszen/sdk";
  import { createAutocomplete } from "@addresszen/sdk/autocomplete";

  const apiKey = "ak_test"; // Replace with your own API key
  const client = createZenClient({ apiKey });
  const autocomplete = createAutocomplete({ client });

  document.querySelector("button").addEventListener("click", async () => {
    const hits = await autocomplete.find({ query: "123 Main St" });
    document.querySelector("pre").textContent = JSON.stringify(hits, null, 2);
  });
```
