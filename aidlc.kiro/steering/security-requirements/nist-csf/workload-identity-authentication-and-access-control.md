---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Workload Identity Authentication And Access Control

**Pack:** NIST CSF Pack  
**Description:** Workloads should define and enforce a comprehensive identity and access control strategy that limits access to logical assets — including APIs, data stores, compute resources, and services — to authorized users, services, and components only. Access permissions should be designed around the principles of least privilege and separation of duties, ensuring each identity receives only the rights necessary for its function. Authentication mechanisms should be appropriate to the sensitivity of the asset and the context of the interaction (e.g., stronger assurance for privileged or high-risk access). Access policies are expected to be formally defined, consistently enforced, and periodically reviewed to remain commensurate with assessed risk.

## Domain / Applicability

Applies to any workload that exposes resources to human users, automated services, or integrated components — including cloud-hosted applications, APIs, microservices, data platforms, and AI/ML systems. Relevant at initial architecture design and during any significant change to identity or access patterns.

## Evaluation Criteria

COMPLIANT: The design clearly defines identity management for all principals (users, services, hardware/components), specifies authentication mechanisms appropriate to the risk context, and establishes access control policies grounded in least privilege and separation of duties. The design demonstrates how permissions are enforced and reviewed over time, OR provides documented rationale for any deviations with compensating controls.

NON-COMPLIANT: The design lacks a defined access control strategy, does not address authentication for one or more principal types, grants overly broad permissions without justification, or fails to incorporate least privilege and separation of duties principles without documented rationale.
