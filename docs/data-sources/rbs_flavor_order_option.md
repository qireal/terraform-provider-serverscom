---
page_title: "Servers.com: serverscom_rbs_flavor_order_option"
---

# serverscom_rbs_flavor_order_option

Get information on a Remote Block Storage (RBS) flavor in a location. A flavor defines the IOPS and bandwidth per GB of volume size and the minimum volume size. To see all flavors in a location, use [`serverscom_rbs_flavor_order_options`](rbs_flavor_order_options.md).

~> **Known issue:** In the current provider version the schema of this data source requires `location_id` and `id`, but its read function takes the flavor ID from a `flavor_id` value that is not part of the schema. As a result, the lookup does not complete successfully. Until this is fixed, use [`serverscom_rbs_flavor_order_options`](rbs_flavor_order_options.md), which returns the same attributes for all flavors in a location.

## Example Usage

Get the RBS flavor by ID:

```hcl
data "serverscom_rbs_flavor_order_option" "example" {
  location_id = 1
  id          = 2
}

output "rbs_flavor_min_size" {
  value = data.serverscom_rbs_flavor_order_option.example.min_size_gb
}
```

## Argument Reference

The following arguments are supported:

- `location_id` - (Required, int) The ID of the location. Use [`serverscom_locations`](locations.md) to find it.
- `id` - (Required, int) The ID of the RBS flavor. Use [`serverscom_rbs_flavor_order_options`](rbs_flavor_order_options.md) to list IDs.

## Attributes Reference

The following attributes are exported:

- `id` - (int) The ID of the RBS flavor. Pass it as `flavor_id` to [`serverscom_rbs_volume`](../resources/rbs_volume.md).
- `name` - (string) The flavor name.
- `iops_per_gb` - (number) The Input/Output Operations Per Second (IOPS) per 1 GB of volume size.
- `bandwidth_per_gb` - (number) Bandwidth per 1 GB of volume size (MB/s).
- `min_size_gb` - (int) The minimum volume size in GB.
