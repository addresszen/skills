# Email validation

`emailValidation()` checks whether an email address can receive mail, wherever its domain is hosted. It also flags disposable, free, role and catch-all addresses.

```php title="email.php"
use AddressZen\AddressZen;
use AddressZen\Types\Email;

$client = AddressZen::client('ak_test');
$email = $client->emailValidation(['query' => 'support@addresszen.com'])->result;

if ($email instanceof Email) {
    echo $email->result, ' deliverable=', var_export($email->deliverable, true), PHP_EOL;
} else {
    echo 'Could not check: ', implode(', ', $email->suggestions), PHP_EOL;
}
```

Your key needs email validation enabled.

## Read the result

`result` is one of three values:

| `result` | Meaning | Class |
| --- | --- | --- |
| `deliverable` | The mailbox accepts mail | `Email`, with `deliverable` `true` |
| `not_deliverable` | Mail will bounce, or the domain cannot receive mail | `Email`, with `deliverable` `false` |
| `unknown` | The API could not check the address | `UnknownEmail`, with every flag `null` |

An `Email` carries four more flags, each `true` or `false`:

- `disposable`: a throwaway domain, such as temp-mail.org
- `free`: a free provider, such as Gmail or Outlook
- `role`: a shared mailbox, such as admin@ or support@
- `catchall`: the domain accepts mail for any name, so a `deliverable` result proves less

An `UnknownEmail` has the same properties typed `null`, so an `instanceof Email` check narrows them to `bool`.

## Suggested corrections

Only when the domain does not resolve or publishes no MX records. Then `suggestions` can hold corrected addresses. The API does not validate them, so check one before you use it. Every other result returns an empty list.

## Cost

One lookup for a checked address. An `unknown` result is free, and so is a domain that does not resolve or has no MX records. The API rejects an address over 320 characters with an `ApiException`.

See [`emailValidation()`](https://docs.addresszen.com/docs/sdks/php/endpoints/email-validation) for the parameters.
