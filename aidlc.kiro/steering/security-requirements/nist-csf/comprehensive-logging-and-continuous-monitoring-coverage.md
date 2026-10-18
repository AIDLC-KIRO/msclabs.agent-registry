---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Comprehensive Logging And Continuous Monitoring Coverage

**Pack:** NIST CSF Pack  
**Description:** Workloads should generate structured log records across all relevant components — including application logic, network traffic, runtime environments, and integrations with external service providers — and make those logs continuously available to monitoring and detection systems. Without deliberate design of logging coverage and monitoring pipelines, the workload creates blind spots that delay or prevent detection of attacks, compromises, and anomalous behavior. The architecture should establish persistent visibility into the workload's environment, enabling timely discovery of indicators of compromise and adverse events that support effective incident response.

## Domain / Applicability

Applies to any workload that processes, stores, or transmits sensitive data, or that relies on networked services, external providers, or multi-component architectures where security events could go undetected without deliberate observability design.

## Evaluation Criteria

COMPLIANT: Design identifies the key logging surfaces (application, network, runtime, external integrations) and specifies how logs are collected and made available to monitoring systems (e.g., centralized log aggregation via Amazon CloudWatch Logs, OpenSearch, Splunk, Datadog, or equivalent). Design demonstrates continuous monitoring coverage across relevant dimensions — network traffic, compute/runtime behavior, user/service activity, and third-party provider interactions — using threat detection services (e.g., Amazon GuardDuty, AWS Security Hub, Azure Sentinel, or comparable SIEM/UEBA tools). Design addresses anomaly detection and alerting to enable timely response. Alternative or partial implementations are acceptable when accompanied by documented rationale and compensating controls.

NON-COMPLIANT: Design lacks defined logging coverage for one or more significant workload surfaces without documented justification. Design has no described mechanism for making logs available to monitoring tools or personnel. Design omits monitoring of external service provider activity or third-party integrations without compensating controls. Design provides no path from log data to detection or alerting.
