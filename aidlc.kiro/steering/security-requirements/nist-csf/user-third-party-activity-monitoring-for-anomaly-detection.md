---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# User Third Party Activity Monitoring For Anomaly Detection

**Pack:** NIST CSF Pack  
**Description:** Workloads should incorporate monitoring of personnel activity and external service provider interactions to detect insider threats, compromised accounts, unauthorized data access, and supply chain-based attacks. Monitoring should focus on identifying anomalous behavioral patterns — such as unusual access volumes, off-hours activity, or unexpected data transfers — rather than routine surveillance. Third-party integrations (e.g., SaaS vendors, managed service providers, cloud APIs) should be treated as distinct monitoring surfaces, with their access and activity observable and auditable within the workload's detection capabilities. Privacy considerations and applicable regulations should inform the scope and retention of monitoring data.

## Domain / Applicability

Applies to workloads where human operators, administrators, or external service providers have access to systems, data, or APIs — particularly those handling sensitive data, privileged operations, or third-party integrations.

## Evaluation Criteria

COMPLIANT: Design identifies key user roles and third-party integrations as monitoring subjects; specifies behavioral baseline or anomaly detection mechanisms (e.g., UEBA tools, SIEM correlation rules, cloud-native threat detection services such as AWS GuardDuty, Microsoft Sentinel, or equivalent); includes audit logging of privileged and third-party access; and documents how alerts are generated for anomalous patterns. Design acknowledges privacy and legal constraints on personnel monitoring scope. OR provides documented rationale for alternative detection approach that addresses insider threat and supply chain risk.

NON-COMPLIANT: Design lacks visibility into personnel or third-party activity; provides no mechanism for detecting anomalous access patterns; treats third-party service provider access as unmonitored; or fails to address insider threat and supply chain attack vectors through any architectural decision.
