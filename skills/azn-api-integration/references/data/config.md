# Config Object

**Schema name:** `Config`

## Fields

| Field | Required | Type | Description | Example |
|---|---|---|---|---|
| `updatedAt` | yes | string | Timestamp for when the config was created | `2016-01-21T17:14:49.971Z` |
| `createdAt` | yes | string | Timestamp for when the config was updated | `2016-01-21T17:14:49.971Z` |
| `name` | yes | string | A unique name to identify the configuration payload | `woocommerce` |
| `payload` | yes | string | A serialised payload of up to `4096` characters | `{
  "removeOrganisation": false
}
` |

## Used By

- [ListConfigs](../endpoints/list-configs.md)
- [CreateConfig](../endpoints/create-config.md)
- [RetrieveConfig](../endpoints/retrieve-config.md)
- [UpdateConfig](../endpoints/update-config.md)
