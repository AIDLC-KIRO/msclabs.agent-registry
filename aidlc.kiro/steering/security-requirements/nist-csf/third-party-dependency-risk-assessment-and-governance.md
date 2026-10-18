---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Third Party Dependency Risk Assessment And Governance

**Pack:** NIST CSF Pack  
**Description:** Workloads that depend on third-party suppliers, services, libraries, or components should identify and prioritize those dependencies by their criticality and risk exposure. Dependencies with access to sensitive data, deep system integration, or critical functional roles pose greater risk and warrant proportionate governance. The workload design is expected to establish cybersecurity expectations for high-criticality third parties — such as minimum security standards, incident notification obligations, and audit rights — and to support ongoing monitoring of supplier risk posture throughout the relationship lifecycle.

## Domain / Applicability

Applies to workloads that integrate third-party components, managed services, SaaS platforms, open-source libraries, APIs, or any external dependency that could introduce supply chain risk — particularly where those dependencies handle sensitive data or are deeply embedded in workload functionality.

## Evaluation Criteria

COMPLIANT: Design identifies third-party dependencies and classifies them by criticality (e.g., data access, integration depth, functional criticality); design documents cybersecurity expectations for high-criticality suppliers (security standards, incident notification, audit rights); design includes a mechanism for ongoing monitoring of supplier risk (e.g., periodic reassessment, vendor security scorecards, dependency vulnerability tracking); OR design provides documented rationale for a reduced-scope approach proportionate to the workload's risk profile.

NON-COMPLIANT: Design integrates third-party dependencies without any risk classification or prioritization; design lacks documented cybersecurity expectations for suppliers handling sensitive data or providing critical functions; design treats supplier risk as a one-time onboarding check with no ongoing monitoring mechanism; design fails to address how changes in supplier security posture (e.g., breaches, acquisitions) would be detected and responded to.
