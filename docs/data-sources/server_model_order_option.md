---
page_title: "Servers.com: serverscom_server_model_order_option"
---

# serverscom_server_model_order_option

Get information on a dedicated server model (chassis). The data source exposes CPU, RAM, RAID controller, and drive slot attributes. To list all models in a location, use [`serverscom_server_model_order_options`](server_model_order_options.md).

~> **Known issue:** In the current provider version the schema of this data source accepts `id` and `server_model_id`, but its read function looks up the model by a `location_id` value that is not part of the schema. As a result, the lookup does not complete successfully. Until this is fixed, use [`serverscom_server_model_order_options`](server_model_order_options.md), which returns the same model attributes (except `drive_slots`) for a location.

The `name` attribute is the value of the `server_model` argument of [`serverscom_dedicated_server`](../resources/dedicated_server.md). The `id` is the `server_model_id` input of the other order options data sources: [drive models](drive_model_order_options.md), [operating systems](operating_system_order_options.md), [RAM](ram_order_options.md), [uplink models](uplink_model_order_options.md), and [bandwidth](bandwidth_order_options.md).

## Example Usage

The arguments below are the ones the schema currently requires:

```hcl
data "serverscom_server_model_order_option" "example" {
  id              = 100
  server_model_id = 100
}
```

## Argument Reference

The following arguments are supported:

- `id` - (Required, int) The ID of the server model.
- `server_model_id` - (Required, int) The ID of the server model.

## Attributes Reference

The following attributes are exported:

- `id` - (int) The ID of the server model.
- `name` - (string) The name of the server model.
- `cpu_name` - (string) The name of the CPU model.
- `cpu_count` - (int) The number of CPUs.
- `cpu_cores_count` - (int) The number of physical cores per CPU.
- `cpu_frequency` - (int) The CPU frequency in MHz.
- `ram` - (int) The default RAM size in GB.
- `ram_type` - (string) The DDR type of RAM.
- `max_ram` - (int) The maximum RAM size available for the server model in GB.
- `has_raid_controller` - (bool) Whether the server model has a RAID controller.
- `raid_controller_name` - (string) The name of the RAID controller. Empty if there is no RAID controller.
- `drive_slots_count` - (int) The number of drive slots.
- `drive_slots` - (list) Drive slots of the server model. Each element contains:
  - `position` - (int) The slot position, starting from `0`. This is the `position` of the `slot` block in [`serverscom_dedicated_server`](../resources/dedicated_server.md).
  - `interface` - (string) The slot interface.
  - `form_factor` - (string) The slot form factor.
  - `drive_model_id` - (int) The ID of the drive model in the slot.
  - `hot_swappable` - (bool) Whether the drive in the slot is hot swappable.
