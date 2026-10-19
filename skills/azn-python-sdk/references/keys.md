# API keys

The key methods show whether a key can take requests and which countries it covers. They also read limits, change settings and export usage. Everything except `key_availability` needs a [Management Key](https://docs.addresszen.com/docs/sdks/python/setup#management-key).

## Key availability

Call `key_availability`. It needs only the API key and costs nothing, so it also works as a health check.

```python title="availability.py"
from addresszen import AddressZen

with AddressZen("ak_test") as client:
    key = client.key_availability("ak_test")
    for country in key.contexts:
        print(country.emoji, country.description, country.iso_3)
    print("Default:", key.context or key.contexts[0].iso_3)
```

`contexts` lists the licensed countries; pass an `iso_3` code as `context` to [`find_address`](https://docs.addresszen.com/docs/sdks/python/endpoints/find-address). `context` is the licensed country that best matches the caller's IP address, or an empty string. `available` is `False` when the key has no lookups left, has hit a daily limit or is called from a URL it does not allow.

## Balance and limits

`key_details` returns `lookups_remaining`, the daily, monthly and per-IP limits, allowed URLs, notification settings and datasets.

```python title="details.py"
import os

from addresszen import AddressZen

with AddressZen(os.environ["ADDRESSZEN_API_KEY"]) as client:
    details = client.key_details("ak_test", user_token=os.environ["ADDRESSZEN_MANAGEMENT_KEY"])
    print(details.lookups_remaining)
```

## Update limits

Call `update_key_details` with only the settings to change. Everything else stays as it is.

```python title="update.py"
import os

from addresszen import AddressZen

with AddressZen(os.environ["ADDRESSZEN_API_KEY"]) as client:
    client.update_key_details(
        "ak_test",
        user_token=os.environ["ADDRESSZEN_MANAGEMENT_KEY"],
        daily_limit={"limit": 1000},
        allowed_urls=["https://www.example.com"],
    )
```

Nested settings are typed dictionaries from `addresszen.requests`; `None` inside one is sent as JSON `null`. `daily_limit={"limit": None}` removes the daily limit, `allowed_urls=[]` removes the URL restriction and `notifications={"enabled": False}` turns off notification emails.

## Usage and logs

`key_usage` returns totals and a daily breakdown. `key_logs` returns each billable lookup as CSV text. Both take `start` and `end` as UNIX timestamps in milliseconds.

```python title="usage.py"
import os
import time

from addresszen import AddressZen

end = int(time.time() * 1000)
start = end - 7 * 24 * 60 * 60 * 1000

with AddressZen(os.environ["ADDRESSZEN_API_KEY"]) as client:
    token = os.environ["ADDRESSZEN_MANAGEMENT_KEY"]
    usage = client.key_usage("ak_test", user_token=token, start=start, end=end)
    csv = client.key_logs("ak_test", user_token=token, start=start, end=end)
```

Pass `licensee` to either method for one [licensee's](https://docs.addresszen.com/docs/sdks/python/licensees) usage.
