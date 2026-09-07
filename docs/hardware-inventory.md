# Hardware Inventory

> **Last verified:** September 2026  
> **Project status:** Work in progress

This document lists the hardware that is relevant to the HomeLab project. It distinguishes between equipment that is already in use, equipment that is available but still awaiting deployment, and hardware that is only being considered for a future phase.

The inventory is intentionally limited to information that is useful for a technical portfolio. Serial numbers, MAC addresses, public or private IP addresses, internal hostnames, device labels, account information, and exact physical locations are excluded.

## Status Definitions

| Status | Meaning |
| --- | --- |
| In use | The device is currently performing its documented role. |
| Partially deployed | The device is performing a verified base function, but its intended managed configuration is not complete. |
| Configuration in progress | Setup has started, but the intended function has not yet been fully validated. |
| Assembled | The hardware has been physically placed or assembled, but final cabling or configuration may still be in progress. |
| Available | The device is owned and ready for a future deployment step, but is not yet operating in its intended HomeLab role. |
| Planned | The item is not currently part of the deployed environment. It may be purchased or integrated later. |

## Compute and Virtualization

| Hardware | Key specifications | Intended role | Current status |
| --- | --- | --- | --- |
| GMKtec NucBox M6 Ultra | AMD Ryzen 5 7640HS, 32 GB RAM, 1 TB NVMe SSD | Primary Proxmox VE virtualization host | **In use:** Proxmox VE `9.2.11` is installed, updated, accessible from an approved client segment, and protected with a separate administrative account and multi-factor authentication. It hosts the Ubuntu guest with Docker and Hermes, a separate Home Assistant VM, and container workloads for Tailscale and Uptime Kuma. |
| Desktop workstation | NVIDIA GeForce RTX 5070 Ti, 32 GB RAM | Primary personal workstation and future on-demand compute node for heavy local-AI workloads | **In use independently:** it is not dedicated to the HomeLab and is not yet integrated with Hermes or automation. Future Wake-on-LAN and workload controls are planned. |

### Current Virtual Workloads

These are workloads on the existing virtualization host, not additional physical computers. Live guest identifiers, hostnames, and network assignments are omitted.

| Workload | Placement | Current state |
| --- | --- | --- |
| Hermes Agent and Docker platform | Ubuntu Server VM | Operational text workflow with hardened remote administration, cross-session memory loading, approval-gated writes, and an initial Home Assistant voice request/response path verified. |
| Home Assistant | Separate VM | Operational with private name resolution and connected mobile companion apps. One voice unit completed onboarding and one request/response cycle to Hermes succeeded; broader reliability and device coverage remain unfinished. |
| Uptime Kuma | Separate container | Operational with initial alerting configured. The Home Assistant monitor was saved and reported **Up**. |
| Tailscale | Separate container in the workload inventory | Present as a remote-access workload. Private access to the Hermes host is externally tested; subnet routing, Exit Node operation, and network-wide access are not established by this inventory. |

Initial encrypted VM and container backups and a later manual VM backup passed checksum comparison after transfer to separate storage. A newer encrypted VM-level Home Assistant recovery copy was exported to secondary storage, but its own source-to-copy integrity result is not established. These records cover different backup scopes; they do not establish tested restoration or backup coverage for every current workload.

## Network and Security

| Hardware | Key specifications | Intended role | Current status |
| --- | --- | --- | --- |
| Dedicated fanless firewall appliance | Intel N100, 8 GB RAM, 128 GB NVMe SSD, 4 × Intel i226-V 2.5 GbE interfaces | Dedicated OPNsense firewall, router, and VLAN gateway | **In use:** OPNsense `26.7.2_2` is installed, and routing, DHCP, DNS, internet connectivity, local administration, multi-factor authentication, segmented access, and initial cross-segment policy enforcement have been verified. |
| TP-Link JetStream TL-SG2008P V3 | 8-port managed switch with PoE support | Main managed switch for wired distribution and role-based segmentation | **In use:** firmware `3.30.6` is installed; local administration, stable private management, traffic forwarding, and three role-based VLANs have been verified. |
| 24-port Cat6 patch panel | 1U rack-mount patch panel | Structured Ethernet termination and cable organization | **In use:** installed as part of the completed physical cabling and organization foundation. |
| Ethernet cabling | Long-run and short patch cables | Connections between network equipment and client devices | **In use:** required connections, final routing, private labeling, and organization have been completed and verified. |

