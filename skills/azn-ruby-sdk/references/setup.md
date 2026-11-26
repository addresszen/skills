# Setup

Install `addresszen`, then create a client with your API key. The SDK needs Ruby 3.3 or later and nothing else.

## Install

```bash
gem install addresszen
```

Or add it to your Gemfile:

```ruby title="Gemfile"
gem "addresszen"
```

## Create a client

Pass your API key as `api_key:`.

```ruby title="client.rb"
require "addresszen"

client = AddressZen::Client.new(api_key: "ak_test")
```

A client holds no connection, so one instance can serve a whole application, across threads.

## Management Key

Key details, usage and logs, licensees and configurations need your Management Key, which begins `uk_`. Pass it as `management_key:`. It grants control of your account, so keep it on your server and out of version control.

```ruby title="management.rb"
client = AddressZen::Client.new(
  api_key: "ak_test",
  management_key: ENV.fetch("ADDRESSZEN_MANAGEMENT_KEY")
)

puts client.key_details("ak_test").result.lookups_remaining
```

A client without a Management Key raises `AddressZen::MissingManagementKeyError` before sending a request that needs one.

## Client options

| Option | Purpose |
| --- | --- |
| `api_key:` | Required. The API key, or a licensee key beginning `sl_` |
| `management_key:` | The Management Key for account operations |
| `base_url:` | Defaults to `https://api.addresszen.com/v1` |
| `timeout:` | Seconds allowed to connect, and again for each read and write. Defaults to 30 |
| `user_agent:` | Your application's identifier, sent ahead of the SDK and Ruby versions, for example `my-app/1.0 addresszen-ruby-sdk/0.1.0 ruby/3.4.1` |
| `transport:` | Replaces Net::HTTP. See below |

## Set a request timeout

Pass `timeout:` in seconds. A request that runs past it raises `AddressZen::TransportError`, as described in [error handling](https://docs.addresszen.com/docs/sdks/ruby/errors).

```ruby title="timeout.rb"
client = AddressZen::Client.new(api_key: "ak_test", timeout: 5)
```

## Custom transport

Pass any object with a `call(request)` method as `transport:`. It receives an `AddressZen::Request` (`http_method`, `url`, `headers`, `body`) and returns an `AddressZen::Response` (`status`, `headers`, `body`). The client builds the request, including credentials, and reads the response, so a transport only moves bytes.

```ruby title="faraday.rb"
require "faraday"

faraday = Faraday.new
transport = lambda do |request|
  response = faraday.run_request(
    request.http_method.downcase.to_sym, request.url, request.body, request.headers
  )
  AddressZen::Response.new(status: response.status, headers: response.headers.to_h,
                           body: response.body.to_s)
end

client = AddressZen::Client.new(api_key: "ak_test", transport: transport)
```

A transport is also the simplest way to stub the API in your own tests.

## Credentials

The API key goes in the `Authorization` header of every address, place, email and phone request. The Management Key goes in the same header of every key, licensee and configuration request, and nowhere else. `key_availability` and `retrieve_config` send no credentials.

To bill requests to a [licensee](https://docs.addresszen.com/docs/sdks/ruby/licensees), create a client with the licensee's `sl_` key as `api_key:`.

## User-Agent

Every request carries `User-Agent: addresszen-ruby-sdk/<version> ruby/<Ruby version>`, such as `addresszen-ruby-sdk/0.1.0 ruby/3.4.1`. The header holds no credentials or address data.
