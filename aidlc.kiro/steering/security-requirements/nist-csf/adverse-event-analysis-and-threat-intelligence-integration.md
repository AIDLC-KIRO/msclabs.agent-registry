---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Adverse Event Analysis And Threat Intelligence Integration

**Pack:** NIST CSF Pack  
**Description:** Workloads should be designed to support the detection and analysis of anomalies, indicators of compromise (IoCs), and other potentially adverse events. This includes emitting sufficient telemetry from all workload components to enable multi-source correlation, integrating cyber threat intelligence (CTI) to contextualize observed anomalies against known tactics, techniques, and procedures (TTPs), and establishing defined criteria for escalating adverse events to formal incident declarations. The design should ensure that adverse event information flows to authorized personnel and automated response tooling in a timely manner, enabling accurate impact and scope estimation.

## Domain / Applicability

Applies to workloads that process, store, or transmit sensitive data, or that are exposed to external threats. Relevant during architecture design and when defining detection, monitoring, and incident response capabilities for the workload.

## Evaluation Criteria

COMPLIANT: Design specifies telemetry sources (e.g., application logs, API access logs, network flow data, authentication events) that collectively enable multi-source event correlation; design describes integration with threat intelligence feeds or enrichment services (such as AWS Security Hub with threat intel integrations, Amazon GuardDuty, MISP, or equivalent CTI platforms); design defines incident declaration criteria and escalation paths; and design demonstrates how adverse event information reaches authorized staff and automated tools (e.g., via SIEM, SOAR, or alerting pipelines). Alternative detection architectures are acceptable when they demonstrably address the same objectives with documented rationale.

NON-COMPLIANT: Design relies on a single telemetry source with no correlation capability; design lacks any mechanism for threat intelligence enrichment or contextualizing anomalies; design has no defined criteria for escalating adverse events to incident response; or design fails to describe how adverse event information reaches response-capable staff or tooling.
