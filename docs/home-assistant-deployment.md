# Home Assistant Deployment

> **Last documented:** September 2026  
> **Status:** Initial deployment operational; application backup exported and copied; voice validation in progress

This document records the initial Home Assistant deployment. It separates application availability, backup handling, and voice configuration so that progress in one area does not imply completion of the others.

Live guest identifiers, addresses, DNS records, device names, account data, backup metadata, and configuration exports are excluded.

## Deployment Summary

Home Assistant runs in its own virtual machine on the existing Proxmox host, separately from the Ubuntu guest that hosts Docker and Hermes Agent. Private name resolution has been verified, and Home Assistant companion apps on selected phone and tablet clients are connected.

Uptime Kuma provides an initial availability check. The Home Assistant monitor was saved and reported **Up**. Initial alerting exists in the monitoring platform, but this record does not establish a successful failure-and-recovery notification test for this specific monitor.

A Home Assistant application backup has been exported, its archive listing inspected, and a copy placed on external storage. This is an application export, distinct from a Proxmox VM backup. Controlled application restoration has not yet been documented.

## Recorded Progress

| Area | Recorded result | Boundary |
| --- | --- | --- |
| Workload placement | Home Assistant operates in a separate Proxmox VM | Separate placement does not by itself prove network isolation or recoverability. |
| Private name resolution | Resolution for the application has been verified | Live DNS records and addresses remain private. |
| Mobile access | Companion apps on selected phone and tablet clients are connected | This does not establish external Home Assistant access from every mobile device. |
| Availability monitoring | The saved Home Assistant monitor reported **Up** in Uptime Kuma | This is the result of the configured check at that time, not proof that every integration works. |
| Application backup | Export completed, archive listing inspected, and copy placed on external storage | Protection, source-to-copy integrity checks, and restoration for this export still need a documented result. |
| Voice hardware | Two Home Assistant Voice Preview Edition devices are available and voice setup has started | Reliable end-to-end voice operation remains unverified in this record. |
| Hermes integration | Planned as a later approved integration | Home Assistant deployment does not establish voice access to Hermes or assistant control of home devices. |

## Workload and Access Design

The separate Home Assistant VM keeps its application environment distinct from the existing assistant guest. Maintenance and recovery can therefore be planned for each service role. Resource assignments and live network settings are retained privately.

The verified mobile-app connections are recorded independently from the external Tailscale test to the Hermes host. That host-administration test must not be used as evidence of remote Home Assistant access or unrestricted access to the HomeLab.

Future device control and assistant integrations require defined permissions and explicit functional tests. No household device-control scope is claimed by this initial deployment record.

## Application Backup

The recorded sequence was:

1. Export a Home Assistant application backup.
2. Inspect its archive listing.
3. Copy the export to external storage.

The listing included application data, local speech-component data, SSL-related content, and backup metadata. Their presence establishes only that those entries appeared in the archive. It does not prove that every payload is usable, that speech processing works, or that the application can be restored successfully.

Earlier VM and container backups passed encryption and SHA-256 comparison steps. Those results apply to their respective archives and cannot establish protection or transfer integrity for this new application export. See [Backup and recovery](backup-and-recovery.md) for the separate scopes and remaining checks.

## Voice Configuration

Voice setup is in progress. The available troubleshooting record includes a satellite-loading issue and a speech-component configuration error. A verified resolution and successful end-to-end voice test are not yet recorded here.

The next voice validation should demonstrate the intended input, processing, response, and any permitted device action. A working Home Assistant interface, installed speech components, or an **Up** availability check is insufficient to mark that workflow complete. Integration with Hermes requires its own implementation and validation.

## Remaining Work

- Record protection and source-to-copy integrity checks for the application-backup copy.
- Perform a controlled application restoration and validate the recovered configuration and required integrations.
- Resolve and retest the recorded voice-configuration issues.
- Validate the intended voice workflow on each device before marking it operational.
- Test actionable failure and recovery notifications for the Home Assistant monitor.
- Define recurring backups, retention, capacity checks, and update procedures.
- Define and test any future remote Home Assistant access separately from Hermes host administration.
- Define permissions before connecting Hermes or additional automation services to household devices.

## Public Documentation Boundary

The public repository contains this deployment record, not the application configuration or backup. Keep account details, tokens, keys, certificates, device and entity identifiers, household information, internal addresses, and backup filenames or paths private. Screenshots and logs require sanitization before publication.

Related records:

- [Architecture](architecture.md)
- [Proxmox installation](proxmox-installation.md)
- [Hardware inventory](hardware-inventory.md)
- [Backup and recovery](backup-and-recovery.md)
- [Security and privacy](security-and-privacy.md)