The segmented path from the ISP equipment through OPNsense and the switch to selected wired clients is operational. Three role-based VLANs, approved Proxmox reachability, internet access, segment-specific DNS access, and selected isolation paths have been verified. Private name resolution is operational for the assistant guest and Home Assistant, and final network-configuration backups are stored privately. Tailscale access to the Hermes host has been externally tested, including from the selected travel laptop through a mobile hotspot. Wider client validation, network-wide remote administration, and comprehensive firewall-policy review remain in progress or pending.

## Rack, Power, and Local Administration

| Hardware | Key specifications | Intended role | Current status |
| --- | --- | --- | --- |
| VEVOR open-frame rack | 12U | Central physical structure for HomeLab equipment | **In use:** the rack, equipment placement, cabling, organization, and ventilation checks have been completed. |
| DIGITUS DN-95401 power distribution unit | 1U, 8 Schuko outlets | Rack power distribution | **In use:** installed and reviewed as part of the completed rack power-distribution foundation. |
| CyberPower UT850EG UPS | 850 VA / 425 W | Basic power protection for selected HomeLab and network equipment | **In use:** connected to the selected HomeLab equipment; power distribution and the connected load have been reviewed. |
| Adjustable rack shelf | 1U | Support for non-rack-mount equipment | **Assembled:** included in the current physical build. |
| Rack cable-management accessories | 1U cable manager and 1U brush panel | Cable routing and strain reduction | **In use:** final routing, organization, and strain-relief checks have been completed. |
| MSI PRO MP165 E6 portable display | 15.6-inch display | Local console display for administration and diagnostics | **Available:** intended for local rack administration. |
| UGREEN HDMI KVM switch | Two computers to one HDMI console | Shared local display and USB control between systems | **Available:** intended for local maintenance of the Proxmox host and firewall appliance. |
| Royal Kludge RK61 keyboard | Compact wireless keyboard | Local rack-console input | **Available:** reserved for HomeLab administration. |

## Automation, Voice, and Physical Monitoring

| Hardware | Quantity | Intended role | Current status |
| --- | ---: | --- | --- |
| Home Assistant Voice Preview Edition | 2 | Local voice interfaces for Home Assistant and approved Hermes interaction | **Initial path verified on one unit:** onboarding completed and one request returned the expected assistant response through Home Assistant and Hermes. Repeated reliability, latency, the second unit, and any device-control permissions still require validation. |
| SONOFF CAM Pan-Tilt 2 (CAM-PT2) | 1 | Indoor physical monitoring of the HomeLab area | **In use independently:** HomeLab or Home Assistant integration has not yet been verified. No camera feeds, credentials, or access details will be published. |

## Client and Supporting Devices

The HomeLab serves selected wired and wireless clients, with further client validation in progress. These endpoints are described only by role because their full personal inventory is not relevant to the infrastructure repository.

| Device category | Intended relationship to the HomeLab | Current status |
| --- | --- | --- |
| Main desktop workstation | Administration, development, testing, and future on-demand GPU workloads | Connected as a client; automated heavy-compute integration is planned but not deployed. |
| Laptops | Administration and client testing | A wired client has validated connectivity through OPNsense and the switch. The selected travel laptop has also passed a Tailscale access test to the Hermes host through an external mobile hotspot. |
| Mobile phone and tablet clients | Home Assistant companion apps and selected remote-access clients | Home Assistant companion apps are connected on selected devices. Completion of the wider remote-client rollout is tracked separately from local app connectivity. |
| Secondary backup storage | Hold backup copies away from the primary virtualization host | **In use:** earlier encrypted VM and container backups passed checksum comparison. Secondary storage also holds an encrypted VM-level Home Assistant recovery copy; its source-to-copy integrity and restoration are not established here. Exact hardware, capacity, connection, and location remain private. |
| Smart-home and camera devices | Future isolated or controlled network clients | Deployment and integration will be documented individually after verification. |

## Planned Hardware

The following items are possible future additions and are **not** part of the deployed HomeLab:

- A dedicated NAS and suitable NAS-grade storage drives
- Additional backup storage
- A second UPS for the main workstation
- Additional security cameras compatible with local or standards-based integration
- Additional compute capacity if future services exceed the available resources

No purchase is considered completed until the device is physically received and verified.

## Publication and Update Rules

This inventory will be updated using the following rules:

1. A device moves from **Planned** to **Available** only after it has been physically received.
2. A device moves to **Assembled** only after its physical placement has been confirmed.
3. A device moves to **In use** only after its intended function has been tested successfully.
4. Installed software does not imply that the complete service or network path is operational.
5. Sensitive identifiers and access details must be removed before every public update.

These distinctions keep the repository accurate and prevent planned work from being presented as completed experience.
