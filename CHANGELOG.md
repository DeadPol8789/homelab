# Changelog

This file records notable, verified changes to the HomeLab and its public documentation.

The project follows a simple evidence-based rule: an infrastructure milestone is recorded as completed only after it has been implemented, tested, and documented. Dates in this file refer to documentation releases, not necessarily to the original hardware installation date.

## [Unreleased]

### Documentation prepared

- Added the initial work-in-progress project overview.
- Added a sanitized hardware inventory.
- Added separate current-state and target-architecture documentation.
- Added physical setup notes and a photo-review checklist.
- Added the verified Proxmox VE installation record.
- Added the planned network design for the dedicated firewall and managed switch.
- Added the project roadmap with completion criteria for each phase.
- Added public security, privacy, and vulnerability-reporting guidance.
- Added repository exclusions for common secrets, local data, logs, backups, and temporary files.
- Added an MIT license for the public project.

### Verified infrastructure baseline

- The physical rack has been assembled.
- Proxmox VE has been installed on the virtualization host.
- Access to the Proxmox web interface has been verified.
- An operating system ISO has been uploaded to Proxmox storage.

### In progress

- Completing and validating the physical cabling.
- Preparing the dedicated firewall appliance for migration from its preinstalled pfSense system to OPNsense.
- Preparing the managed switch for its initial connection and configuration.
- Completing and validating the first Proxmox virtual machine.

### Not yet deployed

- OPNsense as the active HomeLab firewall.
- The managed switch in the active network path.
- VLANs, VPN access, or production network segmentation.
- Container-hosted services.
- Home Assistant and local voice integrations.
- Prometheus and Grafana monitoring.
- Hermes Agent or other persistent assistant services.

## Release process

When the repository is published for the first time, the verified entries under `Unreleased` may be moved to an initial version such as `0.1.0` and assigned the publication date.

Future entries should describe:

- What changed
- What was tested
- Which documentation was updated
- Any sanitized troubleshooting or lesson learned
- Whether rollback, backup, or recovery procedures were reviewed

Sensitive values, live network identifiers, credentials, internal names, and unredacted configuration exports must never be included in this file.
