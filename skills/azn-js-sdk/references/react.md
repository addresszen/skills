# React and Preact

To add address search to a form, use [Address Lookup for React](https://docs.addresszen.com/docs/address-lookup/react). It provides the interface and fills in your address fields.

To build your own component, use the SDK. The examples below search as the user types. `autocomplete.find` and `findAddressOptions` take the same query parameters as `findAddress`, so set `context` to search a country other than your account's default and add a [filter or bias term](https://docs.addresszen.com/docs/sdks/typescript/filter-and-bias) to narrow the results.

## Without dependencies

The [autocomplete helper](https://docs.addresszen.com/docs/sdks/typescript/autocomplete) debounces keystrokes and drops stale requests, so a hook needs no data-fetching library.

```bash
npm install @addresszen/sdk
```

#### React

```tsx title="Search.tsx"
import { useEffect, useState } from "react";
import { createZenClient } from "@addresszen/sdk";
import { createAutocomplete, type Hit } from "@addresszen/sdk/autocomplete";

const autocomplete = createAutocomplete({
  client: createZenClient({ apiKey: "ak_test" }),
});

export function Search() {
  const [query, setQuery] = useState("");
  const [hits, setHits] = useState<Hit[]>([]);

  useEffect(() => {
    if (query.length < 3) return setHits([]);
    autocomplete
      .find({ query })
      .then((found) => found && setHits(found))
      .catch(console.error);
    return () => autocomplete.cancel();
  }, [query]);

  return (
    <div>
      <input value={query} onInput={(event) => setQuery(event.currentTarget.value)} aria-label="Address" />
      <ul>{hits.map((hit) => <li key={hit.id}>{hit.suggestion}</li>)}</ul>
    </div>
  );
}
```

#### Preact

```tsx title="Search.tsx"
import { useEffect, useState } from "preact/hooks";
import { createZenClient } from "@addresszen/sdk";
import { createAutocomplete, type Hit } from "@addresszen/sdk/autocomplete";

const autocomplete = createAutocomplete({
  client: createZenClient({ apiKey: "ak_test" }),
});

export function Search() {
  const [query, setQuery] = useState("");
  const [hits, setHits] = useState<Hit[]>([]);

  useEffect(() => {
    if (query.length < 3) return setHits([]);
    autocomplete
      .find({ query })
      .then((found) => found && setHits(found))
      .catch(console.error);
    return () => autocomplete.cancel();
  }, [query]);

  return (
    <div>
      <input value={query} onInput={(event) => setQuery(event.currentTarget.value)} aria-label="Address" />
      <ul>{hits.map((hit) => <li key={hit.id}>{hit.suggestion}</li>)}</ul>
    </div>
  );
}
```

## Try it

Type an address to see suggestions. Finding suggestions does not draw on your balance.

```html
<div id="app"></div>
```

```jsx
  import { useEffect, useState } from "react";
  import { createRoot } from "react-dom/client";
  import { createZenClient } from "@addresszen/sdk";
  import { createAutocomplete } from "@addresszen/sdk/autocomplete";

  const apiKey = "ak_test"; // Replace with your own API key
  const autocomplete = createAutocomplete({ client: createZenClient({ apiKey }) });

  function Search() {
    const [query, setQuery] = useState("");
    const [hits, setHits] = useState([]);

    useEffect(() => {
      if (query.length < 3) return setHits([]);
      autocomplete
        .find({ query })
        .then((found) => found && setHits(found))
        .catch(console.error);
      return () => autocomplete.cancel();
    }, [query]);

    return (
      <div>
        <input value={query} placeholder="123 Main St" onInput={(event) => setQuery(event.currentTarget.value)} aria-label="Address" />
        <ul>{hits.map((hit) => <li key={hit.id}>{hit.suggestion}</li>)}</ul>
      </div>
    );
  }

  createRoot(document.getElementById("app")).render(<Search />);
```

## TanStack Query

The SDK exports TanStack Query options, query keys and mutations for every operation from `@addresszen/sdk/react-query` and `@addresszen/sdk/preact-query`. Install the matching peer, `@tanstack/react-query` or `@tanstack/preact-query`. Wrap the component in a `QueryClientProvider`.

```bash
npm install @addresszen/sdk @tanstack/react-query
```

#### React

```tsx title="App.tsx"
import { useState } from "react";
import { QueryClient, QueryClientProvider, useQuery } from "@tanstack/react-query";
import { createZenClient } from "@addresszen/sdk";
import { findAddressOptions } from "@addresszen/sdk/react-query";

const client = createZenClient({ apiKey: "ak_test" });
const queryClient = new QueryClient();

function Search() {
  const [query, setQuery] = useState("");
  const result = useQuery({
    ...findAddressOptions({ client, query: { query } }),
    enabled: query.length >= 3,
    staleTime: 60_000,
  });
  return (
    <div>
      <input value={query} onInput={(event) => setQuery(event.currentTarget.value)} aria-label="Address" />
      {result.isError && <p>Address search failed.</p>}
      <ul>{result.data?.result.hits.map((hit) => <li key={hit.id}>{hit.suggestion}</li>)}</ul>
    </div>
  );
}

export function App() {
  return <QueryClientProvider client={queryClient}><Search /></QueryClientProvider>;
}
```

#### Preact

```tsx title="App.tsx"
import { useState } from "preact/hooks";
import { QueryClient, QueryClientProvider, useQuery } from "@tanstack/preact-query";
import { createZenClient } from "@addresszen/sdk";
import { findAddressOptions } from "@addresszen/sdk/preact-query";

const client = createZenClient({ apiKey: "ak_test" });
const queryClient = new QueryClient();

function Search() {
  const [query, setQuery] = useState("");
  const result = useQuery({
    ...findAddressOptions({ client, query: { query } }),
    enabled: query.length >= 3,
    staleTime: 60_000,
  });
  return (
    <div>
      <input value={query} onInput={(event) => setQuery(event.currentTarget.value)} aria-label="Address" />
      {result.isError && <p>Address search failed.</p>}
      <ul>{result.data?.result.hits.map((hit) => <li key={hit.id}>{hit.suggestion}</li>)}</ul>
    </div>
  );
}

export function App() {
  return <QueryClientProvider client={queryClient}><Search /></QueryClientProvider>;
}
```

Pass the client to each builder. Queries forward TanStack Query's cancellation signal and throw on failure, so a failed query's `error` is the `ApiError`, or the native error for a network failure. Debounce the query value before passing it to `findAddressOptions` if you want fewer requests.

Use separate query caches when switching credentials. Do not share an authenticated query cache between server requests or users.
