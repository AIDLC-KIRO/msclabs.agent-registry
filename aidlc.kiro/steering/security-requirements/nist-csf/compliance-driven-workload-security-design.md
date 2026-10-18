---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Compliance Driven Workload Security Design

**Pack:** NIST CSF Pack  
**Description:** Workload architectures should reflect a clear understanding of the legal, regulatory, and contractual cybersecurity obligations applicable to the data they process and the services they provide. Applicable compliance regimes (such as HIPAA, PCI DSS, GDPR, FISMA, or sector-specific regulations) impose minimum security standards — including data protection, access control, audit logging, and breach notification — that should be translated into concrete architectural decisions. Contractual obligations from customers or supply chain partners may impose additional requirements beyond legal minimums and should similarly be incorporated into the workload's security design. Stakeholder and service dependencies should be understood so that compliance scope, impact boundaries, and recovery priorities are accurately reflected in the architecture.

## Domain / Applicability

Applies to any workload that processes regulated data, operates under sector-specific compliance requirements, or is subject to contractual security obligations from customers or supply chain partners. Particularly relevant during initial architecture design, major feature changes, and when onboarding new data types or integration partners.

## Evaluation Criteria

COMPLIANT: The architecture document identifies applicable legal, regulatory, and/or contractual compliance requirements and demonstrates how the workload's design addresses them (e.g., encryption at rest/in transit for PCI DSS or HIPAA, data residency controls for GDPR, audit logging for FISMA). The design accounts for stakeholder and service dependencies relevant to compliance scope and recovery prioritization. Alternative or compensating controls are acceptable when documented with rationale.

NON-COMPLIANT: The architecture document fails to identify applicable compliance obligations, or the design lacks controls that address known regulatory or contractual requirements without documented justification. The design does not reflect awareness of how compliance obligations shape security decisions for the data types or services involved.
