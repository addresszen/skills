# Address verification

`addressVerify` checks a US address against the USPS Coding Accuracy Support System (CASS) and returns it corrected and standardized, with its ZIP+4 code and USPS delivery data. To verify an address in another country, pass `query: { context }` with its ISO 3166-1 alpha-3 code, e.g. `"GBR"`. Outside the United States `match` is the address in the format [Retrieve Address](https://docs.addresszen.com/docs/sdks/typescript/endpoints/retrieve-address) returns, with `dataset` set; a CASS match has no `dataset`.

```ts title="address-verify.ts"
import { createZenClient, addressVerify } from "@addresszen/sdk";

const client = createZenClient({ apiKey: "ak_test" });
const { data } = await addressVerify({
  client,
  body: { query: "1010 Cauthen Ln, Alamogordo, NM 88310" },
});
const result = data.result;
if (result.match === null) {
  console.log("No match:", result.match_information);
} else if ("dataset" in result.match) {
  console.log(result.zip_code, result.match.dataset);
} else {
  console.log(result.zip_code, result.match.dpv, result.match.rdi);
}
```

Your key needs address verification enabled, or the request fails with `401`. Every verification the CASS engine answers draws on your balance, matched or not. A query that cannot be parsed into an address does not.

## Match result

A match returns the standardized address at the top level and the CASS record behind it in `match`. This is the response for the example above, trimmed:

```json
{
  "result": {
    "query": "1010 Cauthen Ln, Alamogordo, NM 88310",
    "count": 1,
    "fit": 1,
    "confidence": 1,
    "match_information": "Address verified successfully",
    "address_line_one": "1010 Cauthen Ln",
    "address_line_two": "",
    "city": "Alamogordo",
    "state": "NM",
    "zip_code": "88310-5631",
    "country_iso_2": "US",
    "match": {
      "address1": "1010 Cauthen Ln",
      "zip_code": "88310-5631",
      "delivery_point": "10",
      "carrier_route": "C019",
      "record_type": "S",
      "dpv": "Y",
      "dpv_footnotes": "AABB",
      "dpv_vacant": "N",
      "dpv_cmra": "N",
      "dpv_no_stat": "N",
      "rdi": "Y",
      "county": "Otero",
      "congressional_district": "02",
      "elot": "0134A",
      "time_zone": "MST",
      "latitude": "32.91278",
      "longitude": "-105.94904"
    }
  },
  "code": 2000,
  "message": "Success"
}
```

## CASS fields

| Field | Meaning |
| --- | --- |
| `zip_code` | Five-digit ZIP code and the four-digit add-on (ZIP+4) |
| `delivery_point` | Last two digits of the primary street number or PO Box |
| `carrier_route` | USPS carrier route, used for carrier route sorting |
| `record_type` | `S` street, `H` high-rise, `F` firm, `P` PO Box, `R` rural route or highway contract, `G` general delivery, `M` military, `C` multi-carrier, `U` unique five-digit ZIP |
| `dpv` | Delivery Point Validation (DPV) result. `Y` primary and secondary validated, `D` secondary missing, `S` extra or incorrect secondary, `N` not validated, empty if not ZIP+4 matched |
| `dpv_footnotes` | DPV footnote codes, such as `AA` (ZIP+4 matched) and `BB` (primary and secondary validated) |
| `dpv_vacant` | `Y` if USPS records the address as vacant |
| `dpv_cmra` | `Y` if the address is a Commercial Mail Receiving Agency, such as a mailbox store |
| `dpv_no_stat` | `Y` if the address is vacant, receives mail as part of a drop or has no established delivery yet |
| `rdi` | Residential Delivery Indicator: whether USPS classifies the delivery point as residential |

The DPV flags are empty strings when the address was not DPV validated. The [API reference](https://docs.addresszen.com/docs/api/address-verify) lists every field, including eLOT, county, congressional district and coordinates.

## Deliverability

Check `match.dpv`. `confidence` measures how well your input matched an address; `dpv` says whether USPS confirms it as a delivery point. The two can disagree. `123 Main St, Springfield, CO 81073` verifies with a `confidence` of `1`, a five-digit `zip_code` of `81073` and a `dpv` of `N`: the street exists but USPS does not confirm the number. Treat `dpv` `Y` as deliverable.

## Fit and confidence

Both are scores from 0 to 1. `fit` compares only the elements you sent with the matched address, so a first line with no city, state or ZIP code can score a `fit` of 1. `confidence` also counts missing elements, so the same input scores below 1. A `confidence` of 1 is a full match.

## No match

An address that cannot be verified still returns HTTP `200`, with a `null` `match`, a `count` of `0`, empty address fields and the reason in `match_information`, such as `Address not found` or `House number not valid for this street`. The wording may change, so test `match === null` rather than parsing `match_information`. CASS corrects what it can first: an address with the wrong city or state for its ZIP code still verifies, with the corrected values. This response is trimmed:

```json
{
  "result": {
    "query": "1 Nowhere Rd, Springfield, CO 81073",
    "count": 0,
    "fit": 0,
    "confidence": 0,
    "match_information": "Address not found",
    "address_line_one": "",
    "address_line_two": "",
    "city": "",
    "state": "",
    "zip_code": "",
    "country_iso_2": "",
    "match": null
  },
  "code": 2000,
  "message": "Success"
}
```

## Address in parts

Put the first address line in `query` and add either `zip_code`, or `city` and `state`. `zip_code` accepts `88310-5631`, `883105631` or `88310`. `state` takes the two-letter abbreviation.

```ts title="address-verify-parts.ts"
const { data } = await addressVerify({
  client,
  body: { query: "1010 Cauthen Ln", zip_code: "88310" },
});
```

A verification still running after 9.5 seconds fails with `429`. See [`addressVerify`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/address-verify) for the request fields and [error handling](https://docs.addresszen.com/docs/sdks/typescript/errors) for failures.

## Try it

Select **Verify** to run the verification. Edit the address in the code to try another.

```html
<button>Verify</button>
<pre></pre>
```

```javascript
  import { createZenClient, addressVerify } from "@addresszen/sdk";

  const apiKey = "ak_test"; // Replace with your own API key
  const client = createZenClient({ apiKey });

  document.querySelector("button").addEventListener("click", async () => {
    const { data } = await addressVerify({
      client,
      body: { query: "1010 Cauthen Ln, Alamogordo, NM 88310" },
    });
    document.querySelector("pre").textContent = JSON.stringify(data, null, 2);
  });
```
