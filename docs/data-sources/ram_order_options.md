---
page_title: "Servers.com: serverscom_ram_order_options"
---

# serverscom_ram_order_options

Lists RAM options available for a server model in a location. Use it to find the values for the `ram_size` argument of [`serverscom_dedicated_server`](../resources/dedicated_server.md).

## Example Usage

```hcl
data "serverscom_ram_order_options" "example" {
  location_id     = 1
  server_model_id = 100
}

output "ram_sizes" {
  value = [for r in data.serverscom_ram_order_options.example.ram_options : r.ram]
}
```

## Argument Reference

The following arguments are supported:

- `location_id` - (Required, int) The ID of the location. Use [`serverscom_locations`](locations.md) to find it.
- `server_model_id` - (Required, int) The ID of the server model. Use [`serverscom_server_model_order_options`](server_model_order_options.md) to find it.

## Attributes Reference

The following attributes are exported:

- `ram_options` - A list of RAM options. Each element contains:
  - `ram` - The RAM size in GB.
  - `type` - The DDR type of RAM.
