# HomeLab Project Roadmap

> **Last verified:** September 2026  
> **Project status:** Work in progress  
> **Current focus:** Travel-client remote access, access governance, controlled restoration, backup automation, assistant memory, and monitoring

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
| 1. Physical foundation | Assemble the rack and complete safe equipment placement, cabling, labeling, ventilation, and power review | **Completed** |
| 2. Virtualization foundation | Install Proxmox VE and deploy the first validated guest workload | **Completed** |
| 3. Network foundation | Deploy OPNsense and the managed switch as a tested segmented network path | **Completed** |
| 4. Core service platform | Create Linux workloads and a controlled container-hosting environment | **In progress** |
| 5. Automation and observability | Deploy Home Assistant, local voice integration, n8n, Prometheus, and Grafana | **Planned** |
| 6. Assistant platform | Deploy and integrate Hermes Agent as a persistent HomeLab assistant | **In progress** |
| 7. Security and resilience | Maintain segmentation and add controlled remote access, recovery tests, and further hardening | **In progress** |
| 8. Advanced labs | Build isolated cybersecurity, development, and optional AI-compute experiments | **Under evaluation** |

## Phase 1 — Physical Foundation

**Status: Completed**

### Verified progress

- [x] Assemble the 12U open rack.
- [x] Install the rack shelf and cable-management accessories.
- [x] Make the firewall appliance, managed switch, UPS, display, and KVM equipment available for the build.
- [x] Connect and validate the base firewall-to-switch path and selected wired devices.
- [x] Complete and privately label the final cabling.
- [x] Verify power distribution and document the connected load safely.
- [x] Verify ventilation, physical stability, cable organization, and strain relief.
- [x] Document physical completion using sanitized text and diagrams.

### Completion criteria

- Equipment is safely positioned and powered.
- Required network and KVM connections are tested.
- Cable routing does not obstruct ventilation or create unnecessary strain.
- The public physical-setup documentation matches the verified installation.

The physical-foundation objective is complete. Public rack photographs remain optional and must pass the repository privacy checklist before publication.

## Phase 2 — Virtualization Foundation

**Status: Completed**

### Verified progress

- [x] Install Proxmox VE on the GMKtec virtualization host.
- [x] Verify access to the Proxmox web interface.
- [x] Upload an operating system ISO to local storage.
- [x] Update the host to Proxmox VE `9.2.11` and configure the package source for the non-subscribed lab environment.
- [x] Configure stable private management connectivity and local name resolution.
- [x] Migrate and verify the Proxmox management path within the segmented network.
- [x] Verify Proxmox administration from an approved client segment.
- [x] Prepare and verify the network-policy and private name-resolution foundation for the first service workload.
- [x] Create a separate administrative account and protect it with multi-factor authentication.
- [x] Complete, boot, update, restart, and validate the first Ubuntu Server virtual machine.
- [x] Verify key-based administration through a dedicated non-root account.
- [x] Disable password-based SSH authentication and direct root login.
- [x] Document the guest deployment without publishing live resource or network identifiers.

### Completion criteria

- At least one guest has been created, booted, updated, and reached through an approved management method.
- Guest purpose, operating system, administration, and network choices are documented without exposing live identifiers.

Guest backup rotation and controlled restoration remain tracked in Phase 7 and are not blockers for the completed virtualization-foundation objective.

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
- [x] Apply and verify required DNS access for selected network roles.
- [x] Verify approved access to the Proxmox administration path.
- [x] Apply and verify isolation between selected management and service-oriented roles.
- [x] Prepare private name resolution for the first service workload.
- [x] Document the final high-level topology using sanitized labels.

### Operational follow-up

The foundation objective is complete, and an initial DNS and cross-segment policy baseline has also been verified. A private Tailscale path to the Hermes host has since been externally tested. DHCP-reservation review, broader client migration, controlled restoration testing, comprehensive policy review, network-wide remote administration, and monitoring remain tracked as operational or security-resilience work rather than blockers for this phase.

### Completion criteria

- OPNsense boots reliably and the intended network roles have been tested.
- The managed switch operates in the approved network path and its administration is secured.
- Selected essential client connectivity has been validated.
- A rollback path and private configuration backup exist.
- Public documentation contains no live addresses, credentials, identifiers, or remote-access details.

## Phase 4 — Core Service Platform

**Status: In progress**

### Verified progress

- [x] Deploy a maintained Ubuntu Server guest for selected infrastructure workloads.
- [x] Install and validate Docker Engine `29.7.2` and Docker Compose `5.5.0`.
- [x] Verify the Docker service, container runtime, and a disposable test container.
- [x] Use sanitized documentation and keep live secrets outside Git.

### Planned work

- [ ] Decide which workloads require separate VMs and which may use containers.
- [ ] Document update, health-check, backup, and recovery procedures for each service.
- [ ] Add monitoring and alerting for the Linux guest and critical services.

