<!-- BEGIN_ANSIBLE_DOCS -->

# Ansible Role: trippsc2.vmware.deploy_vm
Version: 1.3.1

This role deploys and customizes a new VMware VM from a template.

## Requirements


## Dependencies

| Collection |
| ---------- |
| community.vmware |

## Role Arguments
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| vmware_hostname | <p>The FQDN or IP address of the VMware infrastructure to which the VM will be deployed.</p> | str | no |  |  |
| vmware_username | <p>The username for authenticating with the VMware infrastructure.</p> | str | no |  |  |
| vmware_password | <p>The password for authenticating with the VMware infrastructure.</p> | str | no |  |  |
| vmware_validate_certs | <p>Whether to validate SSL certificates.</p> | bool | no |  |  |
| vmware_os_type | <p>The type of operating system installed on the VM to be deployed.</p><p>This value is used to determine which customization options are available.</p> | str | yes | <ul><li>linux</li><li>windows</li></ul> |  |
| vmware_template_folder | <p>The name of the folder in which the template exists to deploy the VM.</p> | str | no |  |  |
| vmware_template | <p>The name of the template from which to deploy the VM.</p> | str | yes |  |  |
| vmware_custom_values | <p>A list of custom values to configure on the VM.</p> | list of dicts of 'vmware_custom_values' options | no |  |  |
| vmware_name | <p>The name of the VM to be deployed.</p> | str | yes |  |  |
| vmware_datacenter | <p>The name of the datacenter in which to deploy the VM.</p> | str | yes |  |  |
| vmware_datacenter_folder | <p>The name of the folder in which the datacenter exists to deploy the VM.</p> | str | no |  |  |
| vmware_folder | <p>The name of the folder in which to deploy the VM.</p><p>If not provided, the VM is deployed in the root folder of the datacenter.</p> | str | no |  |  |
| vmware_cluster | <p>The name of the cluster in which to deploy the VM.</p><p>This is mutually exclusive with *vmware_host*.</p><p>If the cluster does not have DRS enabled, the *vmware_host* option must be used instead.</p> | str | no |  |  |
| vmware_host | <p>The name of the host on which to deploy the VM.</p><p>This is mutually exclusive with *vmware_cluster*.</p><p>If the host is part of a cluster with DRS enabled, the *vmware_cluster* option must be used instead.</p> | str | no |  |  |
| vmware_datastore | <p>The name of the datastore on which to deploy the VM files.</p> | str | yes |  |  |
| vmware_vm_hostname | <p>The hostname to configure on the VM.</p><p>If not provided and *vmware_os_type* is `linux`, the lowercase value of *vmware_name* is used.</p><p>If not provided and *vmware_os_type* is `windows`, the uppercase value of *vmware_name* is used.</p> | str | no |  |  |
| vmware_allow_long_hostnames | <p>Whether to allow long hostnames on the VM.</p><p>If this is set to `true`, the *vmware_vm_hostname* must be less than 16 characters.</p> | bool | no |  | False |
| vmware_dns_servers | <p>A list of DNS servers to configure on the VM.</p> | list of 'str' | no |  |  |
| vmware_dns_suffixes | <p>A list of DNS suffixes to configure on the VM.</p> | list of 'str' | no |  |  |
| vmware_domain | <p>The domain to which the VM belongs.</p><p>If *vmware_os_type* is `windows` and *vmware_join_domain* is `true`, the VM will be joined to this domain and this is required.</p> | str | no |  |  |
| vmware_full_name | <p>The full name of the user to configure on the Windows VM.</p><p>If *vmware_os_type* is `linux`, this is ignored.</p> | str | no |  |  |
| vmware_organization | <p>The organization to configure on the Windows VM.</p><p>If *vmware_os_type* is `linux`, this is ignored.</p> | str | no |  |  |
| vmware_product_id | <p>The product ID to configure on the Windows VM.</p><p>If *vmware_os_type* is `linux`, this is ignored.</p> | str | no |  |  |
| vmware_timezone | <p>The timezone to configure on the VM.</p><p>If *vmware_os_type* is `linux`, this should be in tz format (e.g. `America/New_York`).</p><p>If *vmware_os_type* is `windows`, this should be in Windows index format (e.g. **Eastern Standard Time** is `035`).</p><p>Linux Reference: https://en.wikipedia.org/wiki/List_of_tz_database_time_zones</p><p>Windows Reference: https://learn.microsoft.com/en-us/previous-versions/windows/embedded/ms912391(v=winembedded.11)</p> | str | no |  |  |
| vmware_autologon_count | <p>The number of times to enable autologon on the Windows VM.</p><p>If *vmware_os_type* is `linux`, this is ignored.</p> | int | no |  | 1 |
| vmware_administrator_password | <p>The password for the administrator account on the Windows VM.</p><p>If *vmware_os_type* is `windows`, this is required. Otherwise, it is ignored.</p> | str | no |  |  |
| vmware_join_domain | <p>Whether to join the Windows VM to a domain.</p><p>If *vmware_os_type* is `linux`, this is ignored.</p> | bool | no |  | False |
| vmware_domain_username | <p>The username for authenticating with the domain.</p><p>If *vmware_os_type* is `windows` and *vmware_join_domain* is `true`, this is required. Otherwise, it is ignored.</p> | str | no |  |  |
| vmware_domain_password | <p>The password for authenticating with the domain.</p><p>If *vmware_os_type* is `windows` and *vmware_join_domain* is `true`, this is required. Otherwise, it is ignored.</p> | str | no |  |  |
| vmware_workgroup | <p>The workgroup to which the Windows VM belongs.</p><p>If *vmware_os_type* is `linux` or *vmware_join_domain* is `true`, this is ignored.</p> | str | no |  | WORKGROUP |
| vmware_run_once_commands | <p>A list of commands to run on the Windows VM after deployment.</p><p>If *vmware_os_type* is `linux`, this is ignored.</p> | list of 'str' | no |  | [] |
| vmware_hw_clock_is_utc | <p>Whether the hardware clock on the VM is set to UTC.</p><p>If *vmware_os_type* is `windows`, this is ignored.</p> | bool | no |  |  |
| vmware_boot_firmware | <p>The boot firmware to configure on the VM.</p><p>If *vmware_secure_boot* is `true`, this must be set to `efi`.</p> | str | no | <ul><li>bios</li><li>efi</li></ul> | efi |
| vmware_secure_boot | <p>Whether to enable Secure Boot on the VM.</p><p>If this is set to `true`, *vmware_boot_firmware* must be set to `efi`.</p> | bool | no |  | True |
| vmware_nested_virtualization | <p>Whether to enable nested virtualization on the VM.</p><p>This may be required for running hypervisors within the VM or using certain security features like Windows Defender Application Guard.</p> | bool | no |  |  |
| vmware_virtualization_based_security | <p>Whether to enable virtualization-based security on the Windows VM.</p><p>This is required for using certain security features like Windows Defender Credential Guard.</p><p>This will fail if the version of Windows does not support virtualization-based security.</p><p>If *vmware_os_type* is `linux`, this is ignored.</p> | bool | no |  |  |
| vmware_cpus | <p>The number of CPUs to configure on the VM.</p> | int | no |  | 2 |
| vmware_ram_in_gb | <p>The amount of RAM in MB to configure on the VM.</p><p>If *vmware_os_type* is `linux`, this defaults to `2`.</p><p>If *vmware_os_type* is `windows`, this defaults to `4`.</p> | int | no |  |  |
| vmware_network_name | <p>The name of the network to which the VM will be connected.</p> | str | yes |  |  |
| vmware_dv_switch_name | <p>The name of the distributed virtual switch to which the VM will be connected.</p><p>If not provided, the VM is connected to a standard switch.</p> | str | no |  |  |
| vmware_network_type | <p>The type of network configuration to use on the VM.</p><p>If this is set to `static`, the *vmware_ip*, *vmware_netmask*, and *vmware_gateway* are required.</p> | str | no | <ul><li>dhcp</li><li>static</li></ul> | dhcp |
| vmware_ip | <p>The IP address to configure on the VM.</p><p>If *vmware_network_type* is `static`, this is required.</p> | str | no |  |  |
| vmware_netmask | <p>The netmask to configure on the VM.</p><p>If *vmware_network_type* is `static`, this is required.</p> | str | no |  |  |
| vmware_gateway | <p>The gateway to configure on the VM.</p><p>If *vmware_network_type* is `static`, this is required.</p> | str | no |  |  |
| vmware_network_device_type | <p>The type of network device to configure on the VM.</p><p>Unless you have a specific reason to change this, the default should be used.</p> | str | no | <ul><li>e1000</li><li>e1000e</li><li>vmxnet3</li></ul> | vmxnet3 |
| vmware_mac_address | <p>The MAC address to configure on the VM.</p><p>If not provided, a random MAC address is generated.</p> | str | no |  |  |

### Options for vmware_custom_values
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| key | <p>The key of the custom value to configure on the VM.</p> | str | yes |  |  |
| value | <p>The value of the custom value to configure on the VM.</p> | str | yes |  |  |


## License
MIT

## Author and Project Information
Jim Tarpley
<!-- END_ANSIBLE_DOCS -->
