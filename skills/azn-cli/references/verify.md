# azn verify

Verify and standardize US addresses against USPS CASS-certified data: `POST /verify/addresses`. Requires `api_key`. Each input counts as a paid lookup.

## Usage

```
azn verify [options] [query]
azn verify --file input.txt
azn verify --stdin
```

| Flag | Description |
|---|---|
| `-f, --file <path>` | Read one address per line |
| `--stdin` | Read one address per line from stdin |
| `-o, --out <path>` | Write CSV to a file (batch mode only) |
| `--city <city>` | City hint to disambiguate the match |
| `--state <state>` | State hint to disambiguate the match |
| `--zip <zip>` | ZIP code hint to disambiguate the match |

Exactly one of: `[query]`, `--file`, `--stdin`. Requests are tagged `cli`.

## Output

**Single input** (always JSON):

```json
{
  "query": "1600 amphitheatre pkwy mountain view ca",
  "response": {
    "result": {
      "confidence": 1,
      "fit": 1,
      "match_information": "Single Response - exact match",
      "address_line_one": "1600 Amphitheatre Pkwy",
      "address_line_two": "",
      "city": "Mountain View",
      "state": "CA",
      "zip_code": "94043-1351",
      "country_iso_2": "US"
    }
  }
}
```

The result carries the standardized, normalized address fields directly (`address_line_one`, `address_line_two`, `city`, `state`, `zip_code`), alongside a `confidence` and `fit` score and a human-readable `match_information` string. There is no absolute confidence threshold; decide per your dataset.

**Multiple inputs** (file or stdin) emit CSV by default; pass `--json` for the `{ count, results: [{ query, response }] }` shape. CSV columns:

```
query,status,confidence,fit,match_information,address_line_one,address_line_two,city,state,zip_code,country_iso_2,query_city,query_state,query_zip_code
```

A row that fails its lookup doesn't abort the batch: in CSV its `status` becomes `Error: <message>`; in JSON its entry is `{ query, error: { code, message } }`. The batch still exits `0`; filter on `status` or the `error` key to find failures. Auth/permission failures (`auth_failed`, `forbidden`) are the exception: they abort the whole run.

## Agent patterns

```bash
# Single
azn verify "1600 Amphitheatre Pkwy, Mountain View, CA 94043" | jq .response.result

# Batch
cat messy.txt | azn verify --stdin > verified.json

# Batch to CSV, keep only confident matches
cat messy.txt | azn verify --stdin > verified.csv
awk -F, '$3 >= 0.9' verified.csv
```

## Error codes

- `missing_argument`: no `[query]`, `--file`, or `--stdin` supplied
- `auth_failed`: invalid key, or key lacks paid verify permission
- `rate_limited`: back off and retry
- `invalid_input`: malformed body rejected by the API
