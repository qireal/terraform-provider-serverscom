---
page_title: "Servers.com: serverscom_bandwidth_order_options"
---

# serverscom_bandwidth_order_options

Lists bandwidth options (traffic billing policies) available for an uplink model in a location, with optional filtering. Use it to find the name for the `bandwidth` argument of [`serverscom_dedicated_server`](../resources/dedicated_server.md).

## Example Usage

Order a server with the first unmetered bandwidth option of a public uplink:

```hcl
data "serverscom_uplink_model_order_options" "public" {
  location_id     = 1
  server_model_id = 100

  filter {
    type       = "public"
    redundancy = true
  }
}

data "serverscom_bandwidth_order_options" "unmetered" {
  location_id     = 1
  server_model_id = 100
  uplink_model_id = data.serverscom_uplink_model_order_options.public.uplink_models[0].id

  filter {
    type = "unmetered"
  }
}

resource "serverscom_dedicated_server" "node_1" {
  # ...
  public_uplink = data.serverscom_uplink_model_order_options.public.uplink_models[0].name
  bandwidth     = data.serverscom_bandwidth_order_options.unmetered.bandwidth_options[0].name
}
```

## Argument Reference

The following arguments are supported:

- `location_id` - (Required, int) The ID of the location. Use [`serverscom_locations`](locations.md) to find it.
- `server_model_id` - (Required, int) The ID of the server model. Use [`serverscom_server_model_order_options`](server_model_order_options.md) to find it.
- `uplink_model_id` - (Required, int) The ID of the public uplink model. Use [`serverscom_uplink_model_order_options`](uplink_model_order_options.md) to find it.
- `filter` - (Optional, block) A block to filter the returned options. Supports:
  - `type` - (Optional, string) The type of the bandwidth option: `bytes`, `bandwidth`, or `unmetered`.

## Attributes Reference

The following attributes are exported:

- `bandwidth_options` - A list of bandwidth options. Each element contains:
  - `id` - The ID of the bandwidth option.
  - `name` - A human-readable name of the bandwidth option.
  - `type` - The type of the bandwidth option: `bytes`, `bandwidth`, or `unmetered`.
  - `commit` - The number of units included in the commit. It is `0` for an unmetered option.
