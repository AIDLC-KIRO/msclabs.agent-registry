---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Workload Risk Visibility And Communication Design

**Pack:** NIST CSF Pack  
**Description:** Workloads should be designed to surface their security posture in a way that supports structured, bidirectional risk communication across organizational levels. This means the workload architecture is expected to produce meaningful security signals — such as key risk indicators (KRIs), key performance indicators (KPIs), and compliance status — that can be consumed by managers and executives to inform risk decisions. The design should align the workload's security controls and monitoring outputs to documented risk targets, enabling gap analysis between current and target security states.

## Domain / Applicability

Applies during workload architecture and design phases, and whenever the workload's security monitoring or reporting capabilities are reviewed or updated. Particularly relevant when the workload handles sensitive data, supports critical business functions, or is subject to regulatory oversight.

## Evaluation Criteria

COMPLIANT: The workload design identifies security monitoring outputs (e.g., KRIs, KPIs, audit logs, compliance dashboards) and describes how those outputs feed into organizational risk registers, progress reports, or equivalent risk communication mechanisms. The design references a documented risk target or profile against which current state can be measured, OR provides a justified rationale for why such reporting is handled externally.

NON-COMPLIANT: The workload design lacks any mechanism for surfacing security posture to stakeholders beyond the immediate engineering team, with no documented rationale or compensating controls for the omission.
