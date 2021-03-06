---
layout: "oci"
page_title: "OCI: oci_core_dhcp_options"
sidebar_current: "docs-oci-datasource-core-dhcp_options"
description: |-
  Provides a list of DhcpOptions
---

# Data Source: oci_core_dhcp_options
The `oci_core_dhcp_options` data source allows access to the list of OCI dhcp_options

Lists the sets of DHCP options in the specified VCN and specified compartment.
The response includes the default set of options that automatically comes with each VCN,
plus any other sets you've created.


## Example Usage

```hcl
data "oci_core_dhcp_options" "test_dhcp_options" {
	#Required
	compartment_id = "${var.compartment_id}"
	vcn_id = "${oci_core_vcn.test_vcn.id}"

	#Optional
	display_name = "${var.dhcp_options_display_name}"
	state = "${var.dhcp_options_state}"
}
```

## Argument Reference

The following arguments are supported:

* `compartment_id` - (Required) The OCID of the compartment.
* `display_name` - (Optional) A filter to return only resources that match the given display name exactly. 
* `state` - (Optional) A filter to only return resources that match the given lifecycle state.  The state value is case-insensitive. 
* `vcn_id` - (Required) The OCID of the VCN.


## Attributes Reference

The following attributes are exported:

* `options` - The list of dhcp_options.

### DhcpOptions Reference

The following attributes are exported:

* `compartment_id` - The OCID of the compartment containing the set of DHCP options.
* `defined_tags` - Defined tags for this resource. Each key is predefined and scoped to a namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm).  Example: `{"Operations.CostCenter": "42"}` 
* `display_name` - A user-friendly name. Does not have to be unique, and it's changeable. Avoid entering confidential information. 
* `freeform_tags` - Free-form tags for this resource. Each tag is a simple key-value pair with no predefined name, type, or namespace. For more information, see [Resource Tags](https://docs.us-phoenix-1.oraclecloud.com/Content/General/Concepts/resourcetags.htm).  Example: `{"Department": "Finance"}` 
* `id` - Oracle ID (OCID) for the set of DHCP options.
* `options` - The collection of individual DHCP options.
	* `type` - The specific DHCP option. Either `DomainNameServer` (for [DhcpDnsOption](https://docs.us-phoenix-1.oraclecloud.com/api/#/en/iaas/20160918/DhcpDnsOption/)) or `SearchDomain` (for [DhcpSearchDomainOption](https://docs.us-phoenix-1.oraclecloud.com/api/#/en/iaas/20160918/DhcpSearchDomainOption/)). 
	* `custom_dns_servers` -  Used only when `type` is `DomainNameServer`. If you set `server_type` to `CustomDnsServer`, specify the IP address of at least one DNS server of your choice (three maximum).
	* `server_type` - Used only when `type` is `DomainNameServer`. It can be set to one of the following values: 
	    * `VcnLocal`: Reserved for future use.
	    * `VcnLocalPlusInternet`: Also referred to as "Internet and VCN Resolver". Instances can resolve internet hostnames (no Internet Gateway is required), and can resolve hostnames of instances in the VCN. This is the default value in the default set of DHCP options in the VCN. For the Internet and VCN Resolver to work across the VCN, there must also be a DNS label set for the VCN, a DNS label set for each subnet, and a hostname for each instance. The Internet and VCN Resolver also enables reverse DNS lookup, which lets you determine the hostname corresponding to the private IP address.
	    * `CustomDnsServer`: Instances use a DNS server of your choice (three maximum).
	* `search_domain_names` - Used only when `type` is `SearchDomainNames`. A single search domain name according to [RFC 952](https://tools.ietf.org/html/rfc952) and [RFC 1123](https://tools.ietf.org/html/rfc1123). During a DNS query,
                              the OS will append this search domain name to the value being queried.
                              If you set [DhcpDnsOption](https://docs.us-phoenix-1.oraclecloud.com/api/#/en/iaas/20160918/DhcpDnsOption/) to `VcnLocalPlusInternet`,
                              and you assign a DNS label to the VCN during creation, the search domain name in the
                              VCN's default set of DHCP options is automatically set to the VCN domain (for example, `vcn1.oraclevcn.com`).
                              If you don't want to use a search domain name, omit this option from the set of DHCP options. Do not include this option with an empty list
                              of search domain names, or with an empty string as the value for any search domain name.
* `state` - The current state of the set of DHCP options.
* `time_created` - Date and time the set of DHCP options was created, in the format defined by RFC3339.  Example: `2016-08-25T21:10:29.600Z` 
* `vcn_id` - The OCID of the VCN the set of DHCP options belongs to.

