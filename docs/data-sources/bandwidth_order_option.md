---
page_title: "Servers.com: serverscom_bandwidth_order_option"
---

# serverscom_bandwidth_order_option

Get information on a bandwidth option (a traffic billing policy) available for an uplink model in a location. To list all bandwidth options, use [`serverscom_bandwidth_order_options`](bandwidth_order_options.md).

The `name` attribute is the value of the `bandwidth` argument of [`serverscom_dedicated_server`](../resources/dedicated_server.md). Bandwidth is required when a public uplink is used.

## Example Usage

```hcl
data "serverscom_bandwidth_order_option" "example" {
  location_id     = 1
  server_model_id = 100
  uplink_model_id = 400
  id              = 500
}

output "bandwidth_name" {
  value = data.serverscom_bandwidth_order_option.example.name
}
```

## Argument Reference

The following arguments are supported:

- `location_id` - (Required, int) The ID of the location. Use [`serverscom_locations`](locations.md) to find it.
- `server_model_id` - (Required, int) The ID of the server model. Use [`serverscom_server_model_order_options`](server_model_order_options.md) to find it.
- `uplink_model_id` - (Required, int) The ID of the public uplink model. Use [`serverscom_uplink_model_order_options`](uplink_model_order_options.md) to find it.
- `id` - (Required, int) The ID of the bandwidth option. Use [`serverscom_bandwidth_order_options`](bandwidth_order_options.md) to list IDs.

## Attributes Reference

The following attributes are exported:

- `id` - (int) The ID of the bandwidth option.
- `name` - (string) A human-readable name of the bandwidth option.
- `type` - (string) The type of the bandwidth option: `bytes` (a quantity of included traffic), `bandwidth` (throughput), or `unmetered` (no limits on traffic).
- `commit` - (int) The number of units included in the commit. It is `0` for an unmetered option.
