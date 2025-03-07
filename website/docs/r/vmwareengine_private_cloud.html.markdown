---
# ----------------------------------------------------------------------------
#
#     ***     AUTO GENERATED CODE    ***    Type: MMv1     ***
#
# ----------------------------------------------------------------------------
#
#     This file is automatically generated by Magic Modules and manual
#     changes will be clobbered when the file is regenerated.
#
#     Please read more about how to change this file in
#     .github/CONTRIBUTING.md.
#
# ----------------------------------------------------------------------------
subcategory: "Cloud VMware Engine"
description: |-
  / Represents a private cloud resource.
---

# google\_vmwareengine\_private\_cloud

/ Represents a private cloud resource. Private clouds are zonal resources.

~> **Warning:** This resource is in beta, and should be used with the terraform-provider-google-beta provider.
See [Provider Versions](https://terraform.io/docs/providers/google/guides/provider_versions.html) for more details on beta resources.

To get more information about PrivateCloud, see:

* [API documentation](https://cloud.google.com/vmware-engine/docs/reference/rest/v1/projects.locations.privateClouds)

## Example Usage - Vmware Engine Private Cloud Basic


```hcl
resource "google_vmwareengine_private_cloud" "vmw-engine-pc" {
  provider    = google-beta
  location    = "us-west1-a"
  name        = "sample-pc"
  description = "Sample test PC."
  network_config {
    management_cidr       = "192.168.30.0/24"
    vmware_engine_network = google_vmwareengine_network.pc-nw.id
  }

  management_cluster {
    cluster_id = "sample-mgmt-cluster"
    node_type_configs {
      node_type_id = "standard-72"
      node_count   = 3
    }
  }
}

resource "google_vmwareengine_network" "pc-nw" {
  provider    = google-beta
  name        = "us-west1-default"
  location    = "us-west1"
  type        = "LEGACY"
  description = "PC network description."
}
```
## Example Usage - Vmware Engine Private Cloud Full


```hcl
resource "google_vmwareengine_private_cloud" "vmw-engine-pc" {
  provider    = google-beta
  location    = "us-west1-a"
  name        = "sample-pc"
  description = "Sample test PC."
  network_config {
    management_cidr       = "192.168.30.0/24"
    vmware_engine_network = google_vmwareengine_network.pc-nw.id
  }

  management_cluster {
    cluster_id = "sample-mgmt-cluster"
    node_type_configs {
      node_type_id = "standard-72"
      node_count   = 3
      custom_core_count = 32
    }
  }
}

resource "google_vmwareengine_network" "pc-nw" {
  provider    = google-beta
  name        = "us-west1-default"
  location    = "us-west1"
  type        = "LEGACY"
  description = "PC network description."
}
```

## Argument Reference

The following arguments are supported:


* `network_config` -
  (Required)
  Network configuration in the consumer project with which the peering has to be done.
  Structure is [documented below](#nested_network_config).

* `management_cluster` -
  (Required)
  The management cluster for this private cloud. This used for creating and managing the default cluster.
  Structure is [documented below](#nested_management_cluster).

* `location` -
  (Required)
  The location where the PrivateCloud should reside.

* `name` -
  (Required)
  The ID of the PrivateCloud.


<a name="nested_network_config"></a>The `network_config` block supports:

* `management_cidr` -
  (Required)
  Management CIDR used by VMware management appliances.

* `vmware_engine_network` -
  (Optional)
  The relative resource name of the VMware Engine network attached to the private cloud.
  Specify the name in the following form: projects/{project}/locations/{location}/vmwareEngineNetworks/{vmwareEngineNetworkId}
  where {project} can either be a project number or a project ID.

* `vmware_engine_network_canonical` -
  (Output)
  The canonical name of the VMware Engine network in
  the form: projects/{project_number}/locations/{location}/vmwareEngineNetworks/{vmwareEngineNetworkId}

* `management_ip_address_layout_version` -
  (Output)
  The IP address layout version of the management IP address range.
  Possible versions include:
  * managementIpAddressLayoutVersion=1: Indicates the legacy IP address layout used by some existing private clouds. This is no longer supported for new private clouds
  as it does not support all features.
  * managementIpAddressLayoutVersion=2: Indicates the latest IP address layout
  used by all newly created private clouds. This version supports all current features.

<a name="nested_management_cluster"></a>The `management_cluster` block supports:

* `cluster_id` -
  (Required)
  The user-provided identifier of the new Cluster. The identifier must meet the following requirements:
    * Only contains 1-63 alphanumeric characters and hyphens
    * Begins with an alphabetical character
    * Ends with a non-hyphen character
    * Not formatted as a UUID
    * Complies with RFC 1034 (https://datatracker.ietf.org/doc/html/rfc1034) (section 3.5)

* `node_type_configs` -
  (Optional)
  The map of cluster node types in this cluster,
  where the key is canonical identifier of the node type (corresponds to the NodeType).
  Structure is [documented below](#nested_node_type_configs).


<a name="nested_node_type_configs"></a>The `node_type_configs` block supports:

* `node_type_id` - (Required) The identifier for this object. Format specified above.

* `node_count` -
  (Required)
  The number of nodes of this type in the cluster.

* `custom_core_count` -
  (Optional)
  Customized number of cores available to each node of the type.
  This number must always be one of `nodeType.availableCustomCoreCounts`.
  If zero is provided max value from `nodeType.availableCustomCoreCounts` will be used.
  This cannot be changed once the PrivateCloud is created.

- - -


* `description` -
  (Optional)
  User-provided description for this private cloud.

* `project` - (Optional) The ID of the project in which the resource belongs.
    If it is not provided, the provider project is used.


## Attributes Reference

In addition to the arguments listed above, the following computed attributes are exported:

* `id` - an identifier for the resource with format `projects/{{project}}/locations/{{location}}/privateClouds/{{name}}`

* `uid` -
  System-generated unique identifier for the resource.

* `state` -
  State of the resource. New values may be added to this enum when appropriate.

* `hcx` -
  Details about a HCX Cloud Manager appliance.
  Structure is [documented below](#nested_hcx).

* `nsx` -
  Details about a NSX Manager appliance.
  Structure is [documented below](#nested_nsx).

* `vcenter` -
  Details about a vCenter Server management appliance.
  Structure is [documented below](#nested_vcenter).


<a name="nested_hcx"></a>The `hcx` block contains:

* `internal_ip` -
  (Optional)
  Internal IP address of the appliance.

* `version` -
  (Optional)
  Version of the appliance.

* `state` -
  (Optional)
  State of the appliance.
  Possible values are: `ACTIVE`, `CREATING`.

* `fqdn` -
  (Optional)
  Fully qualified domain name of the appliance.

<a name="nested_nsx"></a>The `nsx` block contains:

* `internal_ip` -
  (Optional)
  Internal IP address of the appliance.

* `version` -
  (Optional)
  Version of the appliance.

* `state` -
  (Optional)
  State of the appliance.
  Possible values are: `ACTIVE`, `CREATING`.

* `fqdn` -
  (Optional)
  Fully qualified domain name of the appliance.

<a name="nested_vcenter"></a>The `vcenter` block contains:

* `internal_ip` -
  (Optional)
  Internal IP address of the appliance.

* `version` -
  (Optional)
  Version of the appliance.

* `state` -
  (Optional)
  State of the appliance.
  Possible values are: `ACTIVE`, `CREATING`.

* `fqdn` -
  (Optional)
  Fully qualified domain name of the appliance.

## Timeouts

This resource provides the following
[Timeouts](https://developer.hashicorp.com/terraform/plugin/sdkv2/resources/retries-and-customizable-timeouts) configuration options:

- `create` - Default is 240 minutes.
- `update` - Default is 190 minutes.
- `delete` - Default is 150 minutes.

## Import


PrivateCloud can be imported using any of these accepted formats:

* `projects/{{project}}/locations/{{location}}/privateClouds/{{name}}`
* `{{project}}/{{location}}/{{name}}`
* `{{location}}/{{name}}`


In Terraform v1.5.0 and later, use an [`import` block](https://developer.hashicorp.com/terraform/language/import) to import PrivateCloud using one of the formats above. For example:

```tf
import {
  id = "projects/{{project}}/locations/{{location}}/privateClouds/{{name}}"
  to = google_vmwareengine_private_cloud.default
}
```

When using the [`terraform import` command](https://developer.hashicorp.com/terraform/cli/commands/import), PrivateCloud can be imported using one of the formats above. For example:

```
$ terraform import google_vmwareengine_private_cloud.default projects/{{project}}/locations/{{location}}/privateClouds/{{name}}
$ terraform import google_vmwareengine_private_cloud.default {{project}}/{{location}}/{{name}}
$ terraform import google_vmwareengine_private_cloud.default {{location}}/{{name}}
```

## User Project Overrides

This resource supports [User Project Overrides](https://registry.terraform.io/providers/hashicorp/google/latest/docs/guides/provider_reference#user_project_override).
