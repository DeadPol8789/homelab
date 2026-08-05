# Personal HomeLab

> **Status:** Work in progress — physical assembly and initial virtualization setup.

This repository documents the design, deployment, and evolution of my personal HomeLab. The project is being built to develop practical skills in virtualization, Linux systems administration, networking, cybersecurity, monitoring, automation, and self-hosted services.

The documentation reflects only work that has actually been completed. Planned components and services are clearly marked and are not presented as deployed.

## Current Progress

| Area | Status | Verified progress |
| --- | --- | --- |
| Physical rack | Assembled | The rack and its current hardware have been physically installed. Final cabling is still in progress. |
| Proxmox host | Installed | Proxmox VE is installed on the main mini PC and access to its web interface has been verified. |
| Installation media | Available | An operating system ISO has been uploaded to Proxmox storage. |
| Virtual machines | Not deployed | Initial VM creation was started, but no complete VM has been created and booted yet. |
| Firewall appliance | Pending migration | The dedicated appliance was received with pfSense preinstalled. OPNsense has not yet been installed or configured. |
| Managed switch | Pending setup | The switch is available, but cabling and configuration have not yet been completed. |
| Production network path | Not deployed | The planned firewall-to-switch network path is not currently operating as the main home network. |
| Self-hosted services | Planned | Docker, Home Assistant, monitoring, automation, and AI services have not yet been deployed. |

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

## Target Architecture

The intended high-level network path is:

```text
ISP equipment
    |
OPNsense firewall
    |
Managed switch
    |
Proxmox host and network devices
```

This diagram represents the target design. It does not imply that the complete network path is currently deployed.

## Project Roadmap

- [x] Assemble the physical rack
- [x] Install Proxmox VE
- [x] Verify access to the Proxmox web interface
- [x] Upload installation media to Proxmox
- [ ] Complete and document the physical cabling
- [ ] Install OPNsense on the dedicated firewall appliance
- [ ] Configure the initial WAN and LAN interfaces safely
- [ ] Connect and configure the managed switch
- [ ] Verify the new network path before making it the primary network
- [ ] Create and document the first Linux virtual machine
- [ ] Deploy container-based services
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
| [Physical setup](docs/physical-setup.md) | Rack assembly status, pending cabling work, and photo-review guidance. |
| [Proxmox installation](docs/proxmox-installation.md) | Verified Proxmox VE installation progress and current limitations. |
| [Network design](docs/network-design.md) | Planned firewall-to-switch topology and validation criteria. |
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

- OPNsense installation and initial configuration
- Managed-switch deployment
- The first complete Linux virtual machine
- Network segmentation and secure remote access
- Container-hosted services
- Monitoring and automation services
- Sanitized troubleshooting notes and lessons learned

## Disclaimer

This is a personal learning environment and an evolving project. The documentation is provided for educational and portfolio purposes and will change as the infrastructure develops.
