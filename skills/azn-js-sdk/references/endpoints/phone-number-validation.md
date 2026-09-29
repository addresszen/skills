# `phoneNumberValidation`

Phone Number Validation

Validates a phone number and returns its country, its national and international formats, and the network it was originally assigned to.

Requires an API Key licensed for phone validation.

Every query decrements your lookup balance, including a number that fails to parse and a number reported as invalid.

## Endpoint

`GET /phone_numbers`

See the [API reference](https://docs.addresszen.com/docs/api/phone-number-validation) for this endpoint.

## Import

```ts
import { phoneNumberValidation } from "@addresszen/sdk";
```

## Path Parameters

_None._

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `api_key` | `string` | no | **API Key** Your unique identifier that allows access to our APIs. Begins `ak_`. Available from your dashboard. |
| `query` | `string` | yes | Specifies the phone number to validate. Phone number must include a country code in an acceptable format. For instance, UK phone numbers should be prefixed with `+44`, `44` or `0044`. |
| `current_carrier` | `"true"` | no | When set to `true`, the API retrieves and populates the current network of the phone number. This operation can be slow, depending on the network and local conditions. |
| `tags` | `string` | no | **Tags** A comma separated list of tags to query over. Useful if you want to specify the circumstances in which the request was made. If you specify multiple tags, the response comprises only requests that satisfy all of them. Searching `"foo,bar"` queries only requests tagged both `"foo"` and `"bar"`. |

## Response Type

```ts
import type { PhoneNumberValidationResponse } from "@addresszen/sdk";
```

## Errors

HTTP errors throw an `ApiError` with the HTTP `status` and the API error `code` and `message`. Network failures and aborts reject with the runtime's native error. Pass `throwOnError: false` to get `{ data, error }` instead. See [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors).

## Example

```ts title="phone-number-validation.ts"
import { createZenClient, phoneNumberValidation } from "@addresszen/sdk";

export const example = async () => {
  const client = createZenClient({ apiKey: "ak_test" });
  const { data } = await phoneNumberValidation({
    client,
    query: { query: "+12025550123" },
  });
  return data;
};
```
