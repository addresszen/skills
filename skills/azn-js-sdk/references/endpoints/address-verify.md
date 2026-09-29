# `addressVerify`

Verify Address

Verifies an address against the USPS Coding Accuracy Support System (CASS) and returns it standardized and corrected.

Submit the whole address in `query`, or the first address line in `query` with either `zip_code`, or `city` and `state`. A freeform `query` is parsed into those components before the search runs.

A match returns the standardized address lines, city, state and ZIP+4, scored by `fit` and `confidence`. It also carries the CASS record behind the match: delivery point, DPV flags, carrier route, eLOT, county, congressional district, RDI, time zone and coordinates. No match returns `200` with a `count` of `0`, a `null` `match` and empty address fields.

Only a match draws on your balance. A key without address verification enabled returns `401`. A verification still running after 9.5 seconds aborts with `429`.

## Countries

Verify defaults to the United States, where it is CASS certified. Pass `context` with an ISO 3166-1 alpha-3 country code to verify an address elsewhere, e.g. `context=GBR` or `context=FRA`. The address datasets your key is licensed for decide which countries it can verify.

Outside the United States there is no CASS record to return, so `match` carries the standardized address from that country's dataset instead. The top-level fields (`address_line_one`, `city`, `state`, `zip_code`, `country_iso_2`) are populated for every country, along with `confidence` and `fit`.

## Endpoint

`POST /verify/addresses`

See the [API reference](https://docs.addresszen.com/docs/api/address-verify) for this endpoint.

## Import

```ts
import { addressVerify } from "@addresszen/sdk";
```

## Path Parameters

_None._

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `api_key` | `string` | no | **API Key** Your unique identifier that allows access to our APIs. Begins `ak_`. Available from your dashboard. |
| `tags` | `string` | no | **Tags** A comma separated list of tags to query over. Useful if you want to specify the circumstances in which the request was made. If you specify multiple tags, the response comprises only requests that satisfy all of them. Searching `"foo,bar"` queries only requests tagged both `"foo"` and `"bar"`. |
| `context` | `string` | no | Identify the country of the address to verify. Defaults to United States (USA) |

## Request Body

```ts
{
    /**
     * Address input to verify.
     *
     * If submitting a freeform address verification query, enter the full address. E.g. `query=123 Main St, Springfield, CO, 81073`
     *
     * Otherwise, query can be accompanied with the following address components:
     * - `zip_code`
     * - `city` and `state`
     *
     * If you supply `zip_code`, or `city` and `state`, omit that information from `query` and use it for the first address line only. E.g. `query=123 Main St`
     *
     */
    query: string;
    /**
     * Specify the ZIP code of an address. The following formats are accepted: `81073-1119`, `810731119`, `81073`.
     *
     */
    zip_code?: string;
    /**
     * City of an address.
     *
     */
    city?: string;
    /**
     * State of an address. For the US, use the 2 letter state abbreviation.
     *
     */
    state?: string;
  }
```

## Response Type

```ts
import type { AddressVerifyResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="address-verify.ts"
import { createZenClient, addressVerify } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({ apiKey: "ak_test" });
  const { data } = await addressVerify({
    client,
    body: { query: "123 Main St, Springfield, CO 81073" },
  });
  return data;
};
```
