# HomeLab Project Roadmap

> **Last verified:** August 2026  
> **Project status:** Work in progress  
> **Current focus:** Physical cabling and network foundation

This roadmap describes the planned evolution of the HomeLab and distinguishes verified work from future objectives. A milestone is marked as **Completed** only after it has been implemented, tested, and documented. Purchasing or physically possessing hardware does not by itself mean that the related milestone has been completed.

No fixed completion dates are published at this stage. The project is developed progressively alongside formal studies and practical learning, and this document will be updated when evidence for each milestone is available.

## Status Definitions

| Status | Meaning |
| --- | --- |
| **Completed** | Implemented, tested, and documented. |
| **In progress** | Work has started, but the milestone has not yet met its completion criteria. |
| **Pending** | Confirmed as a next step, but implementation has not started or has not been verified. |
| **Planned** | Part of the target design; final technical decisions may still change. |
| **Under evaluation** | Being considered, with no deployment commitment yet. |

## Roadmap Overview

| Phase | Objective | Current status |
| --- | --- | --- |
| 1. Physical foundation | Assemble the rack and prepare safe equipment placement and cable management | **In progress** |
| 2. Virtualization foundation | Install Proxmox VE and deploy the first validated guest workload | **In progress** |
| 3. Network foundation | Deploy OPNsense and the managed switch as a tested network path | **Pending** |
| 4. Core service platform | Create Linux workloads and a controlled container-hosting environment | **Planned** |
| 5. Automation and observability | Deploy Home Assistant, local voice integration, Prometheus, and Grafana | **Planned** |
| 6. Assistant platform | Deploy and integrate Hermes Agent as a persistent HomeLab assistant | **Planned** |
| 7. Security and resilience | Add segmentation, controlled remote access, backups, recovery tests, and hardening | **Planned** |
| 8. Advanced labs | Build isolated cybersecurity, development, and optional AI-compute experiments | **Under evaluation** |

## Phase 1 — Physical Foundation

**Status: In progress**

### Verified progress

- [x] Assemble the 12U open rack.
- [x] Install the rack shelf and cable-management accessories.
- [x] Make the firewall appliance, managed switch, UPS, display, and KVM equipment available for the build.
- [ ] Complete and label the final cabling.
- [ ] Verify power distribution and document the connected load safely.
- [ ] Produce sanitized physical-layout photographs or diagrams suitable for the public repository.

### Completion criteria

- Equipment is safely positioned and powered.
- Required network and KVM connections are tested.
- Cable routing does not obstruct ventilation or create unnecessary strain.
- The public physical-setup documentation matches the verified installation.

## Phase 2 — Virtualization Foundation

**Status: In progress**

### Verified progress

- [x] Install Proxmox VE on the GMKtec virtualization host.
- [x] Verify access to the Proxmox web interface.
- [x] Upload an operating system ISO to local storage.
- [ ] Complete, boot, and validate the first virtual machine.
- [ ] Document guest resource allocation and installation decisions.
- [ ] Define an initial backup and restoration procedure.

### Completion criteria

- At least one guest has been created, booted, updated, and reached through an approved management method.
- CPU, memory, storage, and network choices are documented without exposing live identifiers.
- A basic backup has been created and a restoration method has been reviewed or tested.

## Phase 3 — Network Foundation

**Status: Pending**

The dedicated firewall appliance currently has pfSense preinstalled. The target platform is OPNsense, but the migration and final network deployment have not started. The TP-Link JetStream TL-SG2008P V3 is also available but is not yet connected or configured.

### Planned work

- [ ] Record the existing connectivity requirements before making changes.
- [ ] Install OPNsense on the dedicated Intel N100 appliance.
- [ ] Assign and validate WAN and LAN roles without publishing live interface details.
- [ ] Back up the initial sanitized configuration privately.
- [ ] Connect and update the managed switch.
- [ ] Configure switch management and test wired connectivity.
- [ ] Validate internet access, local administration, DNS, and expected client connectivity.
- [ ] Prepare a rollback procedure before using the new path for normal household connectivity.
- [ ] Document the final high-level topology using sanitized labels.

### Completion criteria

- OPNsense boots reliably and the intended network roles have been tested.
- The managed switch operates in the approved network path.
- Essential client connectivity has been validated.
- A rollback path and private configuration backup exist.
- Public documentation contains no live addresses, credentials, identifiers, or remote-access details.