The first Linux and Docker foundation is operational. The final multi-workload layout, recurring maintenance, monitoring, backup rotation, and recovery procedures remain in progress.

## Phase 5 — Automation and Observability

**Status: In progress**

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

**Status: In progress**

The target architecture combines two different roles:

- **ChatGPT Work** supports interactive studies, programming, research, file analysis, and production of complex deliverables.
- **Hermes Agent** is the operational initial HomeLab assistant and is intended to expand into local automation, recurring tasks, monitoring, and approved messaging or voice interfaces.

### Verified progress

- [x] Deploy Hermes Agent on the first hardened Linux guest.
- [x] Validate the initial text-based assistant workflow.
- [x] Create the initial persistent user profile.
- [x] Confirm automatic memory loading in a new session.
- [x] Keep live credentials, configuration, and memory content outside the public repository.
- [x] Deploy Tailscale on the Hermes host and one approved client.
- [x] Verify key-based SSH to the host from an external network without public port forwarding.

### Planned work

- [ ] Expand the memory design with a reviewed knowledge-base and retrieval layer.
- [ ] Define isolated administrator, personal, and restricted-user profiles.
- [ ] Integrate approved Home Assistant, monitoring, and automation functions gradually.
- [ ] Restrict commands to authorised identities and require confirmation for sensitive actions.
- [ ] Record operational costs and decide when tasks should use local or paid AI services.
- [ ] Test failure handling before granting control of important infrastructure.
- [ ] Enroll and externally test the selected travel and backup clients.
- [ ] Add an approved remote Hermes conversation interface; the current remote path provides host administration only.

Hermes Agent, its initial persistent-memory workflow, and private remote administration of its host are operational. The phase remains **In progress** until the wider client rollout, a remote assistant interface, expanded memory, user isolation, monitoring, and selected Home Assistant integrations are implemented and tested.

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
- [x] Apply and verify required DNS access for selected network roles.
- [x] Verify Proxmox administration from an approved client segment.
- [x] Block and test a selected management-to-service path.
- [x] Operate private name resolution for the first service workload.
- [x] Harden the first Linux guest with non-root, key-based remote administration.
- [x] Disable password-based SSH authentication and direct root login on the first guest.
- [x] Create initial compressed backups of the current VM and container workloads.
- [x] Encrypt the initial workload backups before secondary storage.
- [x] Copy the encrypted archives away from the primary virtualization host.
- [x] Verify matching SHA-256 checksums between encrypted source and secondary copies.
- [x] Establish private Tailscale access between the Hermes host and one approved client.
- [x] Verify key-based SSH through Tailscale from outside the home network.
- [x] Confirm that the tested remote path requires no direct public inbound service.
- [x] Apply a security-focused `.gitignore` and public-documentation policy.

### Planned work

- [ ] Complete the inter-VLAN policy review using least-privilege principles.
- [ ] Enroll and externally test the selected travel and backup clients.
- [ ] Review remote-access policy, device lifecycle, authorization, and recovery procedures.
- [ ] Decide whether subnet routing or Exit Node operation is required before deploying either capability.
- [ ] Define restricted access for any future additional users without exposing infrastructure administration.
- [ ] Finalize cleanup or retention handling for unencrypted working archives.
- [ ] Define recurring configuration and service backups outside the public repository.
- [ ] Add retention, capacity, and backup-failure monitoring.
- [ ] Test recovery procedures instead of relying only on successful backup jobs.
- [ ] Review logging, patching, account security, and administrative access.
- [ ] Document security improvements using sanitized evidence.

Three role-based VLANs, private network-configuration backups, required DNS access, approved Proxmox administration, a selected cross-segment isolation path, encrypted initial VM and container backups, and one private Tailscale host-access path are deployed and verified. The workload copies passed SHA-256 comparison after transfer to separate storage, and key-based SSH through Tailscale was tested from an external network. Wider client enrollment, network-wide remote administration, subnet routing, Exit Node operation, comprehensive least-privilege review, automated backup rotation, and controlled restoration testing are not yet deployed or verified.

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

1. Enroll the selected travel laptop in Tailscale and repeat the external-network access test.
2. Prepare and test selected backup clients where required.
3. Review Tailscale authorization, device lifecycle, and recovery procedures.
4. Perform and document a controlled restoration test for the private network backups.
5. Confirm required DHCP reservations and remaining essential client connectivity.
6. Complete the inter-VLAN policy review using least-privilege principles.
7. Finalize local working-archive cleanup and define recurring guest, Hermes configuration, and memory backups.
8. Perform controlled VM and container restoration tests.
9. Expand Hermes memory with a reviewed knowledge-base and retrieval layer.
10. Add monitoring and actionable alerts for the host, guest, and assistant service.

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
