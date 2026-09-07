# HomeLab Architecture

> **Last verified:** September 2026  
> **Project status:** Work in progress

This document describes the HomeLab at two different levels:

1. The **current verified state**, which includes only components that are installed or confirmed to be available.
2. The **target architecture**, which represents the intended direction of the project and must not be interpreted as already deployed.

The diagrams intentionally omit real addresses, internal hostnames, wireless network names, remote-access endpoints, firewall rules, credentials, and hardware identifiers.

## Current Verified State

The dedicated OPNsense appliance provides the firewall, routing, and VLAN gateway layer for the HomeLab. Its upstream connection remains behind the existing ISP equipment, while its internal connection feeds the managed PoE switch. OPNsense has been updated to `26.7.2_2`, and internet and DNS connectivity have been verified after the network changes.

The managed switch is running firmware `3.30.6`, its local administration is accessible, and three role-based VLANs are active. The Proxmox host is running Proxmox VE `9.2.11` and remains reachable from an approved client segment. Initial DNS-access and cross-segment isolation policies have been applied and tested.

The Ubuntu service VM uses private name resolution, key-based remote administration, and a validated Docker platform. Hermes Agent is deployed, its persistent memory loading has been verified across sessions, and persistent-memory writes now use an explicitly tested approval step. Home Assistant runs in a separate VM with private name resolution and connected companion apps on selected mobile devices. One Voice Preview Edition unit has completed onboarding, and one end-to-end request returned the expected response through the configured Home Assistant-to-Hermes path. This is an initial functional result, not evidence of sustained reliability, acceptable latency, complete device coverage, or home-device control.

Uptime Kuma runs as a separate container workload with initial alerting configured. The Home Assistant monitor was saved and reported **Up**. This confirms the configured availability check at that time; it does not establish complete service coverage, successful notification delivery for every monitor, or recovery capability.

Tailscale provides private remote administration of the Hermes host. The selected travel laptop has passed an external-network access test through a mobile hotspot. A dedicated Tailscale container is also present in the workload inventory; that alone does not establish verified subnet routing, Exit Node operation, or network-wide access. Broader remote-access policy and client validation remain in progress.

Final private network-configuration backups have been saved and verified. Initial encrypted VM and container backups and a later manual VM backup were copied to separate storage and checked with matching SHA-256 checksums. A separate encrypted VM-level Home Assistant recovery copy was exported to secondary storage; its source-to-copy integrity and restoration remain pending. A private assistant-configuration safety copy was also created after the initial voice-path configuration, but it has not been recovery-tested.

The following diagram shows workload placement and the tested access and monitoring relationships. It is not a map of firewall permissions.

```mermaid
flowchart TD
    ISP["ISP equipment"] --> FW["OPNsense firewall"]
    FW --> SW["Managed switch and segmented network"]
    SW --> PVE["Proxmox VE"]
    PVE --> HERMES["Ubuntu VM: Docker and Hermes"]
    PVE --> HA["Home Assistant VM"]
    PVE --> KUMA["Uptime Kuma container"]
    PVE --> TS["Tailscale container"]
    VOICE["Voice interface: one unit tested"] --> HA
    HA -->|"initial request path"| HERMES
    KUMA -. "availability check: Up" .-> HA
    REMOTE["Approved travel laptop"] -. "Tailscale and key-based SSH" .-> HERMES
```

### Verified Components

| Layer | Component | Verified state |
| --- | --- | --- |
| Physical | 12U rack and rack accessories | Completed; equipment placement, physical cabling, private labeling, ventilation checks, and power-distribution review have been verified. |
| Compute | GMKtec virtualization host | Proxmox VE `9.2.11` is installed, updated, accessible through its segmented management path, and protected with a separate administrative account and multi-factor authentication. |
| Storage | Proxmox local storage | An operating system ISO has been uploaded. |
| Virtualization | Virtual machines and containers | The hardened Ubuntu Server `24.04.4 LTS` guest hosts Docker and Hermes. Home Assistant has a separate VM; Uptime Kuma and Tailscale have separate container workloads. |
| Edge security | Dedicated Intel N100 appliance | OPNsense `26.7.2_2` is installed; routing, DHCP, DNS, internet access, local administration, segmented access, and initial cross-segment policy enforcement have been verified. |
| Switching | TP-Link managed PoE switch | Firmware `3.30.6` is installed; private management, traffic forwarding, and three role-based VLANs are operational. |
| Containers | Docker Engine and Docker Compose | Docker Engine `29.7.2` and Docker Compose `5.5.0` are installed and validated on the first Linux guest. |
| Assistant | Hermes Agent | Deployed on the first guest; persistent-memory loading and an approval-gated write cycle have been verified. |
| Remote access | Tailscale private overlay | Private administration of the Hermes host is externally tested, including access from the selected travel laptop through a mobile hotspot. The dedicated container's presence does not by itself verify routed access. |
| Home automation | Home Assistant | Operational in a separate VM with private name resolution and connected mobile companion apps. One voice unit completed onboarding and one Home Assistant-to-Hermes request/response cycle succeeded; broader validation remains in progress. |
| Availability monitoring | Uptime Kuma | Operational with initial alerting configured; the Home Assistant monitor reported **Up** after saving. |
| Recovery copy | Home Assistant VM backup | An encrypted VM-level copy was exported to secondary storage. Source-to-copy integrity and restoration have not yet been demonstrated. |
| Future services | n8n, Prometheus, and Grafana | Planned; not documented as deployed. |

## Verified Network Segmentation

OPNsense remains the firewall, routing, DNS, and policy-enforcement layer, while the managed switch transports the segmented network to approved devices. Three VLANs have been deployed and preserved through the final update and validation cycle. Initial rules allow required DNS and approved administrative access while blocking tested cross-segment paths that are not required. Public labels are deliberately generic and do not reveal live VLAN identifiers, addressing, port assignments, or policy details.

