# Home Assistant Deployment

> **Last documented:** September 2026  
> **Status:** Home Assistant Core `2026.9.1` operational on Home Assistant OS `18.2`; two-unit voice-to-Hermes conversation path verified

This document records the initial Home Assistant deployment. It separates application availability, recovery-copy handling, and voice validation so that progress in one area does not imply completion of the others.

Live guest identifiers, addresses, DNS records, device names, account data, backup metadata, and configuration exports are excluded.

## Deployment Summary

Home Assistant runs in its own virtual machine on the existing Proxmox host, separately from the Ubuntu guest that hosts Docker and Hermes Agent. Private name resolution has been verified, and Home Assistant companion apps on selected phone and tablet clients are connected.

Uptime Kuma provides an initial availability check. The Home Assistant monitor was saved and reported **Up**. Initial alerting exists in the monitoring platform, but this record does not establish a successful failure-and-recovery notification test for this specific monitor.

An earlier encrypted VM-level Home Assistant recovery copy was exported to secondary storage. After the A2A voice integration became stable, a protected compressed Proxmox snapshot of the Home Assistant guest completed successfully. A separate encrypted local Home Assistant application backup includes configuration and the installed voice applications. Controlled restoration has not yet been documented.

## Recorded Progress

| Area | Recorded result | Boundary |
| --- | --- | --- |
| Workload placement | Home Assistant operates in a separate Proxmox VM | Separate placement does not by itself prove network isolation or recoverability. |
| Private name resolution | Resolution for the application has been verified | Live DNS records and addresses remain private. |
| Mobile access | Companion apps on selected phone and tablet clients are connected | This does not establish external Home Assistant access from every mobile device. |
| Availability monitoring | The saved Home Assistant monitor reported **Up** in Uptime Kuma | This is the result of the configured check at that time, not proof that every integration works. |
| Recovery sources | Earlier encrypted VM recovery copy, protected stable-state snapshot, and encrypted application backup | Controlled restoration and recovered-service validation still need documented results. |
| Voice hardware | Two Home Assistant Voice Preview Edition devices onboarded and tested | Both returned the expected persistent-memory response through the same configured assistant pipeline. |
| Speech services | **Operational for the Spanish pipeline** | Whisper `3.5.3` provides speech-to-text and Piper `2.3.4` provides text-to-speech. Speech-to-Phrase `1.4.5` is installed but is not the active transcription engine for this pipeline. |
| Hermes integration | **Authenticated A2A path verified** | The custom conversation connector returned Hermes responses in text and through both voice endpoints. Approved device control remains separate and unverified. |

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

## Voice and Conversation Configuration

Both Home Assistant Voice Preview Edition units completed local onboarding. The Spanish Assist pipeline uses the Hermes custom conversation agent, Whisper for speech-to-text, and Piper for text-to-speech. Local-command preference is enabled, allowing Home Assistant to handle supported commands before forwarding other requests to Hermes.

The Home Assistant connector communicates with Hermes as an authenticated A2A peer. Its response parser supports a returned task wrapper, artifacts, task-status messages, and direct messages. This corrected an earlier case in which the assistant answer existed inside the A2A result but was not extracted for Home Assistant.

Both voice endpoints returned the expected user-specific response from Hermes persistent memory in approximately ten seconds. A simple text conversation completed in approximately four to five seconds. A natural-language Home Assistant state query also succeeded; a literal technical identifier had first been mis-transcribed, demonstrating why spoken requests should prefer natural entity names. One duplicate wake-up event was observed and cancelled without evidence of a persistent fault.

These results verify the conversational path and both endpoints. They do not establish approved household-device actions, complete reliability, or continuous full-path monitoring.

## Remaining Work

- Record source-to-copy integrity checks for the encrypted VM recovery copy.
- Perform a controlled VM restoration and validate Home Assistant, speech components, and required integrations.
- Monitor repeated voice requests and continue latency and reliability assessment.
- Define and validate any permitted device actions separately from conversational responses.
- Test actionable failure and recovery notifications for the Home Assistant monitor.
- Test the protected VM snapshot and application backup through controlled restoration, then define recurring retention and capacity checks.
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
