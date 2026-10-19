# Setup

Install `addresszen` from PyPI, create one `AddressZen` client with your API key and reuse it for every request.

```bash
pip install addresszen
```

```python title="client.py"
import os

from addresszen import AddressZen

with AddressZen(os.environ["ADDRESSZEN_API_KEY"]) as client:
    hits = client.find_address(query="100 Queen St W, Toronto", context="CAN").hits
```

The client keeps a pool of HTTP connections open. Use it as a context manager, or call `close()` when your process finishes.

## Client options

| Argument | Default | Purpose |
| --- | --- | --- |
| `api_key` | required | Your API key, beginning `ak_` |
| `timeout` | `10.0` | Seconds to wait for each request |
| `base_url` | `https://api.addresszen.com/v1` | API root. Change it only to point at a test server |
| `transport` | `None` | An HTTPX transport, such as `httpx.MockTransport` in tests |

Every argument after `api_key` is keyword-only.

## Management Key

To read or change your account: key details, usage, logs, licensees and configs. A Management Key begins `uk_`. Pass it to each of those methods as `user_token`; the SDK sends it in the `Authorization` header, never in the URL.

A Management Key controls your account. Keep it in a secret store on your server, never in a browser or mobile app.

## Async code

The client is synchronous. From an async application, run calls in a worker thread with `asyncio.to_thread`.

## User-Agent

Every request carries `User-Agent: addresszen-python-sdk/<version>`, such as `addresszen-python-sdk/0.1.0`. The header holds no credentials or address data.
