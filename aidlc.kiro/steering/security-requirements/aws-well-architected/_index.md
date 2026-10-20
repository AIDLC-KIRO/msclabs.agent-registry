---
inclusion: manual
---

# AWS Well-Architected Pack

This file is a navigation catalogue for security requirements derived from the AWS Well-Architected
Framework Security Pillar. Open and review the linked files before selecting requirements for a project.

| Field | Value |
| --- | --- |
| Pack ID | `srp-am-well-architected` |
| Requirements | 32 |
| Producer | AWS Security Agent (Agent Spaces, `ap-southeast-1`) |
| Framework version | Not documented in this repository |
| Control mapping and review status | Not documented in this repository |

> [!NOTE]
> Applying this pack does not by itself demonstrate Well-Architected review completion, security
> assurance, certification, or compliance. Validate the mapping and collect project evidence.

## Requirements

| # | Requirement |
| --- | --- |
| 1 | [authenticated-network-communication-architecture](authenticated-network-communication-architecture.md) |
| 2 | [automated-certificate-management-architecture](automated-certificate-management-architecture.md) |
| 3 | [automated-credential-governance-architecture](automated-credential-governance-architecture.md) |
| 4 | [automated-data-classification-architecture](automated-data-classification-architecture.md) |
| 5 | [automated-remediation-with-oversight-architecture](automated-remediation-with-oversight-architecture.md) |
| 6 | [automated-security-testing-architecture](automated-security-testing-architecture.md) |
| 7 | [automated-threat-intelligence-integration](automated-threat-intelligence-integration.md) |
| 8 | [automated-vulnerability-management-architecture](automated-vulnerability-management-architecture.md) |
| 9 | [automation-first-operational-access-architecture](automation-first-operational-access-architecture.md) |
| 10 | [code-review-process-architecture](code-review-process-architecture.md) |
| 11 | [compliance-framework-control-mapping](compliance-framework-control-mapping.md) |
| 12 | [comprehensive-security-logging-architecture](comprehensive-security-logging-architecture.md) |
| 13 | [controlled-cross-account-access-architecture](controlled-cross-account-access-architecture.md) |
| 14 | [data-at-rest-access-control-architecture](data-at-rest-access-control-architecture.md) |
| 15 | [data-classification-and-tagging-architecture](data-classification-and-tagging-architecture.md) |
| 16 | [data-lifecycle-management-architecture](data-lifecycle-management-architecture.md) |
| 17 | [encryption-at-rest-enforcement-architecture](encryption-at-rest-enforcement-architecture.md) |
| 18 | [encryption-in-transit-enforcement-architecture](encryption-in-transit-enforcement-architecture.md) |
| 19 | [fine-grained-traffic-flow-control-architecture](fine-grained-traffic-flow-control-architecture.md) |
| 20 | [incident-management-plan-architecture](incident-management-plan-architecture.md) |
| 21 | [layered-network-segmentation-architecture](layered-network-segmentation-architecture.md) |
| 22 | [least-privilege-permission-architecture](least-privilege-permission-architecture.md) |
| 23 | [secrets-management-architecture](secrets-management-architecture.md) |
| 24 | [secure-key-management-architecture](secure-key-management-architecture.md) |
| 25 | [secure-third-party-access-architecture](secure-third-party-access-architecture.md) |
| 26 | [security-design-principles-integration](security-design-principles-integration.md) |
| 27 | [sensitivity-based-data-protection-architecture](sensitivity-based-data-protection-architecture.md) |
| 28 | [shared-responsibility-model-documentation](shared-responsibility-model-documentation.md) |
| 29 | [software-integrity-validation-architecture](software-integrity-validation-architecture.md) |
| 30 | [systematic-threat-modeling-in-design](systematic-threat-modeling-in-design.md) |
| 31 | [temporary-credentials-architecture](temporary-credentials-architecture.md) |
| 32 | [traffic-inspection-architecture](traffic-inspection-architecture.md) |

The index itself uses `manual` inclusion. Each linked requirement currently uses `fileMatch` with
`fileMatchPattern: "**/*"`; once copied, it can apply whenever any file is in context.
