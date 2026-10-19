# Responses, arguments and testing

Every method takes the API's parameters as Python arguments and returns the API's `result` as a Pydantic model.

## Return values

The `result` field of the API response, as a Pydantic v2 model or a list of models. Read fields as attributes, or call `model_dump()` for a dictionary. Fields the API adds after your SDK version still appear in `model_dump()`. Option fields are plain strings, so new values come through. A `native` record from a dataset your SDK version does not know arrives as a dictionary.

`key_logs` returns CSV text as a `str` instead, and `retrieve_address` with `filter` returns a dictionary of only the fields you asked for, such as `filter="line_1,city,zip_code"`.

## Arguments

Path parameters, such as the key, are positional. Everything else is keyword-only. The SDK leaves out any argument set to `None`, so the API applies its default, and sends `False`, `0` and `""` as given. Lists, such as `dataset`, are joined with commas.

Before sending, the SDK checks each argument against the ranges, lengths and allowed values in the spec and raises `ValueError` on a failure. `help(AddressZen.address_verify)` lists every argument and its limits.

## Types

Response models are in `addresszen.types`, such as `UsaVerifyMatch` and `Address`. Typed dictionaries for nested settings are in `addresszen.requests`. The package ships `py.typed`, so type checkers read them with no stubs.

## Testing without the network

Pass an `httpx.MockTransport` as `transport` and every request goes to your handler instead of the API.

```python title="test_verify.py"
import httpx
import pytest

from addresszen import AddressZen, PaymentRequiredError

def out_of_lookups(request: httpx.Request) -> httpx.Response:
    return httpx.Response(402, json={"code": 4020, "message": "Balance depleted"})

def test_empty_balance() -> None:
    with AddressZen("ak_test", transport=httpx.MockTransport(out_of_lookups)) as client:
        with pytest.raises(PaymentRequiredError) as error:
            client.address_verify(query="1010 Cauthen Ln, Alamogordo, NM 88310")
    assert error.value.code == 4020
```

A mocked success needs the API's envelope, `{"code": 2000, "result": ...}`, around a result that matches the response schema. Anything else raises `ProtocolError`.
