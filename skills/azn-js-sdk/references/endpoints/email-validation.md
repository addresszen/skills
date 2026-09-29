# `emailValidation`

Email Validation

Validates an email address and reports whether it is deliverable.

Requires an API Key licensed for email validation. A query over 320 characters is rejected.

A validated address decrements your lookup balance. An address the API cannot check returns `unknown` and costs no lookup. An address whose domain does not resolve, or publishes no MX records, returns `not_deliverable` and also costs no lookup. Only those two domain failures populate `suggestions`. Every other response returns an empty list.

## Endpoint

`GET /emails`

See the [API reference](https://docs.addresszen.com/docs/api/email-validation) for this endpoint.

## Import

```ts
import { emailValidation } from "@addresszen/sdk";
```

## Path Parameters

_None._

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `api_key` | `string` | no | **API Key** Your unique identifier that allows access to our APIs. Begins `ak_`. Available from your dashboard. |
| `query` | `string` | yes | Specifies the email address to validate |
| `tags` | `string` | no | **Tags** A comma separated list of tags to query over. Useful if you want to specify the circumstances in which the request was made. If you specify multiple tags, the response comprises only requests that satisfy all of them. Searching `"foo,bar"` queries only requests tagged both `"foo"` and `"bar"`. |

## Response Type

```ts
import type { EmailValidationResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="email-validation.ts"
import { createZenClient, emailValidation } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({ apiKey: "ak_test" });
  const { data } = await emailValidation({
    client,
    query: { query: "person@example.com" },
  });
  return data;
};
```
