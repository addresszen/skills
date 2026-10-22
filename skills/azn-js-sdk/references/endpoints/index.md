# Endpoints

Each API operation is one function. Operations are grouped by resource. Examples use the `ak_test` key and placeholder identifiers; replace them with your own before running.

## Address Search

| Function | Endpoint | Auth | Summary |
| -------- | -------- | ---- | ------- |
| [`addressVerify`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/address-verify) | `POST /verify/addresses` | API key | Verify Address |
| [`findAddress`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/find-address) | `GET /autocomplete/addresses` | API key | Find Address |
| [`retrieveAddress`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/retrieve-address) | `GET /autocomplete/addresses/{address}/usa` | API key | Retrieve Address |

## Keys

| Function | Endpoint | Auth | Summary |
| -------- | -------- | ---- | ------- |
| [`keyAvailability`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/key-availability) | `GET /keys/{key}` | Key in path | Availability |
| [`keyDetails`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/key-details) | `GET /keys/{key}/details` | Management Key | Details |
| [`updateKeyDetails`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/update-key-details) | `PUT /keys/{key}/details` | Management Key | Update Details |
| [`keyUsage`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/key-usage) | `GET /keys/{key}/usage` | Management Key | Usage Stats |
| [`keyLogs`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/key-logs) | `GET /keys/{key}/lookups` | Management Key | Logs (CSV) |

## Licensees

| Function | Endpoint | Auth | Summary |
| -------- | -------- | ---- | ------- |
| [`listLicensees`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/list-licensees) | `GET /keys/{key}/licensees` | Management Key | List |
| [`createLicensee`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/create-licensee) | `POST /keys/{key}/licensees` | Management Key | Create |
| [`deleteLicensee`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/delete-licensee) | `DELETE /keys/{key}/licensees/{licensee}` | Management Key | Cancel |
| [`retrieveLicensee`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/retrieve-licensee) | `GET /keys/{key}/licensees/{licensee}` | Management Key | Retrieve |
| [`updateLicensee`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/update-licensee) | `POST /keys/{key}/licensees/{licensee}` | Management Key | Update |
| [`regenerateLicenseeKey`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/regenerate-licensee-key) | `POST /keys/{key}/licensees/{licensee}/regenerate-key` | Management Key | Regenerate Key |

## Configs

| Function | Endpoint | Auth | Summary |
| -------- | -------- | ---- | ------- |
| [`listConfigs`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/list-configs) | `GET /keys/{key}/configs` | Management Key | List |
| [`createConfig`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/create-config) | `POST /keys/{key}/configs` | Management Key | Create |
| [`deleteConfig`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/delete-config) | `DELETE /keys/{key}/configs/{config}` | Management Key | Delete |
| [`retrieveConfig`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/retrieve-config) | `GET /keys/{key}/configs/{config}` | Key in path | Retrieve |
| [`updateConfig`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/update-config) | `POST /keys/{key}/configs/{config}` | Management Key | Update |

## Emails

| Function | Endpoint | Auth | Summary |
| -------- | -------- | ---- | ------- |
| [`emailValidation`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/email-validation) | `GET /emails` | API key | Email Validation |

## Phone Numbers

| Function | Endpoint | Auth | Summary |
| -------- | -------- | ---- | ------- |
| [`phoneNumberValidation`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/phone-number-validation) | `GET /phone_numbers` | API key | Phone Number Validation |

## Place Search

| Function | Endpoint | Auth | Summary |
| -------- | -------- | ---- | ------- |
| [`findPlace`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/find-place) | `GET /places` | API key | Find Place |
| [`resolvePlace`](https://docs.addresszen.com/docs/sdks/typescript/endpoints/resolve-place) | `GET /places/{place}` | API key | Resolve Place |
