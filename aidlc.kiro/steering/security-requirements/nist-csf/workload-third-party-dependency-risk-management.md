---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Workload Third Party Dependency Risk Management

**Pack:** NIST CSF Pack  
**Description:** Workloads that depend on external suppliers, third-party services, open-source components, or managed integrations should identify and assess the cybersecurity risks those dependencies introduce. The architecture is expected to maintain awareness of its supply chain — including software libraries, APIs, SaaS platforms, and cloud service dependencies — and apply risk-proportionate controls based on each dependency's criticality to the workload. This reduces the risk of supply chain compromise propagating into the workload through unvetted or unmonitored third-party components.

## Domain / Applicability

Applies to any workload that consumes third-party software components (open-source libraries, commercial SDKs, package registries), external APIs, SaaS integrations, managed services, or outsourced processing — particularly during architecture design, vendor selection, and ongoing operational review.

## Evaluation Criteria

COMPLIANT: The design identifies the workload's key third-party dependencies and classifies them by criticality; the architecture addresses how risks from those dependencies are assessed prior to adoption (e.g., due diligence, security questionnaires, SBOMs, or equivalent vetting); the design includes mechanisms for ongoing monitoring of dependency health (e.g., vulnerability feeds, dependency scanning tools, or vendor security advisories); and the architecture accounts for third-party involvement in incident response or dependency offboarding/end-of-life scenarios. Alternative approaches to any of these are acceptable when documented with rationale.

NON-COMPLIANT: The design introduces third-party dependencies without any documented risk assessment or classification; the architecture lacks any mechanism for detecting or responding to supply chain compromise in consumed components; or the design fails to address what happens when a critical third-party dependency is compromised, deprecated, or discontinued.
