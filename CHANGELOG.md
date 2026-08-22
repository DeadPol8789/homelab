# Changelog

This file records notable, verified changes to the HomeLab and its public documentation.

The project follows a simple evidence-based rule: an infrastructure milestone is recorded as completed only after it has been implemented, tested, and documented. Dates in this file refer to documentation releases, not necessarily to the original hardware installation date.

## [Unreleased]

### Added

- Added a sanitized OPNsense deployment record covering installation, base network roles, validation, security controls, private backup handling, and remaining work.
- Added a sanitized managed-switch deployment record covering traffic forwarding, local administration, stable private management, firmware compatibility review, validation, and remaining work.
- Added the planned on-demand GPU-compute role and Wake-on-LAN concept to the target architecture.

### Changed

- Updated the README to show the operational segmented OPNsense and managed-switch foundation.
- Updated the architecture from future segmentation to a verified three-VLAN network path.
- Updated the hardware inventory with the verified OPNsense and managed-switch versions and segmented roles.
- Updated the network design with the completed VLAN deployment, Proxmox migration, connectivity tests, and remaining policy work.
- Updated the OPNsense deployment record with version `26.7.2_2`, VLAN gateway operation, post-change validation, and private backups.
- Updated the managed-switch deployment record with firmware `3.30.6`, three verified VLANs, and a final private configuration copy.
- Updated the physical setup to record the segmented network path while retaining final cable organization as in progress.
- Updated the Proxmox record with its verified migration to the segmented management path.
- Updated the roadmap to mark the network-foundation phase as completed and reorder recovery, policy, and virtualization work.

### Verified infrastructure progress

- OPNsense has been installed on the dedicated firewall appliance and boots from internal storage.
- The initial upstream and LAN roles have been validated.
- Kea DHCPv4 is active for the HomeLab LAN.
- Client addressing, DNS resolution, internet connectivity, and local OPNsense administration have been tested.
- The managed switch is forwarding traffic to selected wired devices.
- Local managed-switch administration has been verified through a stable private management configuration.
- Managed-switch firmware compatibility has been reviewed.
- OPNsense has been updated to `26.7.2_2` and verified after restart and network changes.
- The managed switch has been updated to firmware `3.30.6`.
- Three role-based VLANs have been deployed and verified without publishing their live identifiers.
- The Proxmox host has been migrated to its segmented management path and remains reachable.
- Internet access and DNS resolution remain operational after the update and segmentation cycle.
- Final private network-configuration copies have been saved and checked outside the repository.
- The project roadmap's network-foundation phase now meets its completion criteria.
- Proxmox has been updated and normal administration uses a separate account protected by multi-factor authentication.
- Multi-factor authentication protects OPNsense administration.
- An initial OPNsense configuration backup has been exported and kept outside the public repository.

### Still in progress or planned

- Confirming required DHCP reservations privately.
- Performing controlled network-configuration restoration tests.
- Reviewing and refining inter-VLAN policy using least-privilege principles.
- Completing cable organization, safe labeling, power-load documentation, and recovery planning.
- Creating and validating the first Proxmox virtual machine and backup.
- VPN access, advanced firewall policy, monitoring, and automated backup rotation.
- Container-hosted services, Home Assistant, n8n, monitoring, and Hermes Agent.
- Wake-on-LAN and controlled use of the GPU workstation for approved heavy tasks.

## [0.1.0] - 2026-08-05

### Added

- Published the initial work-in-progress project overview.
- Added a sanitized hardware inventory.
- Added separate current-state and target-architecture documentation.
- Added physical setup notes and a photo-review checklist.
- Added the initial verified Proxmox VE installation record.
- Added the original planned network design for the dedicated firewall and managed switch.
- Added the project roadmap with completion criteria for each phase.
- Added public security, privacy, and vulnerability-reporting guidance.
- Added repository exclusions for common secrets, local data, logs, backups, and temporary files.
- Added an MIT license for the public project.

### Verified baseline

- The physical rack had been assembled.
- Proxmox VE had been installed on the virtualization host.
- Access to the Proxmox web interface had been verified.
- An operating system ISO had been uploaded to Proxmox storage.

## Changelog rules

Future entries should describe:

- What changed
- What was tested
- Which documentation was updated
- Any sanitized troubleshooting or lesson learned
- Whether rollback, backup, or recovery procedures were reviewed

Sensitive values, live network identifiers, credentials, internal names, and unredacted configuration exports must never be included in this file.
