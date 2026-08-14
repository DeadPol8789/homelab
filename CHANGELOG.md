# Changelog

This file records notable, verified changes to the HomeLab and its public documentation.

The project follows a simple evidence-based rule: an infrastructure milestone is recorded as completed only after it has been implemented, tested, and documented. Dates in this file refer to documentation releases, not necessarily to the original hardware installation date.

## [Unreleased]

### Added

- Added a sanitized OPNsense deployment record covering installation, base network roles, validation, security controls, private backup handling, and remaining work.
- Added the planned on-demand GPU-compute role and Wake-on-LAN concept to the target architecture.

### Changed

- Updated the README to show the operational OPNsense and firewall-to-switch path.
- Updated the architecture from a planned firewall migration to a verified base network with future segmentation.
- Updated the hardware inventory to distinguish the operational firewall, partially deployed switch, and on-demand GPU workstation role.
- Updated the network design with passed base-connectivity checks and remaining managed-network tasks.
- Updated the physical setup to record the operational base cabling while retaining final organization as in progress.
- Updated the Proxmox record with host updates, HomeLab network connectivity, separate administrative access, and multi-factor authentication.
- Updated the roadmap so that the network and security-resilience phases are marked as in progress.

### Verified infrastructure progress

- OPNsense has been installed on the dedicated firewall appliance and boots from internal storage.
- The initial upstream and LAN roles have been validated.
- Kea DHCPv4 is active for the HomeLab LAN.
- Client addressing, DNS resolution, internet connectivity, and local OPNsense administration have been tested.
- The managed switch is forwarding traffic to selected wired devices.
- The Proxmox host remains reachable through the OPNsense and switch path.
- Proxmox has been updated and normal administration uses a separate account protected by multi-factor authentication.
- Multi-factor authentication protects OPNsense administration.
- An initial OPNsense configuration backup has been exported and kept outside the public repository.

### Still in progress or planned

- Confirming required DHCP reservations privately.
- Discovering and securing managed-switch administration and reviewing its firmware.
- Completing cable organization, safe labeling, power-load documentation, and rollback planning.
- Creating and validating the first Proxmox virtual machine and backup.
- VLANs, VPN access, advanced firewall policy, and automated configuration backups.
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
