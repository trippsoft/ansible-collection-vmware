# Ansible Collection: trippsc2.vmware

This collection contains roles and modules for managing VMware infrastructure.

## Content

### Module plugins

- vmware_guest - Manages virtual machines in vCenter (used because of MAC address bug in *community.vmware.vmware_guest*)

### Roles

- [deploy_vm](roles/deploy_vm/README.md) - This role deploys and customizes a new VMware VM from a template.
