# Uptime Kuma Deployment

> **Last documented:** September 2026  
> **Status:** Initial availability monitoring operational; broader coverage and per-monitor notification validation in progress

This document records the initial Uptime Kuma deployment and the available Home Assistant monitoring result. Live monitor targets, device names, addresses, notification destinations, credentials, and dashboard exports remain private.

## Deployment Summary

Uptime Kuma runs in a separate container workload on the Proxmox host. Initial alerting is configured. The existing Home Assistant monitor was saved and reported **Up** during the latest validation.

The recorded result establishes that the configured availability check succeeded at that time. The exact monitor type, check parameters, and complete target inventory are not specified here. This document does not claim continuous availability, full infrastructure coverage, or successful notification delivery for every monitor.

## Recorded Progress

| Area | Recorded state | Validation boundary |
| --- | --- | --- |
| Workload placement | Separate Uptime Kuma container on Proxmox | The monitor shares the physical virtualization host with the services it observes. |
| Monitoring service | Initial deployment operational | Long-term availability and complete monitoring coverage are not established by the deployment record. |
| Initial alerting | Configured | Notification delivery and recovery messages require a recorded result for each required monitor and destination. |
| Home Assistant monitor | Existing monitor saved; state reported **Up** | This confirms its configured availability check at that time. |
| Metrics and capacity monitoring | Prometheus and Grafana remain planned | Their deployment is separate from the initial Uptime Kuma milestone. |
| Monitoring recovery | Not yet documented as tested | Backup coverage, restoration, and restored monitor behavior still need validation. |

## Home Assistant Check

The latest recorded sequence was:

1. Review the existing Home Assistant monitor.
2. Save its configuration.
3. Observe the resulting **Up** state.

An **Up** result is evidence about the configured check. It does not establish that:

- Every Home Assistant integration or mobile access path works.
- Local voice processing or the future Hermes integration is functional.
- A failure notification has reached its intended recipient.
- The Home Assistant backup is complete, protected, or recoverable.

Those outcomes require their own checks. The related application deployment and backup milestones are recorded in [Home Assistant deployment](home-assistant-deployment.md) and [Backup and recovery](backup-and-recovery.md).

## Placement and Failure Boundaries

Uptime Kuma has a separate container workload from the monitored Home Assistant VM. This separates their service environments, while both continue to depend on the same Proxmox host.

If that host or its supporting power or network path becomes unavailable, the local monitoring service may also become unavailable. Independent detection of a complete host or site outage is not established by this deployment. Any future external check should be designed and documented separately.

The monitoring workload should receive only the connectivity required for its checks and notifications. Monitor credentials and notification secrets must remain outside the public repository. No live access-policy configuration is published here.

## Remaining Validation

- Record the private monitor inventory and the purpose of each check.
- Verify that each required monitor is associated with the intended notification path.
- Perform an approved failure-and-recovery test and confirm both detection and notification delivery.
- Review check timing and retry behavior to make alerts useful without excessive noise.
- Extend coverage to required services and document remaining gaps.
- Define backup scope for Uptime Kuma configuration, persistent data, and required secrets.
- Test restoration and confirm that monitors and notifications behave as intended afterward.
- Evaluate independent outage detection for the shared host and network dependencies.
- Add the planned metrics and capacity-monitoring layer when its requirements are defined.

These are follow-up tasks, not claims that failure testing, recovery testing, or comprehensive coverage has already been completed.

## Public Documentation Boundary

Publish only sanitized deployment and validation summaries. Keep monitor URLs, hostnames, addresses, ports tied to live targets, tokens, webhooks, notification recipients, account details, precise schedules, and configuration exports private.

Screenshots require review for target names, dashboard links, browser data, and notification details. Do not upload the live monitoring database or its backup to this repository.

Related records:

- [Architecture](architecture.md)
- [Proxmox installation](proxmox-installation.md)
- [Home Assistant deployment](home-assistant-deployment.md)
- [Backup and recovery](backup-and-recovery.md)
- [Security and privacy](security-and-privacy.md)
