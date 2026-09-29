# Filter and bias address search

`findAddress` and `autocomplete.find` accept filters, which remove addresses that do not match, and bias terms, which rank matching addresses higher without removing the rest. Both apply within one country, chosen with `context`.

```ts title="filter.ts"
import { createZenClient, findAddress } from "@addresszen/sdk";

const client = createZenClient({ apiKey: "ak_test" });
const { data } = await findAddress({
  client,
  query: {
    query: "100 market st",
    context: "USA",
    postal_code_3: "94102",
  },
});
console.log(data.result.hits);
```

Pass the same keys to the [autocomplete helper](https://docs.addresszen.com/docs/sdks/typescript/autocomplete) in the object you give `find`:

```ts title="autocomplete-filter.ts"
const hits = await autocomplete.find({
  query: "100 market st",
  context: "USA",
  state_code: "CA",
});
```

## Should I filter or bias?

Filter when an address outside the constraint is wrong for your form, such as a checkout that ships to one state. Bias when it is only less likely, such as a customer who probably lives near their store. A filter that matches no address returns an empty array. A bias term never removes a result.

Filters and bias terms do not affect your lookup balance.

## How do I choose the country?

Set `context` to the country's three-letter ISO 3166-1 code, the same code the API returns in `country_iso`. A missing or unrecognized `context` falls back to your account's default country, so set it on every request if your users are in more than one country. The [supported countries](https://docs.addresszen.com/docs/data/supported-countries) page lists each code.

```ts title="context.ts"
const { data } = await findAddress({
  client,
  query: { query: "1425 James St", context: "CAN" },
});
```

## How do I filter by ZIP or postal code?

Use one of three postal code filters. For US addresses:

| Parameter | US value | Example |
| --- | --- | --- |
| `postal_code` | Nine-digit ZIP+4 | `94102-1234` |
| `postal_code_2` | Three-digit ZIP prefix (sectional center) | `941` |
| `postal_code_3` | Five-digit ZIP code | `94102` |

`postal_code` ignores case, spaces and hyphens, so `94102-1234` and `941021234` match the same addresses. For other countries, `postal_code` matches the full postal code, `postal_code_2` matches the start of it and `postal_code_3` matches the short form.

Separate terms with commas to accept any of them:

```ts title="zip-filter.ts"
const { data } = await findAddress({
  client,
  query: {
    query: "flatbush ave",
    context: "USA",
    postal_code_3: "11225,11226,11238",
  },
});
```

## How do I filter or bias by state?

Filter with `state_code` or `state`. `state_code` takes a state or region code, such as the two-letter USPS abbreviation `CA`. `state` takes the full name, such as `California`. Both ignore case.

```ts title="state-filter.ts"
const { data } = await findAddress({
  client,
  query: { query: "100 main st", context: "USA", state_code: "CA" },
});
```

To rank some states first without hiding the others, use `bias_state_code` or `bias_state`:

```ts title="state-bias.ts"
const { data } = await findAddress({
  client,
  query: { query: "100 main st", context: "USA", bias_state_code: "NY,NJ" },
});
```

## How do I limit search to an area?

Bias toward a point with `bias_lonlat`, or restrict to a rectangle with `box`. Both take longitude first.

`bias_lonlat` is `longitude,latitude,radius`, with the radius in meters up to `50000` (50 km). This example favors addresses within 5 km of central Victoria, British Columbia:

```ts title="lonlat-bias.ts"
const { data } = await findAddress({
  client,
  query: {
    query: "james st",
    context: "CAN",
    bias_lonlat: "-123.355,48.4283,5000",
  },
});
```

`box` is `top_left_lon,top_left_lat,bottom_right_lon,bottom_right_lat`. The top-left longitude must be less than the bottom-right longitude and the top-left latitude greater than the bottom-right latitude. The API ignores a box that fails either check.

`bias_ip: "true"` biases results by the approximate geolocation of the IP address.

Each request takes one `bias_lonlat` and one `box` at most.

## How do I find or exclude PO Boxes and businesses?

Set `is_pobox` or `is_business` to `"true"` to return only those addresses, or `"false"` to exclude them. Both are defined for US addresses, where the API derives them from the USPS record type: `P` for a PO Box and `F` for a firm.

```ts title="pobox-filter.ts"
const { data } = await findAddress({
  client,
  query: { query: "100 main st", context: "USA", is_pobox: "false" },
});
```

## How do filters combine?

Different filters combine with AND, so `state_code: "CA"` with `city: "San Francisco"` requires both. Comma-separated terms within one filter combine with OR. A request takes up to 10 filter terms and 5 bias terms. The API ignores a filter name it does not recognize and a bias term it cannot read.

## Parameters

| Parameter | Kind | Value |
| --- | --- | --- |
| `context` | Country | ISO 3166-1 alpha-3 code, such as `USA`, `CAN` or `JPN` |
| `dataset` | Filter | Dataset names, for keys with more than one dataset for a country |
| `postal_code` | Filter | Full postal code. ZIP+4 for US addresses |
| `postal_code_2` | Filter | Postal code prefix. Three-digit ZIP prefix for US addresses |
| `postal_code_3` | Filter | Short postal code. Five-digit ZIP for US addresses |
| `city` | Filter | City, town or locality. Ignores case, spaces and accents |
| `state` | Filter | State, province or region name |
| `state_code` | Filter | State or region code, such as `CA` |
| `is_pobox` | Filter | `"true"` or `"false"` |
| `is_business` | Filter | `"true"` or `"false"` |
| `box` | Filter | `top_left_lon,top_left_lat,bottom_right_lon,bottom_right_lat` |
| `bias_postal_code` | Bias | Full postal code |
| `bias_postal_code_2` | Bias | Postal code prefix |
| `bias_postal_code_3` | Bias | Short postal code |
| `bias_city` | Bias | City, town or locality |
| `bias_state` | Bias | State, province or region name |
| `bias_state_code` | Bias | State or region code |
| `bias_lonlat` | Bias | `longitude,latitude,radius`, radius in meters up to `50000` |
| `bias_ip` | Bias | `"true"` |

See [`findAddress`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/find-address) for every parameter and the [API reference](https://docs.addresszen.com/docs/api/find-address) for the endpoint.
