# Security and Privacy Policy

> **Last reviewed:** September 2026  
> **Scope:** Public documentation for this personal HomeLab repository

This document defines the security and privacy rules used when publishing HomeLab documentation. Its purpose is to make the project useful as a technical portfolio without exposing credentials, personal information, access paths, or unnecessary details about the live environment.

This policy applies to every Markdown file, diagram, screenshot, configuration example, log excerpt, issue, commit, and release added to the public repository.

## Core Principles

1. Publish the technical reasoning, not the secrets or live identifiers.
2. Document verified work separately from planned work.
3. Share only the minimum information required to explain a design or result.
4. Replace real environment values with obvious placeholders or documentation-only examples.
5. Review content at full resolution before every public upload.
6. Treat Git history as public and persistent, even after a file is edited or deleted.

## Information Classification

| Classification | Examples | Public repository policy |
| --- | --- | --- |
| Public | Hardware models, software names, general architecture, completed milestones, high-level lessons learned | Allowed after review |
| Sanitized | Network diagrams, configuration fragments, logs, command output, dashboard images | Allowed only after replacing or removing live values |
| Private | Internal IP addresses, hostnames, VLAN IDs tied to the live design, usernames, Wi-Fi names, device labels, household layout details | Do not publish unless a future review determines that a specific value is necessary and safe |
| Secret | Passwords, API keys, tokens, private keys, recovery codes, cookies, certificates with private material, real `.env` files | Never publish |

When uncertain, information is treated as private until it has been reviewed.

## Information That Must Never Be Published

- Passwords, passphrases, PINs, recovery codes, or two-factor authentication secrets
- API keys, access tokens, session cookies, webhook secrets, or bot tokens
- SSH private keys, VPN private keys, certificate private material, or unredacted key stores
- Real `.env` files, credential stores, browser profiles, or password-manager exports
- Public IP addresses, dynamic DNS names, remote-access URLs, or port-forwarding endpoints
- Wi-Fi SSIDs, Wi-Fi passwords, router administration details, or ISP account information
- Unredacted firewall backups, hypervisor backups, database dumps, or service configuration exports
- Serial numbers, MAC addresses, QR codes, barcodes, activation codes, or device-registration identifiers
- Full names, addresses, telephone numbers, personal email addresses, invoices, or shipping labels
- Authentication screens, backup codes, password-reset links, or signed download URLs

## Information Requiring Sanitization

The following content may be technically useful, but it must be cleaned before publication:

- Internal IP addresses and subnets
- Hostnames, node names, internal domains, and local DNS records
- Interface names when they expose real device assignments
- VLAN identifiers and firewall aliases connected to the live environment
- Firewall-rule names, ordering, directions, source and destination mappings, ports, and logging details tied to the live environment
- Usernames and paths containing personal or account names
- Assistant memory files, user profiles, prompts, conversation exports, and tool histories
- Memory-write approval identifiers, pending-operation records, gateway request logs, and assistant tool-call payloads
- Timestamps that reveal personal routines when they are not technically relevant
- Logs containing addresses, identifiers, query strings, tokens, or unrelated events
- Browser tabs, bookmarks, account avatars, notifications, and task-history panels
- File names or storage names that reveal private projects or personal information
- Backup identifiers, filenames, timestamps, sizes, paths, destinations, checksums, encryption recipients, and recovery metadata
- Tailscale addresses, tailnet names, device names, node identifiers, tags, account details, and live access-policy values
- Tailscale authentication keys, node keys, API tokens, recovery material, and unredacted ACL or grants configuration
- Home Assistant device and entity identifiers, areas, household routines, presence data, companion-app registrations, integration settings, voice recordings, transcripts, and voice-session identifiers
- Home Assistant application backups, security material, archive listings, and recovery metadata
- Uptime Kuma monitor targets, dashboard addresses, notification recipients, webhook URLs, credentials, databases, and exported configuration
- Mobile SSH-client profiles, synchronized key stores, public keys, fingerprints, connection labels, and session history
- Photographs showing labels, screens, documents, reflections, windows, or identifying household details

Redaction must be permanent. Covering text with a movable shape in an editable document is not sufficient.

## Safe Documentation Values

Examples should use clearly fictional placeholders rather than values copied from the live system.

| Live value type | Safe public representation |
| --- | --- |
| IP address | `<INTERNAL_IP>` or an address from a documentation range such as `192.0.2.10` |
| Hostname | `<PROXMOX_HOST>` or `pve-example` |
| Domain | `example.com` or `home.example` |
| Username | `<ADMIN_USER>` |
| Password or token | `<REDACTED>` or `${SECRET_FROM_ENV}` |
| MAC address | `<MAC_ADDRESS>` |
| Public endpoint | `<REMOTE_ACCESS_ENDPOINT>` |
| Network name | `<NETWORK_NAME>` |
| Tailscale device or tailnet | `<PRIVATE_OVERLAY_DEVICE>` or `<PRIVATE_OVERLAY_NETWORK>` |
| Home Assistant entity or area | `<EXAMPLE_ENTITY>` or `<EXAMPLE_AREA>` |
| Monitor target or notification destination | `<MONITORED_SERVICE>` or `<NOTIFICATION_DESTINATION>` |

