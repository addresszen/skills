# Verify Address

**Endpoint:** `POST /verify/addresses`

**Operation ID:** `AddressVerify`

**Tags:** Address Search

Verifies an address against the USPS Coding Accuracy Support System (CASS) and returns it standardized and corrected.

Submit the whole address in `query`, or the first address line in `query` with either `zip_code`, or `city` and `state`. A freeform `query` is parsed into those components before the search runs.

A match returns the standardized address lines, city, state and ZIP+4, scored by `fit` and `confidence`. It also carries the CASS record behind the match: delivery point, DPV flags, carrier route, eLOT, county, congressional district, RDI, time zone and coordinates. CASS corrects what it can, so an address with the wrong city or state for its ZIP code still verifies, with the corrected values.

An address that cannot be verified returns `200` with a `count` of `0`, a `null` `match` and empty address fields. `match_information` says why, e.g. `Address not found` or `House number not valid for this street`. It is for people to read and its wording may change, so test `match` for `null` rather than parsing it.

In the United States every verification the CASS engine answers draws on your balance, matched or not. A query that cannot be parsed into an address does not. Elsewhere only a match draws on your balance. A key without address verification enabled returns `401`. A verification still running after 9.5 seconds aborts with `429`.

## Countries

Verify defaults to the United States, where it is CASS certified. Pass `context` with an ISO 3166-1 alpha-3 country code to verify an address elsewhere, e.g. `context=GBR` or `context=FRA`. The address datasets your key is licensed for decide which countries it can verify.

Outside the United States there is no CASS record, so `match` is the address in the same format Retrieve Address returns: USPS-style field names, empty strings where the country has no equivalent, and the raw dataset record in `native`. Check `dataset` to tell the two apart: it is present on every non-US match and absent from a CASS match.

The top-level fields (`address_line_one`, `address_line_two`, `city`, `state`, `zip_code`, `country_iso_2`) are populated for every country, along with `confidence` and `fit`.

## Parameters

| Name | In | Required | Type | Description |
|---|---|---|---|---|
| `tags` | query | no | string | A comma separated list of tags to query over. |
| `context` | query | no | string | Identify the country of the address to verify. Defaults to United States (USA) |

## Request Body

Content-Type: `application/json` (required)

| Field | Required | Type | Description |
|---|---|---|---|
| `query` | yes | string | Address input to verify. |
| `zip_code` | no | string | Specify the ZIP code of an address. The following formats are accepted: `81073-1119`, `810731119`, `81073`. |
| `city` | no | string | City of an address. |
| `state` | no | string | State of an address. For the US, use the 2-letter state abbreviation. |

## Request Samples

**curl**

```bash
curl -X POST 'https://api.addresszen.com/v1/verify/addresses' \
  -H 'Authorization: api_key="ak_test"' \
  -H 'Content-Type: application/json' \
  -d '{
    "query": "123 Main St, Springfield, IL 62701"
  }'
```

**JavaScript**

```javascript
import { createZenClient, addressVerify } from '@addresszen/sdk';

const client = createZenClient({ apiKey: 'ak_test' });

const { data } = await addressVerify({
  client,
  body: {
    query: '123 Main St, Springfield, IL 62701',
  },
});
```

**Python**

```python
# pip install addresszen
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    result = client.address_verify(query="123 Main St, Springfield, IL 62701")
```

**Ruby**

```ruby
require "net/http"
require "json"

uri = URI("https://api.addresszen.com/v1/verify/addresses")
body = {
  query: "123 Main St, Springfield, IL 62701",
}
response = Net::HTTP.post(uri, body.to_json, "Authorization" => 'api_key="ak_test"', "Content-Type" => "application/json")
result = JSON.parse(response.body)["result"]
```

**PHP**

```php
<?php
$ch = curl_init("https://api.addresszen.com/v1/verify/addresses");
curl_setopt_array($ch, [
  CURLOPT_POST => true,
  CURLOPT_HTTPHEADER => ['Authorization: api_key="ak_test"', "Content-Type: application/json"],
  CURLOPT_POSTFIELDS => json_encode([
    "query" => "123 Main St, Springfield, IL 62701",
  ]),
  CURLOPT_RETURNTRANSFER => true,
]);
$result = json_decode(curl_exec($ch), true)["result"];
```

## Response Schema (200)

| Field | Required | Type | Description |
|---|---|---|---|
| `code` | yes | `2000` |  |
| `message` | yes | `Success` |  |
| `result` | yes | [UsaVerifyMatch](../data/usa-verify-match.md) \| [UsaVerifyNoMatch](../data/usa-verify-no-match.md) |  |

## See also

- [Live docs](https://docs.addresszen.com/docs/api/address-verify)
- [Authentication](../authentication.md)
- [Error Codes](../error-codes.md)
- [Data Models](../data/)
