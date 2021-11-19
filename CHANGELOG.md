# Changelog

All notable changes to this repository will be documented in this file.

The format of this Changelog is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/). This changelog and project repository adhere to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

> Don’t let your friends dump git logs into changelogs.

## [0.0.1] - 2020-05-08
### Added
- Initial repository framework and documentation.

## [1.0.0] - 2020-05-11 - RELEASE
### Added
- Initial version of YAML plays for SAS administration.
- Initial version of YAML play to execute SAS using Ansible.

## [1.1.0] - 2020-05-12
### Added
- Initial version of YAML plays for AWS administration (more to come).
- admin/purge_sasdata_controller.yml

### Changed
- Minor updates to insert_hostname_etc_hosts.yml, upgrade_all_packages_yum.yml and mount_sasdata_controller.yml

## [1.1.1] - 2020-05-15
### Added
- Initial version of validate_environment.yml within **validation** component.
- aws/destroy_environment.yml to destory an entire environment (if tagged appropriately).

### Changed
- Update all boolean values to "yes" and "no" instead of "true" and "false" for consistency.