Documentation-only values must not be presented as recommended live credentials or copied into production without review.

## Configuration Files and Templates

Only sanitized examples and templates may be committed. Files that can contain secrets should have a public template and a private local counterpart.

Example:

```text
.env.example        # Public template with placeholders
.env                # Private local file; never committed
config.example.yml  # Public sanitized example
config.yml          # Private live configuration where applicable
```

The repository-level `.gitignore` excludes common secret and local-state patterns. Its current rules include entries such as:

```gitignore
.env
.env.*
!.env.example
*.key
*.pem
*.p12
*.pfx
*.ovpn
*.log
*.bak
*.backup
secrets/
private/
backups/
```

This is an initial defensive list, not a complete policy for every future tool. Each new service must be reviewed for its own secret, state, database, and backup files, and the `.gitignore` must be updated before that service's files are added to Git.

Hermes Agent configuration, provider credentials, persistent memory, user profiles, conversation data, and tool state are private operational data. Public documentation may describe their purpose and sanitized validation results, but it must not contain their live contents or storage locations.

Home Assistant configuration, application backups, integration credentials, security material, and household data are private. Uptime Kuma databases, monitor definitions, notification settings, and backups are also private. This documentation update does not authorize publishing those files or assume that the existing ignore rules cover every service-specific path.

## Screenshot and Photograph Review

Before publishing an image, inspect the original file at full resolution and verify all of the following:

- [ ] No IP address, hostname, domain, URL, username, or email address is visible.
- [ ] No token, password, QR code, recovery code, or authentication prompt is visible.
- [ ] Browser tabs, bookmarks, notifications, account avatars, and unrelated windows are hidden or cropped out.
- [ ] Proxmox task logs, node names, storage names, and network details are sanitized.
- [ ] OPNsense interfaces, aliases, rules, DNS records, certificates, gateways, and remote-access details are sanitized.
- [ ] Switch management addresses, device names, MAC tables, LLDP neighbors, and port labels are sanitized.
- [ ] Tailscale addresses, tailnet or device names, node details, account identity, authentication material, and access-policy configuration are hidden or sanitized.
- [ ] Hermes configuration, provider details, memory content, prompts, user profiles, tool output, and session history are hidden or sanitized.
- [ ] Home Assistant areas, entities, device registrations, household activity, voice data, integration credentials, and backup metadata are hidden or sanitized.
- [ ] Uptime Kuma targets, notification destinations, webhook URLs, dashboard links, and identifying event history are hidden or sanitized.
- [ ] Mobile SSH-client profiles, keys, fingerprints, synchronized-account details, and connection history are hidden or sanitized.
- [ ] Hardware serial numbers, asset labels, barcodes, and shipping labels are not readable.
- [ ] The background, reflections, and visible documents do not reveal personal or location information.
- [ ] Image metadata is removed when it is not required.
- [ ] The edited image has been exported as a new flattened file and checked again.

When a screenshot is not necessary to prove or explain a result, a written explanation or sanitized diagram is preferred.

## Pre-Publication Checklist

Run this review before every commit intended for the public repository:

1. Confirm that every technical claim matches the current verified state.
2. Check the staged files rather than relying only on the working-folder view.
3. Search for credentials, tokens, private keys, IP addresses, email addresses, and personal names.
4. Review new configuration files against the relevant service's secret-file conventions.
5. Inspect every image at full resolution.
6. Confirm that no backup, database, log, export, or temporary file has been included.
7. Confirm that backup names, paths, sizes, timestamps, hashes, encryption metadata, and storage destinations have not been disclosed.
8. Confirm that Tailscale addresses, device and tailnet identifiers, account data, authentication material, and live access-policy details have not been disclosed.
9. Verify that every service is labelled accurately as **operational**, **in progress**, **planned**, **pending**, or **not deployed**.
10. Check that example values are obviously fictional or use reserved documentation ranges.
11. Review the final diff for unexpected or unrelated content.
12. Publish only after all checks pass.

For Home Assistant, Hermes, Uptime Kuma, and remote-client updates, also verify that:

- Application availability is distinguished from working voice, assistant integration, and notification delivery.
- A single successful voice request is distinguished from reliable repeated operation, acceptable latency, second-device validation, and permissioned device control.
- VM-level, application-level, and configuration-only recovery copies are classified accurately; encryption and checksum results are attributed only to the copies actually checked.
- Memory loading is distinguished from approval-gated writes, and neither result is presented as complete RAG, authorization, or recovery validation.
- Backup coverage is mapped to the relevant service before it is claimed, and an archive inspection or checksum match is not presented as a successful restoration.
- Client enrollment is distinguished from external reachability and SSH authentication.
- A dedicated Tailscale container is not presented as proof of subnet routing, Exit Node operation, or complete access-policy validation.

## Repository Practices

