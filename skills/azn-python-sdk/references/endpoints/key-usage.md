# `key_usage`

Usage Stats

Reports the number of lookups a key consumed over a date range, as a total and a daily breakdown.

The range defaults to the last 21 days. `start` and `end` take UNIX timestamps in milliseconds, and `end` defaults to the current time. The maximum range is 90 days.

Query at most three tags at once.

## Endpoint

`GET /keys/{key}/usage`

See the [API reference](https://docs.addresszen.com/docs/api/key-usage) for this endpoint.

This operation needs a Management Key. Pass it as the required `user_token` keyword argument; the client sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/python/setup).

## Import

```python
from addresszen import AddressZen
```

Call `key_usage` on the `AddressZen` client. Path parameters are positional; query and body parameters are keyword-only.

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `str` | yes | **API Key** The API Key to retrieve. Begins `ak_`. |

## Query Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `start` | `int` | no | **Start Timestamp** A start date/time in the form of a UNIX Timestamp in milliseconds. E.g. `1418556452651` |
| `end` | `int` | no | **End Timestamp** An end date/time in the form of a UNIX Timestamp in milliseconds. E.g. `1418556477882` |
| `tags` | `str` | no | **Tags** A comma separated list of tags to query over. Useful if you want to specify the circumstances in which the request was made. If you specify multiple tags, the response comprises only requests that satisfy all of them. Searching `"foo,bar"` queries only requests tagged both `"foo"` and `"bar"`. |
| `licensee` | `str` | no | **Licensee Key** Uniquely identifies a licensee. |

## Response Type

```python
from addresszen.types import KeyUsageResult
```

## Errors

Unsuccessful HTTP responses raise `APIError` or a subclass, with the HTTP `status` and the API error `code` and `message`. Connection failures and timeouts raise `TransportError`. Unexpected responses raise `ProtocolError`. All derive from `ClientError`. See [error handling](https://docs.addresszen.com/docs/sdks/python/errors).

## Example

```python title="key_usage.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    usage = client.key_usage("ak_test", user_token="uk_example")
```
