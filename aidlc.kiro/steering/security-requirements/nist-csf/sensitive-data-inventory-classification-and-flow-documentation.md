---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Sensitive Data Inventory Classification And Flow Documentation

**Pack:** NIST CSF Pack  
**Description:** Workloads that process, store, or transmit sensitive data should maintain clear, current documentation of what sensitive data they hold, where it resides, how it is classified, and how it flows across workload boundaries. This includes a data inventory identifying sensitive data types and their storage locations, a data classification scheme that informs access controls and protective measures, and network/data flow diagrams depicting authorized internal and external communication paths. This visibility is foundational to effective data protection: without knowing what sensitive data exists and where it flows, workloads cannot apply proportionate controls, detect unauthorized data movement, or satisfy regulatory documentation obligations (e.g., GDPR Article 30 records of processing, PCI DSS data flow requirements).

## Domain / Applicability

Applies to workloads that process, store, or transmit sensitive, regulated, personal, or classified data — including those subject to compliance frameworks such as GDPR, HIPAA, PCI DSS, or equivalent. Also applies to workloads with non-trivial network communication patterns or external data-sharing relationships where unauthorized data flows represent a meaningful risk.

## Evaluation Criteria

COMPLIANT: The architecture document includes: (1) a data inventory or data classification map identifying sensitive data types, their storage locations, classification levels, and access patterns; (2) network or data flow diagrams depicting authorized internal and external communication paths, including data crossing trust boundaries or leaving the workload environment; and (3) documentation of how sensitive data is handled at end-of-life (e.g., deletion, anonymization, or retention policies for decommissioned data stores). Alternative documentation formats are acceptable when they address the same data visibility objectives. Workloads with no sensitive data in scope may document this determination with rationale in lieu of a full data inventory.

NON-COMPLIANT: The design lacks documentation of sensitive data assets or their classification, omits network/data flow representations for data crossing trust boundaries, or fails to address how sensitive data is handled when components are decommissioned — without compensating controls or documented rationale.
