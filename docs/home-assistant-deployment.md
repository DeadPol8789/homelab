# Home Assistant Deployment

> **Last documented:** September 2026  
> **Status:** Initial deployment operational; encrypted VM recovery copy exported; first voice-to-Hermes response verified

This document records the initial Home Assistant deployment. It separates application availability, recovery-copy handling, and voice validation so that progress in one area does not imply completion of the others.

Live guest identifiers, addresses, DNS records, device names, account data, backup metadata, and configuration exports are excluded.

## Deployment Summary

Home Assistant runs in its own virtual machine on the existing Proxmox host, separately from the Ubuntu guest that hosts Docker and Hermes Agent. Private name resolution has been verified, and Home Assistant companion apps on selected phone and tablet clients are connected.

Uptime Kuma provides an initial availability check. The Home Assistant monitor was saved and reported **Up**. Initial alerting exists in the monitoring platform, but this record does not establish a successful failure-and-recovery notification test for this specific monitor.

An encrypted VM-level Home Assistant recovery copy has been exported to secondary storage. Its source-to-copy integrity and controlled restoration have not yet been documented.

## Recorded Progress

| Area | Recorded result | Boundary |
| --- | --- | --- |
| Workload placement | Home Assistant operates in a separate Proxmox VM | Separate placement does not by itself prove network isolation or recoverability. |
| Private name resolution | Resolution for the application has been verified | Live DNS records and addresses remain private. |
| Mobile access | Companion apps on selected phone and tablet clients are connected | This does not establish external Home Assistant access from every mobile device. |
| Availability monitoring | The saved Home Assistant monitor reported **Up** in Uptime Kuma | This is the result of the configured check at that time, not proof that every integration works. |
| VM recovery copy | Encrypted backup exported to secondary storage | A source-to-copy integrity comparison and controlled restoration still need documented results. |
| Voice hardware | Two Home Assistant Voice Preview Edition devices are available; one completed onboarding | The second unit and repeated operation remain unverified in this record. |
| Hermes integration | **Initial request path verified** | One voice request returned the expected user-specific response through the configured Home Assistant-to-Hermes path in approximately ten seconds. This does not establish sustained reliability, acceptable latency, or assistant control of home devices. |

## Workload and Access Design

The separate Home Assistant VM keeps its application environment distinct from the existing assistant guest. Maintenance and recovery can therefore be planned for each service role. Resource assignments and live network settings are retained privately.

The verified mobile-app connections are recorded independently from the external Tailscale test to the Hermes host. That host-administration test must not be used as evidence of remote Home Assistant access or unrestricted access to the HomeLab.

Future device control and assistant integrations require defined permissions and explicit functional tests. No household device-control scope is claimed by this initial deployment record.

## VM Recovery Copy

The recorded sequence was:

1. Create a VM-level Home Assistant backup.
2. Protect the backup with private encryption material.
3. Export the encrypted recovery copy to secondary storage.

This recovery source covers the Home Assistant guest at the virtualization layer. It does not prove that the archive can be decrypted and restored successfully or that every application component and integration will work after recovery.

Earlier VM and container backups passed SHA-256 comparison steps. Those results apply to their respective archives and cannot establish transfer integrity for this Home Assistant copy. See [Backup and recovery](backup-and-recovery.md) for the separate scopes and remaining checks.

## Voice Configuration

One Home Assistant Voice Preview Edition unit completed local onboarding. After the earlier satellite-loading and speech-component issues were addressed sufficiently for testing, an initial request traversed the configured Home Assistant-to-Hermes path and returned the expected user-specific response in approximately ten seconds.

This single result verifies an initial input, processing, and response path. It does not establish repeated reliability, acceptable performance, validation of the second voice unit, or any permitted device action. A working Home Assistant interface, installed speech components, or an **Up** availability check remains insufficient on its own to mark the broader workflow complete.

## Remaining Work

- Record source-to-copy integrity checks for the encrypted VM recovery copy.
- Perform a controlled VM restoration and validate Home Assistant, speech components, and required integrations.
- Repeat the successful voice request and assess reliability and latency.
- Complete onboarding and validation for the second voice unit.
- Define and validate any permitted device actions separately from conversational responses.
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
