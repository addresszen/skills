# How it Works

Address Lookup can be attached to any form with pre-existing address inputs.

When initialized it will:
1. Identify the primary input to bind the Address Lookup dropdown. This defaults to `outputFields.line_1` but you can separately specify `inputField` to indicate where you want the dropdown to bind.
2. Pipe address results to the fields defined in `outputFields`.
3. Perform a key check to determine whether it is usable. If the check fails, initialization is aborted. Use the `onFailedCheck` callback to update your page for manual address entry.

Address Lookup will mutate the DOM slightly for accessibility reasons. For more information see [DOM Changes](https://docs.addresszen.com/docs/address-lookup/behaviours#dom-changes)