VLAN transport, approved Proxmox reachability, internet access, segment-specific DNS access, and selected isolation paths have been verified. The separate Tailscale overlay provides tested remote access to the Hermes host, including the travel-laptop test. These tests establish an initial least-privilege baseline; comprehensive policy review, broader remote administration, and workload-level isolation remain future work. A service being reachable or monitored does not prove that every unwanted cross-segment path is blocked.

## Target Logical Architecture

Proxmox VE remains the virtualization layer for the operational assistant, home-automation, monitoring, and remote-access workloads. Their separate placement allows maintenance to be planned by role. Future integrations must define permissions, secret handling, health checks, and recovery procedures before they are treated as operational.

```mermaid
flowchart TD
    VOICE["Voice interface: one unit tested"] --> HA["Home Assistant: operational"]
    HA -->|"initial request and response verified"| HERMES["Hermes: operational"]
    HERMES -. "planned workflows" .-> N8N["n8n: planned"]
    N8N -. "planned heavy tasks" .-> GPU["GPU workstation: planned"]
```

The solid path records one successful request-and-response validation; it does not establish reliable repeated operation, validation of both voice units, home-device control, or broad permissions. The dashed relationships remain intended integrations. n8n, Prometheus, Grafana, and GPU integration remain planned. Initial Uptime Kuma availability checks do not replace the planned metrics and capacity-monitoring layer.

The GPU-equipped primary workstation is not intended to be permanently dedicated to Hermes or other HomeLab services. The target design treats it as an on-demand compute node for approved heavy local-AI tasks. When the workstation is off, an authorized automation may request Wake-on-LAN; automatic suspension or shutdown after an automated task will be evaluated later. The GPU must remain available for interactive workloads such as streaming and must not be consumed merely because the computer is powered on.

## Functional Layers

| Layer | Planned role | Current status |
| --- | --- | --- |
| Edge and routing | OPNsense routing, firewalling, VLAN gateways, and controlled remote access | Operational segmented foundation with initial DNS and isolation policies verified; comprehensive policy review and network-wide remote administration remain pending. |
| Remote access | Private access to selected services from approved external devices | Tailscale access to the Hermes host is operational; the selected travel laptop passed an external mobile-hotspot test. Broader client validation and policy refinement remain in progress. |
| Network distribution | Managed switching and role-based segmentation | Traffic forwarding, private management, firmware, and three VLANs are operational. |
| Virtualization | Virtual machines and separate service workloads | Proxmox VE `9.2.11` hosts the Ubuntu assistant guest, a separate Home Assistant VM, and container workloads for Uptime Kuma and Tailscale. |
| Containers | Reproducible deployment of selected services | Docker Engine `29.7.2` and Docker Compose `5.5.0` are operational on the first guest. |
| Home automation | Home Assistant and local voice interfaces | Home Assistant and selected mobile companion apps are operational. One voice unit and one request/response path to Hermes are verified; reliability, remaining-device rollout, and approved control actions remain in progress. |
| Observability | Availability checks, alerts, metrics, and dashboards | Uptime Kuma and initial alerting are configured; Home Assistant reported **Up**. Broader coverage and notification validation remain in progress. Prometheus and Grafana are planned. |
| Assistant platform | Persistent local assistant using Hermes Agent | Operational initial deployment with cross-session memory loading, approval-gated writes, and an initial Home Assistant voice request/response path verified. |
| AI compute | Heavy local inference on the GPU-equipped workstation | Planned as an on-demand node; Wake-on-LAN and workload controls are not yet integrated. |
| Storage and backups | Network configuration, workload and service backups, future NAS, and recovery procedures | Earlier encrypted VM and container backups and the follow-up VM copy passed integrity validation. A separate encrypted VM-level Home Assistant recovery copy was exported, but its source-to-copy integrity and restoration are not established here. A private assistant-configuration safety copy exists without a recovery claim. Recurring rotation and controlled restoration remain pending. |

## Architecture Principles

The project will follow these principles as it evolves:

- **Verified documentation:** deployed and planned components are always identified separately.
- **Least privilege:** services should receive only the access needed for their role.
- **Separation of responsibilities:** firewalling, virtualization, automation, monitoring, and experimental workloads should remain logically distinct.
- **Safe changes:** major network changes should be tested before becoming the primary network path.
- **Reproducibility:** relevant deployment steps and sanitized example configurations should be documented.
- **Observability:** important services should eventually expose health and performance information without publishing sensitive operational data.
- **Recoverability:** private network-configuration and encrypted workload backups are retained and integrity-checked, while restoration procedures must still be tested before recovery is treated as dependable.
- **Privacy by design:** public documentation must not reveal details that could identify or weaken the live environment.

## Future Documentation

The existing physical-setup, Proxmox, network-design, roadmap, and changelog documents will be updated as milestones are verified. New implementation records will be added only after the corresponding work is completed. Planned topics include:

- Hermes Agent expansion and integration notes
- Segmentation policy refinement and recovery-validation notes
- Service deployment records
- Backup rotation, controlled restoration, and recovery procedures

## Public Documentation Boundaries

Future diagrams and examples will use descriptive labels and documentation-only values. The public repository will not include:

- Real public or private IP addresses
- Internal DNS names or Wi-Fi identifiers
- MAC addresses, serial numbers, or device labels
- Credentials, tokens, private keys, certificates, or recovery codes
- Complete firewall exports or backup files
- Remote-access endpoints
- Camera streams, access details, or private physical-layout information

These boundaries allow the project to demonstrate architecture and operational knowledge without exposing the live HomeLab.