## Phase 4 — Core Service Platform

**Status: Planned**

### Planned work

- [ ] Deploy a maintained Linux server guest for selected infrastructure workloads.
- [ ] Decide which workloads require separate VMs and which may use containers.
- [ ] Install a container runtime only after the host role and security boundaries are defined.
- [ ] Use sanitized example configuration files and keep live secrets outside Git.
- [ ] Document update, health-check, backup, and recovery procedures for each service.

The final VM and container layout has not been selected. Docker or another container platform must not be described as deployed until installation and validation are complete.

## Phase 5 — Automation and Observability

**Status: Planned**

### Planned work

- [ ] Deploy Home Assistant in an appropriate isolated workload.
- [ ] Integrate the available Home Assistant Voice hardware.
- [ ] Define which local devices may be controlled and what permissions they require.
- [ ] Deploy Prometheus for selected metrics.
- [ ] Deploy Grafana dashboards for infrastructure health and capacity.
- [ ] Configure alerting only after useful thresholds and notification paths are defined.

No home-automation, voice, Prometheus, or Grafana service is currently deployed.

## Phase 6 — Assistant Platform

**Status: Planned**

The target architecture combines two different roles:

- **ChatGPT Work** supports interactive studies, programming, research, file analysis, and production of complex deliverables.
- **Hermes Agent** is planned as the persistent HomeLab assistant for local automation, recurring tasks, monitoring, and approved messaging or voice interfaces.

### Planned work

- [ ] Define Hermes Agent's workload placement and resource limits.
- [ ] Design its memory, skills, and secret-management boundaries.
- [ ] Integrate approved Home Assistant, monitoring, and automation functions gradually.
- [ ] Restrict commands to authorised identities and require confirmation for sensitive actions.
- [ ] Record operational costs and decide when tasks should use local or paid AI services.
- [ ] Test failure handling before granting control of important infrastructure.

Hermes Agent is not currently installed or connected to the HomeLab.

## Phase 7 — Security and Resilience

**Status: Planned**

### Planned work

- [ ] Design network segmentation based on device roles and trust levels.
- [ ] Introduce VLANs only after the base network is stable and recovery access is understood.
- [ ] Apply least-privilege firewall rules and test expected traffic explicitly.
- [ ] Add controlled remote access through a reviewed VPN design.
- [ ] Create configuration and service backups outside the public repository.
- [ ] Test recovery procedures instead of relying only on successful backup jobs.
- [ ] Review logging, patching, account security, and administrative access.
- [ ] Document security improvements using sanitized evidence.

VLANs, VPN access, production firewall rules, and automated backups are not currently deployed or verified.

## Phase 8 — Advanced Labs

**Status: Under evaluation**

Possible future work includes:

- Isolated systems-administration and cybersecurity practice environments
- Blue Team monitoring and controlled security-testing labs
- Development and database workloads connected to DAM studies
- Optional integration of the GPU-equipped workstation for local AI workloads
- A future NAS and a documented storage, backup, and recovery design
- Additional specialised agents coordinated through the persistent assistant platform

These items are exploratory and may change as the project, studies, budget, and technical requirements evolve.

## Immediate Next Milestones

The next verified updates should follow this order:

1. Complete the current physical cabling work.
2. Install and perform initial validation of OPNsense on the dedicated firewall appliance.
3. Connect and perform the initial managed-switch setup.
4. Test the intended firewall-to-switch network path and retain a rollback option.
5. Complete and validate the first Proxmox virtual machine.
6. Update the architecture, physical setup, Proxmox notes, and this roadmap with verified results.

This order may be adjusted if testing identifies a safer dependency sequence. Any change will be documented rather than silently presented as part of the original plan.

## Documentation Rule

Every completed milestone should add or update:

- A clear description of the objective and final result
- The main technical decisions and their reasoning
- Sanitized implementation steps or example configuration
- Validation evidence that does not expose the live environment
- Problems encountered and lessons learned
- Backup, rollback, or recovery information where relevant
- The status in this roadmap and the repository README

The roadmap is a living document, but status changes require evidence. Planned architecture is valuable as design work; it must remain visibly separate from verified implementation.
