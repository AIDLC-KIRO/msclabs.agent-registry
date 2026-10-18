---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Workload Incident Recovery Architecture And Communication

**Pack:** NIST CSF Pack  
**Description:** Workloads should be designed with a documented incident recovery capability that enables timely, structured restoration of systems and services following a cybersecurity incident. This includes defining recovery procedures, prioritizing critical functions, verifying the integrity of backups and restoration assets before use, and confirming restored system integrity before returning to normal operations. Recovery design should also establish communication pathways so that designated internal and external stakeholders — including the public where applicable — receive timely, accurate, and approved updates on recovery progress. A well-architected recovery capability reduces downtime, prevents reintroduction of malware through compromised backups, and ensures that post-incident operational norms reflect cybersecurity risk considerations.

## Domain / Applicability

Applies to any workload that processes, stores, or transmits sensitive data or provides critical operational services — particularly where availability, data integrity, and stakeholder trust are security objectives. Relevant at architecture design time and during incident response planning.

## Evaluation Criteria

COMPLIANT: The design documents a recovery plan or runbook covering restoration sequencing, prioritization of critical functions, and criteria for declaring recovery complete. The design specifies mechanisms for verifying backup and restoration asset integrity before use (e.g., cryptographic checksums, hash validation, immutable backup storage, or equivalent integrity controls). The design identifies communication channels and stakeholder notification procedures for recovery status updates. Post-incident operational norms or re-entry criteria are defined.

NON-COMPLIANT: The design lacks documented recovery procedures or relies on ad-hoc restoration without defined sequencing or prioritization. The design does not address backup integrity verification, creating risk of restoring from corrupted or compromised assets. No stakeholder communication pathways are defined for recovery status. Critical mission functions are not considered in the recovery architecture.
