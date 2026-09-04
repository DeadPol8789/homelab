# Changelog

This file records notable, verified changes to the HomeLab and its public documentation.

The project follows a simple evidence-based rule: an infrastructure milestone is recorded as completed only after it has been implemented, tested, and documented. Dates in this file refer to documentation releases, not necessarily to the original hardware installation date.

## [Unreleased]

### Added

- Added a sanitized OPNsense deployment record covering installation, base network roles, validation, security controls, private backup handling, and remaining work.
- Added a sanitized managed-switch deployment record covering traffic forwarding, local administration, stable private management, firmware compatibility review, validation, and remaining work.
- Added a sanitized Hermes Agent deployment record covering the first Linux guest, hardened administration, Docker validation, the initial text workflow, persistent memory, and remaining work.
- Added a sanitized backup-and-recovery record covering workload scope, encryption, secondary copies, integrity validation, and the controlled-restoration boundary.
- Added a sanitized Tailscale remote-access record covering the initial host-and-client scope, external validation, security boundary, and remaining rollout work.
- Added the planned on-demand GPU-compute role and Wake-on-LAN concept to the target architecture.

### Changed

- Updated the README to show the operational segmented foundation, first validated Linux guest, Docker platform, and Hermes Agent deployment.
- Updated the architecture with the operational Proxmox-to-Linux-to-Hermes workload path while preserving planned services separately.
- Updated the hardware inventory with Proxmox VE `9.2.11` and the first operational guest and assistant workload.
- Updated the network design with the operational private DNS and approved service path for the first Linux and Hermes workload.
- Updated the OPNsense deployment record with the verified DNS and network path used by the first service workload.
- Updated the managed-switch deployment record with firmware `3.30.6`, three verified VLANs, and a final private configuration copy.
- Updated the physical setup to record the completed rack, cabling, private labeling, ventilation, strain-relief, and power-distribution foundation.
- Updated the Proxmox record with version `9.2.11`, the first Ubuntu Server guest, SSH hardening, Docker validation, and Hermes Agent deployment.
- Updated the roadmap to complete the virtualization-foundation phase and move the core-service and assistant phases to in progress.
- Corrected the security-and-privacy boundary so it accurately presents the first guest, Docker, and Hermes as operational.
- Expanded the public-sanitization rules for assistant memory, profiles, prompts, session data, configuration, tool output, and backups.
- Updated the README, architecture, hardware inventory, Proxmox record, Hermes deployment, roadmap, and security policy with the verified initial workload-backup milestone.
- Expanded the public-sanitization rules for backup identifiers, filenames, paths, timestamps, sizes, checksums, encryption metadata, and storage destinations.
- Updated the README, architecture, network design, OPNsense record, Hermes deployment, roadmap, and security policy with the tested private host-access milestone.
- Expanded the public-sanitization rules for Tailscale addresses, tailnet and device identifiers, account data, authentication material, and live access-policy configuration.
- Updated the README, architecture, backup-and-recovery record, Proxmox record, Hermes deployment, and roadmap with the verified follow-up virtual-machine backup cycle.

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
- Proxmox has been updated to `9.2.11`, and normal administration uses a separate account protected by multi-factor authentication.
- Multi-factor authentication protects OPNsense administration.
- An initial OPNsense configuration backup has been exported and kept outside the public repository.
- Required DNS access has been verified for selected network roles.
- Proxmox administration has been verified from an approved client segment.
- A selected management-to-service path has been blocked and tested.
- Private name resolution is operational and verified for the first service workload.
- The physical foundation is complete, including equipment placement, cable organization, private labeling, ventilation and stability checks, power distribution, and connected-load review.
- The project roadmap's physical-foundation phase now meets its completion criteria.
- The first Ubuntu Server `24.04.4 LTS` VM has been installed, updated, restarted, and validated through its approved segmented path.
- The guest uses a dedicated non-root account and encrypted key for remote administration; password-based SSH authentication and direct root login are disabled.
- Docker Engine `29.7.2`, Docker Compose `5.5.0`, the Docker service, container runtime, and a disposable test container have been validated.
- Hermes Agent is operational through its initial text workflow.
- Hermes persistent user-memory loading has been verified in a new session.
- The project roadmap's virtualization-foundation phase now meets its completion criteria.
- Initial compressed backups of the current virtual machine and container workloads have been created.
- Encrypted copies of both workload backups have been stored separately from the primary virtualization host.
- Matching SHA-256 checksums have verified the integrity of the encrypted source and secondary copies.
- The manual virtual-machine backup workflow was repeated after further configuration changes.
- The follow-up virtual-machine archive was encrypted, copied away from the virtualization host, and verified against its encrypted source with matching SHA-256 results.
- The follow-up integrity check is recorded separately from the still-pending decryption and controlled-restoration tests.
- Tailscale is operational on the Hermes host and one approved client.
- Key-based SSH through Tailscale has been verified from outside the home network.
- The tested remote path requires no direct public inbound service or router port forwarding.

### Still in progress or planned

- Confirming required DHCP reservations privately.
- Performing controlled network-configuration restoration tests.
- Completing the inter-VLAN policy review using least-privilege principles.
- Measuring UPS battery runtime and defining controlled shutdown behavior as separate resilience work.
- Finalizing cleanup or retention handling for unencrypted local working archives.
- Defining recurring guest, container, Hermes configuration, and persistent-memory backups.
- Adding retention, capacity, and backup-failure monitoring.
- Performing controlled guest, service, and network-configuration restoration tests.
- Enrolling and externally testing the selected travel and backup clients.
- Reviewing Tailscale access policy, device lifecycle, authorization, and recovery procedures.
- Deciding whether subnet routing or Exit Node operation is required before deploying either capability.
- Defining restricted access for any future additional users without exposing infrastructure administration.
- Network-wide remote administration, advanced firewall policy, monitoring, and automated backup rotation.
- Expanded memory/RAG, isolated user profiles, a remote Hermes conversation interface, Home Assistant, voice integration, and n8n.
- Additional container-hosted services and assistant integrations.
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
