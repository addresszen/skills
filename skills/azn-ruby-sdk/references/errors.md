# Error handling

An HTTP error raises `AddressZen::ApiError`. A failed connection raises `AddressZen::TransportError`. Every error the SDK raises inherits from `AddressZen::Error`.

## ApiError

`ApiError` carries the HTTP status, the API error code and the decoded body.

| Reader | Contents |
| --- | --- |
| `status` | HTTP status, such as `401` |
| `code` | API error code, such as `4010`. `nil` when the body carries none |
| `message` | API error message, or `HTTP <status>` when the body carries none |
| `body` | Decoded JSON body as a hash, or the raw text when it is not JSON |

```ruby title="errors.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")

begin
  result = client.address_verify(query: "1010 Cauthen Ln, Alamogordo, NM 88310").result
rescue AddressZen::ApiError => e
  if e.status == 401
    puts "Check the key, and that address verification is enabled on it"
  else
    puts "#{e.status} #{e.code} #{e.message}"
  end
end
```

The message and body can echo the address you sent, so treat them as personal data when you log them. The [error codes guide](https://docs.addresszen.com/docs/guides/error-codes) lists each code and how to fix it.

## Other errors

| Error | When |
| --- | --- |
| `TransportError` | No response arrived: DNS, connection, TLS or timeout failure. The original exception is `cause` |
| `UnserializableResponseError` | A success response whose body is not a JSON object. `response` holds it |
| `MissingManagementKeyError` | A key, licensee or configuration operation on a client with no Management Key. Raised before any request is sent |

A keyword the method does not take raises Ruby's own `ArgumentError`, before any request.

## Catch every SDK error

Rescue `AddressZen::Error`. Every SDK error inherits from it, so one `rescue` covers API errors, transport failures and configuration mistakes.

```ruby title="catch_all.rb"
begin
  client.find_address(query: "1010 Cauthen Ln")
rescue AddressZen::Error => e
  warn e.message
end
```

## Retries

The SDK never retries. A timed-out request may still have been processed and charged, so retries are left to you. Retry an `ApiError` with status `429` or `5xx`, and a `TransportError`, with a bounded number of attempts.

## Timeouts and connection failures

Both raise `TransportError`. Check its `cause`: a timeout is a `Net::OpenTimeout` or `Net::ReadTimeout`, and a refused connection an `Errno::ECONNREFUSED`.
