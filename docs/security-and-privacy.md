# Security and Privacy Policy

> **Last reviewed:** August 2026  
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
- Usernames and paths containing personal or account names
- Timestamps that reveal personal routines when they are not technically relevant
- Logs containing addresses, identifiers, query strings, tokens, or unrelated events
- Browser tabs, bookmarks, account avatars, notifications, and task-history panels
- File names or storage names that reveal private projects or personal information
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

A future repository-level `.gitignore` should exclude at least the relevant secret and local-state patterns used by the deployed services. Possible entries include:

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

This is an initial defensive list, not a complete policy for every future tool. Each new service must be reviewed for its own secret, state, database, and backup files before its directory is added to Git.

## Screenshot and Photograph Review

Before publishing an image, inspect the original file at full resolution and verify all of the following:

- [ ] No IP address, hostname, domain, URL, username, or email address is visible.
- [ ] No token, password, QR code, recovery code, or authentication prompt is visible.
- [ ] Browser tabs, bookmarks, notifications, account avatars, and unrelated windows are hidden or cropped out.
- [ ] Proxmox task logs, node names, storage names, and network details are sanitized.
- [ ] OPNsense interfaces, rules, certificates, gateways, and remote-access details are sanitized.
- [ ] Switch management addresses, device names, MAC tables, LLDP neighbors, and port labels are sanitized.
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
7. Verify that planned services are labelled **planned**, **pending**, or **not deployed**.
8. Check that example values are obviously fictional or use reserved documentation ranges.
9. Review the final diff for unexpected or unrelated content.
10. Publish only after all checks pass.

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

- The physical rack has been assembled and final cabling remains in progress.
- Proxmox VE is installed and its web interface has been reached successfully.
- An operating system ISO has been uploaded to Proxmox storage.
- No complete virtual machine has been deployed or booted.
- The dedicated firewall appliance and managed switch are available but not yet deployed in the final network path.
- OPNsense, managed-switch configuration, virtual machines, containers, monitoring, automation, and AI services remain pending or planned.

No document should imply that unfinished services are operational.

## Review Schedule

This policy should be reviewed:

- Before the first public release of the repository
- Whenever a new infrastructure service is documented
- Before publishing configuration files, logs, screenshots, or photographs
- After any security-relevant architectural change
- After any suspected disclosure or repository-security incident

The goal is to demonstrate practical infrastructure work while keeping the live HomeLab and its owner protected.
