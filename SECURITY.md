# Security Policy

This repository documents a personal HomeLab for learning and portfolio purposes. It contains sanitized documentation and may later include example configurations or scripts. It is not intended to expose or provide access to the live environment.

## Supported Content

Security reports are accepted for content currently present on the default branch, including:

- Scripts and automation published in this repository
- Example configuration files
- Documentation that accidentally exposes sensitive information
- Repository workflows or dependencies
- Instructions that could create a significant security risk if followed as written

Older revisions and planned components are not actively supported. However, suspected credential exposure in Git history should still be reported privately.

## Reporting a Vulnerability

Please do **not** disclose a vulnerability, secret, personal detail, or live infrastructure identifier in a public issue, discussion, pull request, commit, or comment.

Use the repository's private vulnerability reporting option if it is available under the **Security** section.

If private reporting is not available, open a minimal public issue titled `Private security contact requested`. Include only the affected repository area and a request for a private communication channel. Do not include technical details that would reveal the vulnerability.

When a private channel has been established, provide:

- A clear description of the issue
- The affected file, script, workflow, or documentation section
- Reproduction steps using safe, non-production examples
- The potential impact
- A suggested mitigation, if known

Do not include passwords, API keys, tokens, private keys, real IP addresses, internal hostnames, personal information, or copies of live configuration files.

## Responsible Testing

This policy does not authorize testing against the live HomeLab, personal devices, accounts, network endpoints, or third-party services.

Please do not:

- Attempt to discover or access private infrastructure
- Scan, probe, exploit, disrupt, or modify any live system
- Perform social engineering or contact unrelated people
- Access, retain, or distribute personal data or credentials
- Publish vulnerability details before the issue has been reviewed and addressed

Testing should be limited to the public repository content and to environments you own or are explicitly authorized to test.

## Response and Disclosure

This is a personal learning project and does not provide a guaranteed response time or service-level agreement. Reports will be reviewed when reasonably possible.

If a report is valid, the maintainer will aim to:

1. Confirm the affected repository content.
2. Remove or correct the unsafe material.
3. Rotate any exposed credential or identifier when applicable.
4. Review Git history and related artifacts for further exposure.
5. Publish a sanitized explanation after remediation when doing so is safe and useful.

Public disclosure should wait until remediation is complete and should never reproduce secrets, personal data, or details that unnecessarily expose the live environment.

## Security and Privacy Documentation

The repository's publication rules, sanitization requirements, screenshot checklist, and incident-response guidance are documented in [`docs/security-and-privacy.md`](docs/security-and-privacy.md).

Thank you for helping keep this project and its owner safe.
