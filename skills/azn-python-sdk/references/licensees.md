# Licensees

A licensee is one of your customers using AddressZen through your key. Sub-licensing lets a platform serve many customers from one account and one bill while tracking each customer's usage separately.

Your key must be enabled for sub-licensing; [contact us](https://addresszen.com/contact) to switch one over. Every licensee method needs a [Management Key](https://docs.addresszen.com/docs/sdks/python/setup#management-key). The [sub-licensing guide](https://docs.addresszen.com/docs/guides/sublicensing) covers billing.

## Create a licensee

Call `create_licensee` with the customer's name and address. The new licensee's own key, beginning `sl_`, is in `key`.

```python title="create_licensee.py"
import os

from addresszen import AddressZen

with AddressZen(os.environ["ADDRESSZEN_API_KEY"]) as client:
    licensee = client.create_licensee(
        "ak_test",
        user_token=os.environ["ADDRESSZEN_MANAGEMENT_KEY"],
        name="Example Inc",
        address="1010 Cauthen Ln, Alamogordo, NM",
        postcode="88310",
    )
    print(licensee.key)
```

`postcode` takes the customer's ZIP or postal code, whatever their country.

## List licensees

`list_licensees` returns 10 per call, or up to 100 with `limit`, oldest first. Canceled licensees are left out. `query` filters by name. For the next page, pass the last licensee's `id` as `starting_after`.

## Update or cancel a licensee

Pass your key and the licensee's `sl_` key:

- `update_licensee` changes the address, ZIP or postal code, allowed URLs (`whitelist`) or daily limit. The name cannot change after creation
- `regenerate_licensee_key` issues a new `sl_` key and stops the old one immediately
- `delete_licensee` cancels the licensee and stops its key. Contact us to undo it

Pass `licensee` to [`key_usage`](https://docs.addresszen.com/docs/sdks/python/keys#usage-and-logs) or `key_logs` to report one licensee's usage.
