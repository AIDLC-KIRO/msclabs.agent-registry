---
inclusion: manual
---

# ASA Base Pack

This file is a navigation catalogue. Open and review the linked requirement files before copying
any of them into a project.

| Field | Value |
| --- | --- |
| Pack ID | `srp-am-base` |
| Purpose | Default security requirements produced by AWS Security Agent |
| Requirements | 10 |
| Producer | AWS Security Agent (Agent Spaces, `ap-southeast-1`) |
| Authoritative source and mapping | Not documented in this repository |

> [!NOTE]
> Applying this pack does not by itself establish security assurance, certification, or compliance.
> Each project must assess applicability and collect its own implementation evidence.

## Requirements

| # | Requirement | Purpose |
| --- | --- | --- |
| 1 | [audit-logging-best-practices](audit-logging-best-practices.md) | Support security monitoring through appropriate audit logging |
| 2 | [authentication-best-practices](authentication-best-practices.md) | Allow only legitimate users to authenticate |
| 3 | [authorization-best-practices](authorization-best-practices.md) | Apply appropriate authorization controls |
| 4 | [information-protection-best-practices](information-protection-best-practices.md) | Protect sensitive information from disclosure or unauthorized change |
| 5 | [log-protection-best-practices](log-protection-best-practices.md) | Protect log confidentiality and integrity |
| 6 | [privileged-access-best-practices](privileged-access-best-practices.md) | Add safeguards for privileged functions |
| 7 | [secret-protection-best-practices](secret-protection-best-practices.md) | Keep credentials and other secrets confidential |
| 8 | [secure-by-default-best-practices](secure-by-default-best-practices.md) | Use secure default configuration |
| 9 | [tenant-isolation-best-practices](tenant-isolation-best-practices.md) | Separate tenants appropriately |
| 10 | [trusted-cryptography-best-practices](trusted-cryptography-best-practices.md) | Use trustworthy cryptographic implementations |

The index itself uses `manual` inclusion. Each linked requirement currently uses `fileMatch` with
`fileMatchPattern: "**/*"`; once copied, it can apply whenever any file is in context.
