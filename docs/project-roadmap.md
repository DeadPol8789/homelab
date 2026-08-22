# HomeLab Project Roadmap

> **Last verified:** August 2026  
> **Project status:** Work in progress  
> **Current focus:** Recovery testing, inter-VLAN policy refinement, final cabling, and the first virtual machine

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
| 3. Network foundation | Deploy OPNsense and the managed switch as a tested segmented network path | **Completed** |
| 4. Core service platform | Create Linux workloads and a controlled container-hosting environment | **Planned** |
| 5. Automation and observability | Deploy Home Assistant, local voice integration, n8n, Prometheus, and Grafana | **Planned** |
| 6. Assistant platform | Deploy and integrate Hermes Agent as a persistent HomeLab assistant | **Planned** |
| 7. Security and resilience | Maintain segmentation and add controlled remote access, recovery tests, and further hardening | **In progress** |
| 8. Advanced labs | Build isolated cybersecurity, development, and optional AI-compute experiments | **Under evaluation** |

## Phase 1 — Physical Foundation

**Status: In progress**

### Verified progress

- [x] Assemble the 12U open rack.
- [x] Install the rack shelf and cable-management accessories.
- [x] Make the firewall appliance, managed switch, UPS, display, and KVM equipment available for the build.
- [x] Connect and validate the base firewall-to-switch path and selected wired devices.
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
- [x] Apply the available host updates and configure the package source for the non-subscribed lab environment.
- [x] Configure stable private management connectivity and local name resolution.
- [x] Migrate and verify the Proxmox management path within the segmented network.
- [x] Create a separate administrative account and protect it with multi-factor authentication.
- [ ] Complete, boot, and validate the first virtual machine.
- [ ] Document guest resource allocation and installation decisions.
- [ ] Define an initial backup and restoration procedure.

### Completion criteria

- At least one guest has been created, booted, updated, and reached through an approved management method.
- CPU, memory, storage, and network choices are documented without exposing live identifiers.
- A basic backup has been created and a restoration method has been reviewed or tested.

## Phase 3 — Network Foundation

**Status: Completed**

OPNsense `26.7.2_2` is installed on the dedicated firewall appliance, and the segmented path through the managed switch is operational for selected wired devices. The switch is running firmware `3.30.6`, its private administration path is operational, and three role-based VLANs have been deployed and verified.

### Verified progress

- [x] Install OPNsense on the dedicated Intel N100 appliance.
- [x] Confirm reliable boot from internal storage.
- [x] Assign and validate the initial WAN and LAN roles without publishing live interface details.
- [x] Enable the initial Kea DHCPv4 service for the HomeLab LAN.
- [x] Validate client addressing, DNS resolution, internet connectivity, and local administration.
- [x] Connect the managed switch and use it to forward traffic to selected wired devices.
- [x] Secure the managed-switch administration path and verify local access.
- [x] Configure stable private switch management without publishing live values.
- [x] Review switch firmware compatibility.
- [x] Update OPNsense and the managed-switch firmware to the verified versions.
- [x] Deploy and validate three role-based VLANs.
- [x] Migrate the Proxmox management path and verify continued reachability.
- [x] Retest internet access and DNS resolution after segmentation.
- [x] Export an initial OPNsense configuration backup privately.
- [x] Save and check final private network-configuration backups.
- [x] Enable multi-factor authentication for OPNsense administration.
- [x] Document the final high-level topology using sanitized labels.

### Operational follow-up

The foundation objective is complete. DHCP-reservation review, broader client migration, controlled restoration testing, policy refinement, VPN access, and monitoring remain tracked as operational or security-resilience work rather than blockers for this phase.

### Completion criteria

- OPNsense boots reliably and the intended network roles have been tested.
- The managed switch operates in the approved network path and its administration is secured.
- Selected essential client connectivity has been validated.
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
- [ ] Deploy n8n for approved workflows after its access and secret-management boundaries are defined.
- [ ] Deploy Prometheus for selected metrics.
- [ ] Deploy Grafana dashboards for infrastructure health and capacity.
- [ ] Configure alerting only after useful thresholds and notification paths are defined.

No home-automation, voice, n8n, Prometheus, or Grafana service is currently deployed.

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

**Status: In progress**

### Verified foundation controls

- [x] Enable multi-factor authentication for OPNsense administration.
- [x] Use a separate administrative account with multi-factor authentication for normal Proxmox administration.
- [x] Keep live configuration exports and credentials outside the public repository.
- [x] Export an initial private OPNsense configuration backup.
- [x] Secure local managed-switch administration through a stable private management configuration.
- [x] Review managed-switch firmware compatibility.
- [x] Update OPNsense and the managed-switch firmware and retest the network path.
- [x] Deploy and validate three role-based VLANs.
- [x] Save and check final private network-configuration backups.
- [x] Apply a security-focused `.gitignore` and public-documentation policy.

### Planned work

- [ ] Review and refine inter-VLAN rules using least-privilege principles.
- [ ] Add controlled remote access through a reviewed VPN design.
- [ ] Define recurring configuration and service backups outside the public repository.
- [ ] Test recovery procedures instead of relying only on successful backup jobs.
- [ ] Review logging, patching, account security, and administrative access.
- [ ] Document security improvements using sanitized evidence.

Three role-based VLANs and private network-configuration backups are deployed and verified. VPN access, advanced least-privilege policy, automated backup rotation, and controlled restoration testing are not yet deployed or verified.

## Phase 8 — Advanced Labs

**Status: Under evaluation**

Possible future work includes:

- Isolated systems-administration and cybersecurity practice environments
- Blue Team monitoring and controlled security-testing labs
- Development and database workloads connected to DAM studies
- Optional integration of the GPU-equipped workstation for local AI workloads
- A future NAS and a documented storage, backup, and recovery design
- Additional specialised agents coordinated through the persistent assistant platform

The GPU-equipped workstation has been selected as a future on-demand compute node rather than a permanently dedicated Hermes resource. Wake-on-LAN and post-task power management remain planned and have not been integrated. The other advanced-lab items remain exploratory and may change as the project, studies, budget, and technical requirements evolve.

## Immediate Next Milestones

The next verified updates should follow this order:

1. Perform and document a controlled restoration test for the private network backups.
2. Confirm required DHCP reservations and remaining essential client connectivity.
3. Review and refine inter-VLAN policy using least-privilege principles.
4. Complete the current physical cable organization and safe labeling.
5. Complete, update, and validate the first Proxmox virtual machine.
6. Create and verify the first VM backup before deploying important services.
7. Design controlled remote access through a reviewed VPN solution.

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