- Keep the public repository separate from live configuration and backup locations.
- Commit small, understandable changes so that each diff can be reviewed properly.
- Do not use the public repository as a synchronization location for live secrets.
- Do not paste sensitive values into issues, pull requests, commit messages, or release notes.
- Use least-privilege credentials for any future automated workflow connected to the repository.
- Pin and review future third-party automation before granting it repository access.
- Enable repository security features such as secret scanning when available.
- Review dependencies and example configurations before using them in the live HomeLab.

## If Sensitive Information Is Exposed

Deleting a secret from the latest file is not enough because Git history, caches, forks, and logs may retain it.

If exposure is suspected:

1. Stop publishing further changes.
2. Revoke or rotate the affected credential immediately.
3. Disable the exposed endpoint or access path if applicable.
4. Determine which files, commits, issues, images, and logs contain the information.
5. Remove the sensitive data from the repository history using an appropriate history-rewrite process.
6. Review access and service logs for unexpected activity.
7. Replace affected credentials and verify the new configuration.
8. Record a private incident note without reproducing the secret.

Credential rotation is the priority; rewriting repository history does not make an exposed credential trustworthy again.

## Current Project Boundary

At the time of this review, the public documentation may state that:

- The physical foundation is completed, including equipment placement, cabling, private labeling, ventilation checks, power distribution, and connected-load review.
- Proxmox VE `9.2.11` is installed, updated, hardened, and reachable through its segmented administration path from an approved client role.
- An operating system ISO has been uploaded to Proxmox storage.
- OPNsense `26.7.2_2` is operational on the dedicated firewall appliance and provides routing, DHCP, DNS, VLAN gateways, and initial policy enforcement.
- The managed switch is running firmware `3.30.6`; private administration, traffic forwarding, and three role-based VLANs are operational.
- Required DNS access, approved Proxmox administration, and a selected cross-segment isolation path have been verified using sanitized role descriptions.
- The first Ubuntu Server `24.04.4 LTS` guest is installed, updated, and hardened for key-based administration.
- Docker Engine `29.7.2` and Docker Compose `5.5.0` are installed and validated on the first guest.
- Private name resolution and the approved network path are operational for the first service workload, while all live values remain private.
- Initial and final network-configuration copies are stored privately and are not part of the repository.
- Hermes Agent is operational through its initial text workflow. Persistent user-memory loading and a temporary approval-gated write-and-delete cycle have been verified.
- Tailscale provides externally tested private administration of the Hermes host without requiring a direct public inbound service. The selected travel laptop passed a mobile-hotspot test, and a selected tablet confirmed Termius host access through a phone hotspot.
- A further tablet has connected to Tailscale and had an SSH key prepared; its completed external SSH validation is not established in the current record.
- A dedicated Tailscale container is present in the workload inventory. Network-wide administration, subnet routing, Exit Node operation, and complete access-governance validation are outside the verified scope.
- Hermes credentials, live configuration, persistent-memory contents, approval records, user identities, session data, gateway logs, tool-call payloads, and backup material remain private.
- Initial encrypted VM and container backups have been copied to separate storage and verified through private SHA-256 comparison. The manual virtual-machine workflow was later repeated after further configuration changes, and the follow-up encrypted copy also passed private source-to-destination integrity comparison.
- The exact service scope of those earlier archives must be mapped before claiming coverage of current workloads or attributing the follow-up VM archive specifically to Hermes.
- Home Assistant runs in a separate VM with verified private name resolution and connected mobile companion apps.
- One Home Assistant Voice Preview Edition unit completed onboarding. One request returned the expected user-specific response through the configured Home Assistant-to-Hermes path in approximately ten seconds. Reliable repetition, acceptable latency, the second unit, and device control are not established.
- An encrypted VM-level Home Assistant recovery copy was exported to secondary storage. Source-to-copy integrity and controlled restoration are not established by the earlier VM and container results.
- A private Hermes configuration safety copy was created after the initial voice-path validation. It is not a complete, integrity-verified, or restoration-tested assistant backup.
- Uptime Kuma runs in a separate container with initial alerting configured. The saved Home Assistant monitor reported **Up**; this does not establish every notification path, complete monitoring coverage, or recoverability.
- Real backup IDs, filenames, paths, timestamps, sizes, hashes, encryption details, destinations, and local working archives remain private.
- Earlier initial and follow-up archive integrity checks are verified. Decryption testing, controlled restoration, recurring rotation, and source-to-copy integrity checks for the Home Assistant VM recovery copy remain pending.
- An initial local voice-to-Hermes conversational path is verified. Reliable operation, the second voice unit, device-control permissions, n8n, Prometheus, Grafana, expanded memory/RAG, multi-user profiles, and on-demand GPU integration remain in progress or planned.
- Remaining client tests, assistant-specific monitoring, per-monitor notification validation, and broader access-policy review remain in progress or pending.

No document should imply that unfinished services are operational.

## Review Schedule

This policy should be reviewed:

- Before the first public release of the repository
- Whenever a new infrastructure service is documented
- Before publishing configuration files, logs, screenshots, or photographs
- After any security-relevant architectural change
- After any suspected disclosure or repository-security incident

The goal is to demonstrate practical infrastructure work while keeping the live HomeLab and its owner protected.
