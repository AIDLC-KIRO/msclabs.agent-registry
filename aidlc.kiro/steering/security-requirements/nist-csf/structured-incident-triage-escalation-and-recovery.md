---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Structured Incident Triage Escalation And Recovery

**Pack:** NIST CSF Pack  
**Description:** Workloads should be supported by a structured incident response process that covers the full lifecycle from initial detection through to recovery. This includes pre-defined triage and validation steps to confirm genuine incidents before committing response resources, a categorization and prioritization scheme based on severity and potential impact, clear escalation paths that ensure high-severity incidents receive appropriate attention, and explicit criteria for initiating recovery only after containment and eradication are confirmed. Pre-establishing these elements — including coordination touchpoints with relevant third parties such as cloud providers, managed security services, or supply chain partners — reduces improvisation during an incident and limits the risk of premature recovery leading to reinfection or re-exploitation.

## Domain / Applicability

Incident response planning and operational readiness; applies to any workload that processes, stores, or transmits sensitive data or provides critical business functions, particularly during the design and operational planning phases.

## Evaluation Criteria

COMPLIANT: The architecture or operational design documents a structured incident response process that includes: (1) triage and validation steps to confirm incidents before full response engagement; (2) a categorization and prioritization model (e.g., severity tiers, impact classifications); (3) defined escalation paths with criteria for elevating incidents to senior stakeholders or third parties; (4) pre-defined recovery initiation criteria that require containment and eradication confirmation before recovery begins; and (5) identified third-party coordination contacts (cloud providers, MSSPs, supply chain partners) integrated into the plan. Alternative implementations are acceptable when the design demonstrates equivalent coverage of these lifecycle stages with documented rationale.

NON-COMPLIANT: The design lacks a defined incident response process for the workload, omits triage or categorization mechanisms, provides no escalation criteria, or fails to establish recovery initiation gates — without documented compensating controls or justification for the omission.
