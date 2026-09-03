# Personal HomeLab

> **Status:** Work in progress — operational segmented-network foundation, first assistant workload, verified backups, and tested private remote access.

This repository documents the design, deployment, and evolution of my personal HomeLab. The project is being built to develop practical skills in virtualization, Linux systems administration, networking, cybersecurity, monitoring, automation, and self-hosted services.

The documentation reflects only work that has actually been completed. Planned components and services are clearly marked and are not presented as deployed.

## Current Progress

| Area | Status | Verified progress |
| --- | --- | --- |
| Physical rack | Completed | The rack, equipment placement, physical cabling, cable organization, private labeling, ventilation checks, and power-distribution review have been completed. |
| Proxmox host | Operational | Proxmox VE `9.2.11` is installed, updated, reachable through its segmented management path, and protected with a separate administrative account and multi-factor authentication. |
| Installation media | Available | An operating system ISO has been uploaded to Proxmox storage. |
| Virtual machines | First guest operational | The first Linux server VM is installed, updated, reachable through its approved segmented path, and hardened for key-based remote administration. |
| Firewall appliance | Operational with initial policy enforcement | OPNsense `26.7.2_2` is installed on the dedicated appliance. Routing, DHCP, DNS, internet connectivity, local administration, segmented network access, and initial cross-segment policy controls have been verified. |
| Managed switch | Operational segmented foundation | The switch is running firmware `3.30.6`, its private administration path is operational, and three role-based VLANs are active and verified. |
| HomeLab network path | Operational, segmented, and policy-tested | The path from the ISP equipment through OPNsense and the managed switch has been tested successfully. Approved management access, segment-specific DNS access, and isolation between selected network roles have also been verified. |
| Self-hosted services | Initial platform operational | Docker Engine `29.7.2`, Docker Compose `5.5.0`, and Hermes Agent are deployed on the first Linux guest. Hermes persistent memory loading has been verified across sessions. |
| Backup and recovery | Initial backups verified | Encrypted backups of the current virtual machine and container workloads have been copied to separate storage and verified with matching SHA-256 checksums. Controlled restoration and automated rotation remain pending. |
| Remote access | Initial path operational | Tailscale provides private remote access to the Hermes host from an approved client. Key-based SSH access has been verified from outside the home network without exposing a public inbound service. |

## Hardware Overview

The current build includes:

- A 12U open-frame rack
- A GMKtec NucBox M6 Ultra used as the Proxmox host
- A dedicated Intel N100 firewall appliance with four 2.5 GbE interfaces
- A TP-Link JetStream TL-SG2008P managed PoE switch
- A patch panel, rack power distribution, cable management, and rack accessories
- A UPS for basic power protection
- A compact rack display and KVM peripherals for local administration

Model names are included only where they are useful for technical context. Serial numbers, MAC addresses, public IP addresses, internal hostnames, credentials, and other sensitive identifiers are intentionally excluded.

## Current Network Architecture

The verified high-level network path is:

```text
ISP equipment
    |
OPNsense firewall
    |
VLAN-aware managed switch
    |
Three role-based network segments
    |
Proxmox host and selected devices
```

This segmented path is operational for selected wired devices, and the switch can be administered through a stable private management configuration. The Proxmox host remains reachable from an approved client segment after its network migration. Initial DNS-access and cross-segment isolation rules have been tested, and the first Linux guest is operating through its approved service path with private name resolution. Tailscale now provides a tested private path to the Hermes host from an approved external client; broader remote administration remains limited and under review.

## Project Roadmap

