# Changelog

All notable changes to this project will be documented in this file.

## [1.3.2] - 2025-06-11

### Collection

- Changed repository URL to use GitHub Organization.
- Corrected missing or extra dependencies.

## [1.3.1] - 2025-02-24

### Role - deploy_vm

- Fixed bug with standard port group validation.

## [1.3.0] - 2025-02-24

### Role - deploy_vm

- Allowed for folder to be added to template.

## [1.2.1] - 2025-01-08

### Collection

- Added Changelog.
- Updated collection README documentation.

## [1.2.0] - 2024-09-21

### Role - deploy_vm

- Added the `vmware_mac_address` variable to supply a static MAC address.  If it is not supplied, the MAC address will be dynamic and assigned randomly.

## [1.1.2] - 2024-09-19

### Role - deploy_vm

- Added missing Windows domain admin credentials for customization.

## [1.1.1] - 2024-09-16

### Role - deploy_vm

- The `vmware_hostname`, `vmware_username`, `vmware_password`, and `vmware_validate_certs` variables are now optional to allow for them to be assigned in other ways.

## [1.1.0] - 2024-09-11

### Role - deploy_vm

- Added registration of the result of VM deployment.

## [1.0.0] - 2024-09-10

### Collection

- Initial release.
- *vmware_guest* module plugin added.
- *deploy_vm* role added.
