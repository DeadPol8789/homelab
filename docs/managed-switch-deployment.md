# Managed Switch Deployment

> **Last verified:** August 2026  
> **Project status:** Operational segmented managed-switch foundation; further hardening remains in progress

This document records the verified deployment of the TP-Link JetStream managed PoE switch used as the wired distribution point for the HomeLab. It covers its current network role, local management setup, firmware state, VLAN deployment, validation, private backup handling, and remaining hardening boundaries.

The public record intentionally omits the real management address, administrative username, password, MAC address, serial number, exact port assignments, configuration exports, and domestic cable routes.

## Deployment Summary

The managed switch is installed between the OPNsense firewall and selected wired HomeLab devices. It was first used as a basic forwarding point while the firewall and client connectivity were validated. Its local administration interface has since been reached successfully, and a stable private management configuration has been applied.

Firmware information was reviewed against the exact switch family, hardware revision, and regional package requirements before the switch was updated to `3.30.6`. Three role-based VLANs were then deployed and verified. Other advanced Layer 2 features are not presented as enabled unless they have been tested separately.

## Verified Progress

| Stage | Status | Verified result |
| --- | --- | --- |
| Physical connection | **Completed** | The switch is connected between OPNsense and selected wired HomeLab devices. |
| Traffic forwarding | **Verified** | Connected clients can use the segmented HomeLab network through the switch. |
| Local administration | **Verified** | The switch management interface is reachable from an approved local path. |
| Stable management configuration | **Configured** | A private management address has been assigned and tested without publishing the live value. |
| Administrative access | **Configured privately** | Live credentials are stored outside the public repository. |
| Firmware state | **Updated and verified** | Firmware `3.30.6` is installed after compatibility checks against the switch model, hardware revision, and regional requirements. |
| Proxmox connectivity | **Verified** | The virtualization host remains reachable through its segmented managed-switch path after migration. |
| Client connectivity | **Verified** | Selected wired clients retain address assignment, DNS resolution, and internet access. |
| VLAN segmentation | **Deployed and verified** | Three role-based VLANs are active. Live identifiers, port profiles, tagging details, and policy values remain private. |
| Configuration backup | **Verified privately** | A final private configuration copy has been saved and checked. A full restoration test remains separate work. |

## Current Network Role

```mermaid
flowchart TD
    FW["OPNsense firewall<br/>VLAN gateways"] --> SW["Managed PoE switch<br/>Firmware and VLANs verified"]
    SW --> SEG_A["Role-based segment A"]
    SW --> SEG_B["Role-based segment B"]
    SW --> SEG_C["Role-based segment C"]
    SEG_C --> PVE["Proxmox VE host<br/>Reachability verified"]
```

The switch currently transports three role-based VLANs. The diagram does not disclose VLAN identifiers, physical port numbers, management addressing, tagging details, cable routes, or device identifiers.

## Management Decisions

The initial switch setup follows these principles:

- Use a stable private management configuration instead of relying on an unpredictable address.
- Keep the administration interface reachable only through an approved local path.
- Match firmware packages to the exact model, hardware revision, and region.
- Validate connectivity before and after firmware, management, and VLAN changes.
- Avoid publishing complete port maps or live configuration exports.
- Keep the base network recoverable while advanced features are introduced gradually.

The switch is not described as a fully hardened production platform. Its current status is an operational segmented managed foundation.

## Validation Performed

The following checks support the current status:

1. Confirm that the local management interface is reachable.
2. Apply and retest the stable private management configuration.
3. Review firmware compatibility for the exact switch variant and verify firmware `3.30.6` after the update.
4. Confirm that the OPNsense uplink remains operational.
5. Confirm that all three role-based VLANs remain active after the update cycle.
6. Confirm that the Proxmox host remains accessible through its migrated network path.
7. Confirm address assignment, DNS resolution, and internet connectivity from selected wired clients.
8. Save and verify a final private switch-configuration copy.

## Security Considerations

- Administrative credentials must remain outside Git and public screenshots.
- The management interface must not be exposed directly to the internet.
- Firmware must come from the official vendor source and match the exact hardware and region.
- Future remote administration must occur only through an approved secure-access design.
- Configuration backups may contain live management and network details and must remain private.
- SNMP, discovery protocols, logging, and controller integration must be reviewed before being enabled or exposed.
- VLAN changes require a recovery path because an incorrect management VLAN or port profile can remove administrative access.

## Pending Work

The following items remain pending or require separate validation:

- Perform and document a controlled local restoration test.
- Complete final cable organization and private port labeling.
- Decide whether standalone management or controller-based management best fits the HomeLab.
- Review and refine inter-VLAN policy using least-privilege principles.
- Revalidate private access, trunk, tagged, and untagged behavior after future changes.
- Review loop-prevention, discovery, time, logging, and monitoring settings.
- Validate PoE requirements and budget before powering devices from the switch.
- Add secure monitoring only after its access and credential boundaries are defined.

## Completion Boundary

The switch is correctly described as an **operational segmented managed-switch foundation**. Wider network hardening remains **in progress** until restoration testing, remaining client requirements, final cabling, monitoring decisions, and inter-VLAN policy refinement have been completed and documented.

## Information Intentionally Omitted

This public document does not include:

- The real management address, subnet, gateway, or management URL
- Administrative usernames, passwords, recovery information, or session data
- MAC addresses, serial numbers, device labels, or account identifiers
- Exact physical port assignments, cable routes, or domestic locations
- Complete configuration exports, logs, packet captures, or screenshots
- VLAN identifiers, live subnets, controller endpoints, or remote-access details
- ISP information, Wi-Fi credentials, or unrelated client information

Any future screenshots or configuration examples must be sanitized at full resolution before publication.