- [x] Assemble the physical rack
- [x] Install Proxmox VE
- [x] Verify access to the Proxmox web interface
- [x] Upload installation media to Proxmox
- [x] Update and harden the initial Proxmox administration setup
- [x] Install OPNsense on the dedicated firewall appliance
- [x] Configure and validate the initial WAN and LAN roles
- [x] Enable and validate the initial DHCP service
- [x] Connect OPNsense, the managed switch, and selected wired devices
- [x] Verify internet and DNS connectivity through the new HomeLab path
- [x] Configure and validate the managed-switch administration path
- [x] Review the switch firmware and hardware-revision compatibility
- [x] Update OPNsense and the managed-switch firmware
- [x] Design, deploy, and validate three role-based VLANs
- [x] Migrate and verify the Proxmox management path within the segmented network
- [x] Save and verify final private network-configuration backups
- [x] Apply and verify initial DNS-access rules for approved network roles
- [x] Verify isolation between the management and server-oriented segments
- [x] Prepare private name resolution for the first service workload
- [x] Complete and document the physical cabling
- [x] Update Proxmox VE and preserve a private pre-update configuration copy
- [x] Complete, update, and harden the first Linux virtual machine
- [x] Install and validate Docker Engine and Docker Compose
- [x] Deploy Hermes Agent and verify persistent memory loading across sessions
- [x] Create encrypted initial backups of the current VM and container workloads
- [x] Copy the protected backups to separate storage and verify matching SHA-256 checksums
- [x] Deploy Tailscale for private remote access to the Hermes host
- [x] Verify key-based SSH access from outside the home network
- [ ] Add and test the travel laptop and selected backup client devices
- [ ] Review Tailscale access controls, device lifecycle, and recovery procedures
- [ ] Define recurring guest and service backup rotation
- [ ] Perform controlled guest and service restoration tests
- [ ] Deploy additional container-based services
- [ ] Add monitoring with Prometheus and Grafana
- [ ] Add Home Assistant and local automation services
- [ ] Evaluate and deploy the planned AI assistant services

The roadmap will be updated as each stage is completed and verified.

## Documentation Principles

This repository follows four rules:

1. Document completed work separately from future plans.
2. Explain the reasoning behind important infrastructure decisions.
3. Keep instructions reproducible without exposing the real environment.
4. Review every file and image for sensitive information before publication.

## Documentation

| Document | Purpose |
| --- | --- |
| [Hardware inventory](docs/hardware-inventory.md) | Sanitized inventory with clear implementation states. |
| [Architecture](docs/architecture.md) | Verified current state and separate target architecture. |
| [Physical setup](docs/physical-setup.md) | Completed rack and cabling foundation, maintenance principles, and photo-review guidance. |
| [Proxmox installation](docs/proxmox-installation.md) | Verified Proxmox VE installation progress and current limitations. |
| [Hermes Agent deployment](docs/hermes-agent-deployment.md) | Sanitized first-guest, container-platform, Hermes Agent, and persistent-memory deployment record. |
| [Backup and recovery](docs/backup-and-recovery.md) | Sanitized backup scope, encryption, integrity validation, and remaining restoration work. |
| [Tailscale remote access](docs/tailscale-remote-access.md) | Sanitized private-access design, external validation, security boundary, and remaining client rollout. |
| [OPNsense deployment](docs/opnsense-deployment.md) | Sanitized installation, initial network roles, security controls, and connectivity validation. |
| [Managed-switch deployment](docs/managed-switch-deployment.md) | Sanitized management setup, firmware state, VLAN deployment, validation, and recovery notes. |
| [Network design](docs/network-design.md) | Verified segmented topology and planned security improvements. |
| [Project roadmap](docs/project-roadmap.md) | Completed, in-progress, and planned phases with completion criteria. |
| [Security and privacy](docs/security-and-privacy.md) | Rules for sanitizing files, screenshots, logs, and configurations. |

Repository-level information:

- [Changelog](CHANGELOG.md) — verified project and documentation changes
- [Security policy](SECURITY.md) — responsible reporting guidance
- [MIT License](LICENSE) — reuse terms for code and documentation

## Security and Privacy

This public repository will never intentionally include:

- Passwords, API keys, tokens, recovery codes, or private keys
- Real `.env` files or unredacted configuration backups
- Public IP addresses, MAC addresses, serial numbers, or device labels
- Internal DNS names, Wi-Fi details, or remote-access endpoints
- Screenshots containing personal information or browser and account data
- Exact rules or details that would unnecessarily expose the live network

Examples and future configuration templates will use placeholders and documentation-only values.

## Future Documentation

Additional implementation notes will be added only after the corresponding work has been completed and verified. Planned topics include:

- Further segmentation-policy refinement and recovery testing
- Backup rotation and controlled restoration procedures
- Additional remote-access clients, policy refinement, and recovery testing
- Additional container-hosted services
- Monitoring and automation services
- Sanitized troubleshooting notes and lessons learned

## Disclaimer

This is a personal learning environment and an evolving project. The documentation is provided for educational and portfolio purposes and will change as the infrastructure develops.
