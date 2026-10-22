# `update_key_details`

Update Details

Updates a key's settings and returns its private details. Only the fields you send change. A key on an unlimited plan ignores changes to `datasets`, `daily_limit` and `monthly_limit`. Datasets set by your plan cannot be changed here: sending one with a different value returns a 400.

## Endpoint

`PUT /keys/{key}/details`

See the [API reference](https://docs.addresszen.com/docs/api/update-key-details) for this endpoint.

This operation needs a Management Key. Pass it as the required `user_token` keyword argument; the client sends it in the `Authorization` header. See [setup](https://docs.addresszen.com/docs/sdks/python/setup).

## Import

```python
from addresszen import AddressZen
```

Call `update_key_details` on the `AddressZen` client. Path parameters are positional; query and body parameters are keyword-only.

## Path Parameters

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `key` | `str` | yes | **API Key** The API Key. Begins `ak_`. |

## Query Parameters

_None._

## Request Body

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| `name` | `str` | no | A name for the key |
| `daily_limit` | `requests.UpdateKeyDetailsDailyLimit` | no |  |
| `monthly_limit` | `requests.UpdateKeyDetailsMonthlyLimit` | no |  |
| `individual_limit` | `requests.UpdateKeyDetailsIndividualLimit` | no |  |
| `allowed_urls` | `list[str]` | no | A list of allowed URLs. An empty list disables the check. Up to 10 allowed. A request is allowed when its `Origin` or `Referer` header matches an entry. Use one of these formats: - `https://www.example.com` allows one site. Scheme and host must match - `*.example.com` allows the domain and all its subdomains See [Allowed URLs](https://docs.addresszen.com/docs/guides/allowed-urls). |
| `redact_days` | `int` | no | Number of days to preserve personal data stored in your key usage history. Set to 0 to prevent personal data storage |
| `notifications` | `requests.UpdateKeyDetailsNotifications` | no |  |
| `ip_forwarding` | `bool` | no | Accept IP addresses forwarded in the `AZ-Source-IP` header |
| `datasets` | `requests.UpdateKeyDetailsDatasets` | no | Datasets you can switch on or off for this key. Datasets set by your plan (`paf`, `mr`, `nyb`, `ecad`, `ecaf`) cannot be changed here: sending one with a different value returns a 400. |

Nested settings are typed dictionaries from `addresszen.requests`.

```python
class UpdateKeyDetailsDailyLimit(TypedDict):
    limit: NotRequired[int | None]

class UpdateKeyDetailsMonthlyLimit(TypedDict):
    limit: NotRequired[int | None]

class UpdateKeyDetailsIndividualLimit(TypedDict):
    limit: NotRequired[int | None]

class UpdateKeyDetailsNotifications(TypedDict):
    emails: NotRequired[list[str]]
    enabled: NotRequired[bool]
    balance_threshold: NotRequired[int | None]
    no_balance: NotRequired[bool]
    limit_reached: NotRequired[bool]

class UpdateKeyDetailsDatasets(TypedDict):
    pafa: NotRequired[bool]
    pafw: NotRequired[bool]
    usps: NotRequired[bool]
    hereap: NotRequired[bool]
    herehk: NotRequired[bool]
    herei: NotRequired[bool]
    herem: NotRequired[bool]
    heremea: NotRequired[bool]
    heremeas: NotRequired[bool]
    herena: NotRequired[bool]
    hereo: NotRequired[bool]
    heresa: NotRequired[bool]
    heret: NotRequired[bool]
    hereee: NotRequired[bool]
    herewe: NotRequired[bool]
    phone: NotRequired[bool]
    email: NotRequired[bool]
    gnaf: NotRequired[bool]
    kadaster: NotRequired[bool]
    kartverket: NotRequired[bool]
    sdfi: NotRequired[bool]
    cannar: NotRequired[bool]
    fodbosa: NotRequired[bool]
    mois: NotRequired[bool]
    upujp: NotRequired[bool]
    bev: NotRequired[bool]
    ban: NotRequired[bool]
    swt: NotRequired[bool]
    ab: NotRequired[bool]
    abp: NotRequired[bool]
    nip: NotRequired[bool]
    gbrcleanse: NotRequired[bool]
    uspscleanse: NotRequired[bool]
```

## Response Type

```python
from addresszen.types import UpdateKeyDetailsResult
```

## Errors

Unsuccessful HTTP responses raise `APIError` or a subclass, with the HTTP `status` and the API error `code` and `message`. Connection failures and timeouts raise `TransportError`. Unexpected responses raise `ProtocolError`. All derive from `ClientError`. See [error handling](https://docs.addresszen.com/docs/sdks/python/errors).

## Example

```python title="update_key_details.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    details = client.update_key_details("ak_test", user_token="uk_example", daily_limit={"limit": 1000})
```
