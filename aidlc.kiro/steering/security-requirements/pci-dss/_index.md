---
inclusion: manual
---

# PCI DSS Pack

This file is a navigation catalogue for security requirements derived from PCI DSS v4.0.1. Open and
review the linked files before selecting requirements for a project.

| Field | Value |
| --- | --- |
| Pack ID | `srp-am-pci-dss` |
| Requirements | 50 |
| Producer | AWS Security Agent (Agent Spaces, `ap-southeast-1`) |
| Framework version | PCI DSS v4.0.1 |
| Control mapping and review status | Not documented in this repository |

> [!NOTE]
> Applying this pack does not by itself establish PCI DSS scope, validation, certification, or
> compliance. Confirm scope and mapping with the responsible security and compliance owners and
> collect project evidence.

## Requirements

| # | Requirement |
| --- | --- |
| 1 | [account-data-classification-and-retention-controls](account-data-classification-and-retention-controls.md) |
| 2 | [anti-malware-protection-for-workload-components](anti-malware-protection-for-workload-components.md) |
| 3 | [anti-phishing-controls-for-workload-communications](anti-phishing-controls-for-workload-communications.md) |
| 4 | [application-and-system-account-security-management](application-and-system-account-security-management.md) |
| 5 | [audit-log-protection-integrity-and-retention](audit-log-protection-integrity-and-retention.md) |
| 6 | [automated-audit-log-review-and-anomaly-detection](automated-audit-log-review-and-anomaly-detection.md) |
| 7 | [cardholder-data-encryption-scope-isolation](cardholder-data-encryption-scope-isolation.md) |
| 8 | [cde-network-segmentation-and-scope-minimization](cde-network-segmentation-and-scope-minimization.md) |
| 9 | [cde-network-segmentation-and-traffic-control](cde-network-segmentation-and-traffic-control.md) |
| 10 | [cde-scope-documentation-and-data-flow-validation](cde-scope-documentation-and-data-flow-validation.md) |
| 11 | [comprehensive-audit-logging-for-sensitive-data-access](comprehensive-audit-logging-for-sensitive-data-access.md) |
| 12 | [continuous-security-control-monitoring-and-failure-response](continuous-security-control-monitoring-and-failure-response.md) |
| 13 | [cryptographic-agility-and-technology-lifecycle-risk](cryptographic-agility-and-technology-lifecycle-risk.md) |
| 14 | [cryptographic-key-management-for-stored-account-data](cryptographic-key-management-for-stored-account-data.md) |
| 15 | [documented-security-control-rationale-and-objectives](documented-security-control-rationale-and-objectives.md) |
| 16 | [incident-response-and-recovery-workflow](incident-response-and-recovery-workflow.md) |
| 17 | [intrusion-detection-file-integrity-and-page-tamper](intrusion-detection-file-integrity-and-page-tamper.md) |
| 18 | [least-privilege-access-control-with-default-deny](least-privilege-access-control-with-default-deny.md) |
| 19 | [mfa-for-cardholder-data-environment-access](mfa-for-cardholder-data-environment-access.md) |
| 20 | [multi-tenant-isolation-and-per-tenant-security](multi-tenant-isolation-and-per-tenant-security.md) |
| 21 | [network-architecture-and-data-flow-documentation](network-architecture-and-data-flow-documentation.md) |
| 22 | [network-config-security-and-internal-address-protection](network-config-security-and-internal-address-protection.md) |
| 23 | [network-security-controls-for-traffic-segmentation](network-security-controls-for-traffic-segmentation.md) |
| 24 | [pan-display-masking-and-storage-protection](pan-display-masking-and-storage-protection.md) |
| 25 | [pci-dss-scope-documentation-and-change-impact-assessment](pci-dss-scope-documentation-and-change-impact-assessment.md) |
| 26 | [penetration-testing-readiness-and-remediation](penetration-testing-readiness-and-remediation.md) |
| 27 | [poi-device-inventory-and-integrity-management](poi-device-inventory-and-integrity-management.md) |
| 28 | [programmatic-access-control-for-cardholder-data-stores](programmatic-access-control-for-cardholder-data-stores.md) |
| 29 | [protection-of-security-posture-artifacts](protection-of-security-posture-artifacts.md) |
| 30 | [public-facing-web-application-attack-protection](public-facing-web-application-attack-protection.md) |
| 31 | [regular-vulnerability-scanning-and-remediation](regular-vulnerability-scanning-and-remediation.md) |
| 32 | [sad-non-retention-after-authorization](sad-non-retention-after-authorization.md) |
| 33 | [scheduled-security-activities-and-change-triggered-reviews](scheduled-security-activities-and-change-triggered-reviews.md) |
| 34 | [secure-change-management-and-environment-separation](secure-change-management-and-environment-separation.md) |
| 35 | [secure-configuration-and-system-hardening](secure-configuration-and-system-hardening.md) |
| 36 | [secure-data-channel-scoping-and-unintended-data-handling](secure-data-channel-scoping-and-unintended-data-handling.md) |
| 37 | [secure-data-lifecycle-and-media-destruction](secure-data-lifecycle-and-media-destruction.md) |
| 38 | [secure-development-lifecycle-and-vulnerability-prevention](secure-development-lifecycle-and-vulnerability-prevention.md) |
| 39 | [secure-payment-software-lifecycle-and-configuration](secure-payment-software-lifecycle-and-configuration.md) |
| 40 | [secure-wireless-network-configuration-for-cde](secure-wireless-network-configuration-for-cde.md) |
| 41 | [session-idle-timeout-and-re-authentication](session-idle-timeout-and-re-authentication.md) |
| 42 | [stored-account-data-protection-and-retention](stored-account-data-protection-and-retention.md) |
| 43 | [strong-authentication-and-credential-management](strong-authentication-and-credential-management.md) |
| 44 | [strong-cryptography-for-cardholder-data-in-transit](strong-cryptography-for-cardholder-data-in-transit.md) |
| 45 | [strong-cryptography-for-pos-poi-terminal-connections](strong-cryptography-for-pos-poi-terminal-connections.md) |
| 46 | [third-party-service-provider-security-accountability](third-party-service-provider-security-accountability.md) |
| 47 | [time-synchronization](time-synchronization.md) |
| 48 | [unauthorized-network-access-path-detection](unauthorized-network-access-path-detection.md) |
| 49 | [unique-user-identification-and-account-lifecycle](unique-user-identification-and-account-lifecycle.md) |
| 50 | [vulnerability-identification-and-patch-management](vulnerability-identification-and-patch-management.md) |

The index itself uses `manual` inclusion. Each linked requirement currently uses `fileMatch` with
`fileMatchPattern: "**/*"`; once copied, it can apply whenever any file is in context.
