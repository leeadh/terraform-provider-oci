---
layout: "oci"
page_title: "OCI: oci_identity_policy"
sidebar_current: "docs-oci-resource-identity-policy"
description: |-
  Creates and manages an OCI Policy
---

# oci_identity_policy
The `oci_identity_policy` resource creates and manages an OCI Policy

Creates a new policy in the specified compartment (either the tenancy or another of your compartments).
If you're new to policies, see [Getting Started with Policies](https://docs.us-phoenix-1.oraclecloud.com/Content/Identity/Concepts/policygetstarted.htm).

You must specify a *name* for the policy, which must be unique across all policies in your tenancy
and cannot be changed.

You must also specify a *description* for the policy (although it can be an empty string). It does not
have to be unique, and you can change it anytime with [UpdatePolicy](https://docs.us-phoenix-1.oraclecloud.com/api/#/en/identity/20160918/Policy/UpdatePolicy).

You must specify one or more policy statements in the statements array. For information about writing
policies, see [How Policies Work](https://docs.us-phoenix-1.oraclecloud.com/Content/Identity/Concepts/policies.htm) and
[Common Policies](https://docs.us-phoenix-1.oraclecloud.com/Content/Identity/Concepts/commonpolicies.htm).

After you send your request, the new object's `lifecycleState` will temporarily be CREATING. Before using the
object, first make sure its `lifecycleState` has changed to ACTIVE.

New policies take effect typically within 10 seconds.


## Example Usage

```hcl
resource "oci_identity_policy" "test_policy" {
	#Required
	compartment_id = "${var.tenancy_ocid}"
	description = "${var.policy_description}"
	name = "${var.policy_name}"
	statements = "${var.policy_statements}"

	#Optional
	defined_tags = {"Operations.CostCenter"= "42"}
	freeform_tags = {"Department"= "Finance"}
	version_date = "${var.policy_version_date}"
}
```

## Argument Reference

The following arguments are supported:

* `compartment_id` - (Required) The OCID of the compartment containing the policy (either the tenancy or another compartment).
* `defined_tags` - (Optional) (Updatable) Defined tags for this resource. Each key is predefined and scoped to a namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm). Example: `{"Operations.CostCenter": "42"}` 
* `description` - (Required) (Updatable) The description you assign to the policy during creation. Does not have to be unique, and it's changeable. 
* `freeform_tags` - (Optional) (Updatable) Free-form tags for this resource. Each tag is a simple key-value pair with no predefined name, type, or namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm). Example: `{"Department": "Finance"}` 
* `name` - (Required) The name you assign to the policy during creation. The name must be unique across all policies in the tenancy and cannot be changed. 
* `statements` - (Required) (Updatable) An array of policy statements written in the policy language. See [How Policies Work](https://docs.us-phoenix-1.oraclecloud.com/Content/Identity/Concepts/policies.htm) and [Common Policies](https://docs.us-phoenix-1.oraclecloud.com/Content/Identity/Concepts/commonpolicies.htm). 
* `version_date` - (Optional) (Updatable) The version of the policy. If null or set to an empty string, when a request comes in for authorization, the policy will be evaluated according to the current behavior of the services at that moment. If set to a particular date (YYYY-MM-DD), the policy will be evaluated according to the behavior of the services on that date. 


** IMPORTANT **
Any change to a property that does not support update will force the destruction and recreation of the resource with the new property values

## Attributes Reference

The following attributes are exported:

* `compartment_id` - The OCID of the compartment containing the policy (either the tenancy or another compartment). 
* `defined_tags` - Defined tags for this resource. Each key is predefined and scoped to a namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm). Example: `{"Operations.CostCenter": "42"}` 
* `description` - The description you assign to the policy. Does not have to be unique, and it's changeable.
* `freeform_tags` - Free-form tags for this resource. Each tag is a simple key-value pair with no predefined name, type, or namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm). Example: `{"Department": "Finance"}` 
* `id` - The OCID of the policy.
* `inactive_state` - The detailed status of INACTIVE lifecycleState.
* `name` - The name you assign to the policy during creation. The name must be unique across all policies in the tenancy and cannot be changed. 
* `state` - The policy's current state. After creating a policy, make sure its `lifecycleState` changes from CREATING to ACTIVE before using it. 
* `statements` - An array of one or more policy statements written in the policy language.
* `time_created` - Date and time the policy was created, in the format defined by RFC3339.  Example: `2016-08-25T21:10:29.600Z` 
* `version_date` - The version of the policy. If null or set to an empty string, when a request comes in for authorization, the policy will be evaluated according to the current behavior of the services at that moment. If set to a particular date (YYYY-MM-DD), the policy will be evaluated according to the behavior of the services on that date. 

## Import

Policies can be imported using the `id`, e.g.

```
$ terraform import oci_identity_policy.test_policy "id"
```
