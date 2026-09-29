# `keyUsage`

Usage Stats

Reports the number of lookups a key consumed over a date range, as a total and a daily breakdown.

The range defaults to the last 21 days. `start` and `end` take UNIX timestamps in milliseconds, and `end` defaults to the current time. The maximum range is 90 days.

Query at most three tags at once.

## Endpoint

`GET /keys/{key}/usage`

See the [API reference](https://docs.addresszen.com/docs/api/key-usage) for this endpoint.

This operation needs a Management Key. Set it as `userToken` on the client, which sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/typescript/setup).

## Import

```ts
import { keyUsage } from "@addresszen/sdk";
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
| `tags` | `string` | no | **Tags** A comma separated list of tags to query over. Useful if you want to specify the circumstances in which the request was made. If you specify multiple tags, the response comprises only requests that satisfy all of them. Searching `"foo,bar"` queries only requests tagged both `"foo"` and `"bar"`. |
| `licensee` | `string` | no | **Licensee Key** Uniquely identifies a licensee. |

## Response Type

```ts
import type { KeyUsageResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="key-usage.ts"
import { createZenClient, keyUsage } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({
    apiKey: "ak_test",
    userToken: "uk_example",
  });
  const { data } = await keyUsage({
    client,
    path: { key: "ak_test" },
  });
  return data;
};
```
