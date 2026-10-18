---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Forensic Readiness And Evidence Integrity For Workloads

**Pack:** NIST CSF Pack  
**Description:** Workloads should be designed to support forensic investigation by producing comprehensive, tamper-evident audit trails and operational telemetry. This includes capturing sufficient event data (actions, actors, timestamps, and context) to enable root cause analysis, preserving the integrity and provenance of that data so findings are reliable and legally admissible, and generating enough telemetry to estimate the magnitude and scope of an incident. Evidence integrity techniques — such as write-once or append-only log storage, cryptographic hashing, and chain-of-custody controls — are recommended to ensure investigation records cannot be altered after the fact.

## Domain / Applicability

Applies to any workload that processes sensitive data, performs privileged operations, or is subject to regulatory or legal obligations — particularly during incident response, forensic investigation, and post-incident recovery phases.

## Evaluation Criteria

COMPLIANT: Design specifies mechanisms for capturing comprehensive, structured audit logs (API calls, authentication events, data access, configuration changes) AND describes how log integrity is protected (e.g., write-once/append-only storage, log signing, cryptographic hashing, or immutable log destinations) AND demonstrates that telemetry is sufficient to support root cause analysis and incident scoping. Alternative integrity approaches are acceptable when documented with rationale.

NON-COMPLIANT: Design lacks tamper-evident log storage without documented justification, fails to capture sufficient event context for forensic reconstruction, or provides no mechanism to estimate incident scope from workload telemetry.
