# Tailscale Remote Access

> **Last verified:** September 2026  
> **Project status:** Private host access externally tested on the travel laptop; mobile-client rollout in progress

This document records the initial remote-access deployment and subsequent client rollout for the HomeLab. Tailscale provides a private encrypted path to the Linux host running Hermes Agent. The selected travel laptop has passed a real external-network test through a mobile hotspot, and selected mobile clients are being prepared and validated.

The document intentionally omits device names, account identities, addresses, DNS names, authentication data, keys, access-policy details, and screenshots of the live tailnet.

## Deployment Summary

Tailscale is installed and connected on the Hermes Linux host and approved client devices. The original external host-access test has been followed by a successful mobile-hotspot test from the selected travel laptop.

A tablet client has also been used to access the Hermes host through Termius while connected through a phone hotspot. A further tablet has been connected to Tailscale and an ED25519 SSH key prepared. A completed external SSH test for that further tablet is not established in this record.

A dedicated Tailscale container is present on the Proxmox host. Its presence does not establish that advertised routes, subnet access, or Exit Node operation are configured and verified. Those capabilities require separate evidence.

Remote administration continues to use the guest's existing hardened OpenSSH configuration. Tailscale provides the network path; SSH still requires the approved encrypted key. Password-based SSH authentication and direct root login remain disabled.

The external test confirmed that the approved client could establish the private path and connect to the Hermes host after leaving the home network. No router port forwarding or directly exposed public SSH endpoint was required.

## Verified Progress

| Stage | Status | Verified result |
| --- | --- | --- |
| Hermes host enrollment | **Completed** | The Linux service host is connected to the private Tailscale network. |
| Initial client enrollment | **Completed** | The original approved client is connected and can use the private path. |
| Device identification | **Reviewed** | The participating device entry was given a recognizable private label and checked in the administration view. |
| Private reachability | **Verified** | The approved client can reach the Hermes host through Tailscale. |
| SSH authentication | **Verified** | The existing encrypted SSH key works through the private overlay; password login and direct root login remain disabled. |
| External-network test | **Completed** | Access was tested successfully while the client was outside the local home network. |
| Public port exposure | **Not required** | The verified path does not depend on publishing the SSH service through router port forwarding. |
| Travel laptop | **Externally tested** | The selected laptop successfully accessed the Hermes host through a mobile hotspot. |
| Selected mobile tablet | **Host access confirmed** | Termius access to the Hermes host was confirmed while the tablet used a phone hotspot. |
| Further tablet enrollment | **In progress** | Tailscale connection and SSH-key preparation are recorded; final external SSH validation is not established here. |
| Dedicated Tailscale container | **Present** | A separate container appears in the workload inventory. Its routing functions are not established by that fact alone. |
| Exit Node and subnet routing | **Outside verified scope** | General internet egress through the HomeLab and broad access to internal subnets are not verified in this record. |
| Access-policy refinement | **Pending** | Device lifecycle, least-privilege policy, recovery, and future user separation still require review. |

## Current Access Path

| Layer | Recorded role |
| --- | --- |
| Approved client | Starts the private connection from an external network. |
| Tailscale overlay | Provides network reachability to the Hermes host. |
| OpenSSH on the host | Authenticates the approved key for the permitted account. |
| Host session | Provides terminal administration; a dedicated remote assistant interface remains separate work. |

Client enrollment, successful network reachability, and successful SSH authentication are separate milestones. Each intended client requires its own validation.

## Security Boundary

The tested host-access path uses these controls:

- Participating clients are explicitly enrolled; the complete authorization policy still requires review.
- Tailscale provides an encrypted private overlay rather than a directly exposed inbound router port.
- SSH retains independent key-based authentication.
- The SSH private key remains encrypted and outside the public repository.
- Password-based SSH authentication is disabled.
- Direct root login is disabled.
- Live device identities, addresses, account information, and policy details remain private.

The tests establish access to the Hermes host. They do not establish that every other destination is blocked, nor do they verify remote administration of Proxmox, OPNsense, the managed switch, or all internal networks. Home Assistant companion-app connectivity is documented separately and must not be treated as proof of external Home Assistant access.

## External Validation

The initial validation followed this sequence:

1. Confirm local SSH access before changing the remote path.
2. Connect the Hermes host to Tailscale.
3. Connect and identify the approved client.
4. Confirm private overlay reachability.
5. Leave the local home network.
6. Reconnect to the Hermes host through Tailscale.
7. Confirm that the existing SSH key is still required and accepted.
8. Confirm that Hermes remains reachable through the validated host.

Passing this test establishes a working external path. It does not replace periodic device review, recovery testing, monitoring, or testing from every device intended for travel.

### Subsequent Client Results

The travel laptop completed a real access test through a mobile hotspot. A selected tablet also reached the Hermes host in Termius through a phone hotspot. These results extend the recorded client coverage beyond the original test.

The further tablet's Tailscale connection and SSH-key preparation are recorded as setup progress. Final external SSH access remains to be documented. Private keys, public keys, fingerprints, account names, device labels, and session output are excluded.

## Remaining Work

- Complete and document external SSH validation for the remaining selected clients.
- Recheck the validated travel-laptop path after material client or access-policy changes.
- Record which clients have passed enrollment, external reachability, and SSH authentication checks.
- Review least-privilege access controls and device approval rules.
- Define device removal, key rotation, lost-device, and account-recovery procedures.
- Add monitoring for unexpected disconnection or loss of remote reachability.
- Decide separately whether subnet routing or an Exit Node is needed.
- Define restricted identities and service-only permissions before granting family access.

## Information Intentionally Omitted

This public document does not include:

- Tailscale or local IP addresses.
- Tailnet, machine, host, account, or user names.
- Device identifiers, node keys, authentication keys, tags, or key-expiration values.
- SSH usernames, public keys, private keys, fingerprints, aliases, or local configuration paths.
- Access-control policy, grants, groups, routes, DNS configuration, or administrative screenshots.
- Public endpoints, connection logs, session history, or location information.

These boundaries demonstrate a tested remote-access design without disclosing the live access path.
