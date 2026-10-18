---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Workload Data Lifecycle Cia Protection

**Pack:** NIST CSF Pack  
**Description:** Workloads should protect the confidentiality, integrity, and availability of all data they manage across the full data lifecycle — at rest, in transit, in use, and through backup and recovery. This encompasses sensitive personal information, operational data, and intellectual property. Failure to address these protections can result in unauthorized disclosure, data tampering, service disruption, regulatory violations, and harm to individuals (e.g., identity theft, discrimination, or financial loss). Data security decisions should be consistent with the workload's risk classification and the sensitivity of the data it processes.

## Domain / Applicability

Applies to any workload that stores, transmits, processes, or backs up data — particularly workloads handling sensitive personal information, regulated data, or business-critical operational data.

## Evaluation Criteria

COMPLIANT: Design demonstrates protection of data across all applicable lifecycle stages:
- Data-at-rest: encryption or equivalent confidentiality/integrity controls are applied to persistent stores (databases, object storage, file systems, snapshots).
- Data-in-transit: encrypted transport channels (e.g., TLS, mTLS, or equivalent) are used for all data flows between services, clients, and external systems.
- Data-in-use: where applicable (e.g., sensitive computation), protections such as memory isolation, confidential computing, or access controls are considered.
- Backup and recovery: backups are created, protected (encrypted, access-controlled), and periodically tested for restorability.
- Design provides documented rationale for any lifecycle stage where full protection is not applied, with compensating controls identified.

NON-COMPLIANT: Design lacks protection for one or more data lifecycle stages without documented justification; backup and recovery capabilities are absent or untested; no consideration of data sensitivity in architectural decisions.
