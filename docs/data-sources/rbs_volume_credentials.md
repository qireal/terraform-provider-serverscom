---
page_title: "Servers.com: serverscom_rbs_volume_credentials"
---

# serverscom_rbs_volume_credentials

Get the iSCSI connection credentials of a Remote Block Storage (RBS) volume. Use them to configure CHAP authentication on a host, see [Getting started](https://www.servers.com/docs/rbs/getting-started) in the knowledge base.

~> **Warning:** The `password` attribute is not marked as sensitive by the provider and is stored in plain text in the Terraform state. Use a remote backend with encryption and access control, and mark any output that exposes it with `sensitive = true`.

## Example Usage

```hcl
data "serverscom_rbs_volume_credentials" "example" {
  volume_id = serverscom_rbs_volume.data.id
}

output "chap_username" {
  value     = data.serverscom_rbs_volume_credentials.example.username
  sensitive = true
}

output "chap_password" {
  value     = data.serverscom_rbs_volume_credentials.example.password
  sensitive = true
}
```

## Argument Reference

The following arguments are supported:

- `volume_id` - (Required, string) The ID of the RBS volume.

## Attributes Reference

The following attributes are exported:

- `id` - (string) The ID of the RBS volume.
- `username` - (string) iSCSI (CHAP) username for authentication.
- `password` - (string) iSCSI (CHAP) password for authentication.
- `target_iqn` - (string) iSCSI Qualified Name (IQN) of the volume.
- `ip_address` - (string) A private IP address of the volume to connect to (port `3260`).
