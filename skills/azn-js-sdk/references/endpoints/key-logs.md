# `keyLogs`

Logs (CSV)

Returns a CSV of the charged lookups made on a key, one row per request.

Requires the account Management Key. The maximum interval is 90 days. Without a start or end date the interval is the last 21 days.

The response is `text/csv` and downloads as an attachment. A non-200 response reverts to JSON, with the error code and message in the body.

## CSV format

The CSV has no header row. Columns, in order:

1. Timestamp (ISO 8601)
2. IP address the request was received from
3. Search term
4. URL the request originated from
5. Lookup type
6. Tags
7. Lookups consumed
8. Licensee name (sublicensing keys only)
9. Source IP address

The source IP column carries the address forwarded in the `AZ-Source-IP` header. We record it only for keys with IP address forwarding enabled, and only when the header holds a valid IP address. It is empty otherwise.

## Data redaction

We redact personally identifiable data (PII) in your usage log weekly, covering the IP, source IP, search term and URL columns.

The default retention is 28 days. Change the period from your dashboard. Set it to `0` days to stop collecting PII altogether.

## Endpoint

`GET /keys/{key}/lookups`

See the [API reference](https://docs.addresszen.com/docs/api/key-logs) for this endpoint.

This operation needs a Management Key. Set it as `userToken` on the client, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/typescript/setup).

## Import

```ts
import { keyLogs } from "@addresszen/sdk";
```

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `string` | yes | **API Key** The API Key to retrieve. Begins `ak_`. |

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `start` | `number` | no | **Start Timestamp** A start date/time in the form of a UNIX Timestamp in milliseconds. E.g. `1418556452651` |
| `end` | `number` | no | **End Timestamp** An end date/time in the form of a UNIX Timestamp in milliseconds. E.g. `1418556477882` |
| `licensee` | `string` | no | **Licensee Key** Uniquely identifies a licensee. |

## Response Type

```ts
import type { KeyLogsResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="key-logs.ts"
import { createZenClient, keyLogs } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({
    apiKey: "ak_test",
    userToken: "uk_example",
  });
  const { data } = await keyLogs({
    client,
    path: { key: "ak_test" },
  });
  return data;
};
```
