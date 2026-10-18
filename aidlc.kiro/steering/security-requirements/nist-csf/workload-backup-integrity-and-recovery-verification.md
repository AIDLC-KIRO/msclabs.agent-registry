---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Workload Backup Integrity And Recovery Verification

**Pack:** NIST CSF Pack  
**Description:** Workloads should implement a backup strategy that addresses the full lifecycle of data protection and recovery: creation, protection, maintenance, testing, and integrity verification. Backups are expected to be created at a frequency aligned with the workload's recovery point objective (RPO), protected against unauthorized access and ransomware-style tampering (e.g., through immutability or write-once storage), and periodically tested to confirm restorability. Before any backup is used for restoration, its integrity should be verified to ensure it has not been corrupted, tampered with, or infected with malware. After restoration, the recovered assets should be validated for correctness and cleanliness before being returned to production, preventing premature declaration of recovery completion when threats may still be present.

## Domain / Applicability

Applies to any workload that manages stateful data — including databases, file systems, object stores, configuration state, and application secrets — particularly workloads with defined RTO/RPO requirements or those handling sensitive, regulated, or business-critical data.

## Evaluation Criteria

COMPLIANT: Design specifies a backup strategy that addresses all of the following — (1) backup frequency aligned with RPO, (2) protection of backups from unauthorized modification or deletion (e.g., immutable storage, cross-account/cross-region isolation, access controls), (3) a defined process for periodically testing backup restorability, (4) integrity verification of backups prior to use in restoration, and (5) post-restoration validation before returning systems to production. Alternative implementations are acceptable when the design documents the rationale and demonstrates equivalent protection against data loss and recovery failure.

NON-COMPLIANT: Design lacks a defined backup strategy, does not address backup protection against tampering or ransomware, omits integrity verification before restoration, or fails to include post-restoration validation — without documented justification or compensating controls.
