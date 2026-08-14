# Hardware Inventory

> **Last verified:** August 2026  
> **Project status:** Work in progress

This document lists the hardware that is relevant to the HomeLab project. It distinguishes between equipment that is already in use, equipment that is available but still awaiting deployment, and hardware that is only being considered for a future phase.

The inventory is intentionally limited to information that is useful for a technical portfolio. Serial numbers, MAC addresses, public or private IP addresses, internal hostnames, device labels, account information, and exact physical locations are excluded.

## Status Definitions

| Status | Meaning |
| --- | --- |
| In use | The device is currently performing its documented role. |
| Partially deployed | The device is performing a verified base function, but its intended managed configuration is not complete. |
| Assembled | The hardware has been physically placed or assembled, but final cabling or configuration may still be in progress. |
| Available | The device is owned and ready for a future deployment step, but is not yet operating in its intended HomeLab role. |
| Planned | The item is not currently part of the deployed environment. It may be purchased or integrated later. |

## Compute and Virtualization

| Hardware | Key specifications | Intended role | Current status |
| --- | --- | --- | --- |
| GMKtec NucBox M6 Ultra | AMD Ryzen 5 7640HS, 32 GB RAM, 1 TB NVMe SSD | Primary Proxmox VE virtualization host | **In use:** Proxmox VE is installed, updated, accessible through the HomeLab LAN, and protected with a separate administrative account and multi-factor authentication. No complete virtual machine has been deployed yet. |
| Desktop workstation | NVIDIA GeForce RTX 5070 Ti, 32 GB RAM | Primary personal workstation and future on-demand compute node for heavy local-AI workloads | **In use independently:** it is not dedicated to the HomeLab and is not yet integrated with Hermes or automation. Future Wake-on-LAN and workload controls are planned. |

## Network and Security

| Hardware | Key specifications | Intended role | Current status |
| --- | --- | --- | --- |
| Dedicated fanless firewall appliance | Intel N100, 8 GB RAM, 128 GB NVMe SSD, 4 × Intel i226-V 2.5 GbE interfaces | Dedicated OPNsense firewall and router | **In use:** OPNsense is installed and the initial upstream, LAN, DHCP, DNS, internet-connectivity, local-administration, and multi-factor-authentication checks have been completed. |
| TP-Link JetStream TL-SG2008P V3 | 8-port managed switch with PoE support | Main managed switch for wired devices and future network segmentation | **Partially deployed:** connected and forwarding traffic for selected HomeLab devices. Administrative access, firmware review, management settings, and VLAN configuration remain pending. |
| 24-port Cat6 patch panel | 1U rack-mount patch panel | Structured Ethernet termination and cable organization | **Assembled:** part of the current rack build; final cabling is still in progress. |
| Ethernet cabling | Long-run and short patch cables | Connections between network equipment and client devices | **In use:** the base firewall-to-switch and selected client connections are operational; final routing, labeling, and organization remain in progress. |

The base path from the ISP equipment through OPNsense and the switch to selected wired clients is operational. Network segmentation, VLANs, VPN access, and advanced firewall policy will only be documented as deployed after they have been configured and verified.

## Rack, Power, and Local Administration

| Hardware | Key specifications | Intended role | Current status |
| --- | --- | --- | --- |
| VEVOR open-frame rack | 12U | Central physical structure for HomeLab equipment | **Assembled:** the rack is built and equipment placement has started. It remains open while network cabling is completed. |
| DIGITUS DN-95401 power distribution unit | 1U, 8 Schuko outlets | Rack power distribution | **Assembled:** included in the current rack build; final cable organization is in progress. |
| CyberPower UT850EG UPS | 850 VA / 425 W | Basic power protection for selected HomeLab and network equipment | **Available:** part of the current HomeLab power-protection setup. Runtime and load measurements have not yet been formally documented. |
| Adjustable rack shelf | 1U | Support for non-rack-mount equipment | **Assembled:** included in the current physical build. |
| Rack cable-management accessories | 1U cable manager and 1U brush panel | Cable routing and strain reduction | **Assembled:** final cable routing is still in progress. |
| MSI PRO MP165 E6 portable display | 15.6-inch display | Local console display for administration and diagnostics | **Available:** intended for local rack administration. |
| UGREEN HDMI KVM switch | Two computers to one HDMI console | Shared local display and USB control between systems | **Available:** intended for local maintenance of the Proxmox host and firewall appliance. |
| Royal Kludge RK61 keyboard | Compact wireless keyboard | Local rack-console input | **Available:** reserved for HomeLab administration. |

## Automation, Voice, and Physical Monitoring

| Hardware | Quantity | Intended role | Current status |
| --- | ---: | --- | --- |
| Home Assistant Voice Preview Edition | 2 | Future local voice interfaces for Home Assistant and the planned assistant platform | **Available:** not yet integrated or configured. |
| SONOFF CAM Pan-Tilt 2 (CAM-PT2) | 1 | Indoor physical monitoring of the HomeLab area | **In use independently:** HomeLab or Home Assistant integration has not yet been verified. No camera feeds, credentials, or access details will be published. |

## Client and Supporting Devices

The HomeLab will eventually serve several wired and wireless client devices. These endpoints are described only by role because their full personal inventory is not relevant to the infrastructure repository.

| Device category | Intended relationship to the HomeLab | Current status |
| --- | --- | --- |
| Main desktop workstation | Administration, development, testing, and future on-demand GPU workloads | Connected as a client; automated heavy-compute integration is planned but not deployed. |
| Laptops | Administration and client testing | At least one wired client has been used to validate connectivity through OPNsense and the switch. |
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
