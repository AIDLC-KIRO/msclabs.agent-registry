---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Workload Asset Inventory And Lifecycle Management

**Pack:** NIST CSF Pack  
**Description:** A workload should maintain a comprehensive, current inventory of all assets it owns or depends upon — including software components, services, data stores, APIs, third-party/supplier integrations, and network data flows. Assets should be classified by criticality and sensitivity so that the most important ones receive proportionally stronger protection. Managing assets throughout their lifecycle (from onboarding through decommission) is recommended to prevent end-of-life or forgotten components from becoming unmanaged security liabilities. Without this foundational visibility, other security functions such as threat detection, incident response, and vulnerability management cannot operate effectively.

## Domain / Applicability

Applies to any workload during architecture design and throughout its operational lifecycle, particularly when the workload integrates external services, manages sensitive data, or relies on third-party dependencies. Relevant at design time (component selection, data flow mapping) and continuously during operations (dependency updates, decommissioning).

## Evaluation Criteria

COMPLIANT: Design identifies and documents the workload's key asset categories — including software dependencies, cloud/managed services, data stores, external APIs or supplier services, and authorized network/data flows — and assigns relative criticality or classification to each. Design addresses lifecycle considerations (e.g., dependency version management, decommission procedures, end-of-life policies) OR provides documented rationale for why certain asset categories are out of scope. Code artifacts (e.g., dependency manifests, IaC templates, service catalogs) are consistent with the documented asset inventory.

NON-COMPLIANT: Design lacks identification of workload components, data flows, or third-party dependencies without documented justification. Design fails to address asset criticality or classification, making it impossible to prioritize protective controls. Design shows no consideration of asset lifecycle management, leaving decommissioned or end-of-life assets as potential unmanaged risks.
