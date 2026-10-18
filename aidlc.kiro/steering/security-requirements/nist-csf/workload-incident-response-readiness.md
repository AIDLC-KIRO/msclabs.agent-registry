---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Workload Incident Response Readiness

**Pack:** NIST CSF Pack  
**Description:** Workloads should be designed with built-in incident response readiness, ensuring that when a cybersecurity incident is detected, the system can support effective management, analysis, containment, and communication. This includes architectural provisions for forensic data collection and integrity preservation, incident triage and escalation paths, containment and eradication mechanisms, and communication channels to internal and external stakeholders. The goal is to minimize incident impact and enable rapid, evidence-based recovery.

## Domain / Applicability

Applies to all workloads that process, store, or transmit sensitive data or that are exposed to external threats. Particularly critical for workloads with regulatory notification obligations, third-party dependencies, or high availability requirements.

## Evaluation Criteria

COMPLIANT: The architecture demonstrates incident response readiness by addressing most of the following:
- Logging and telemetry pipelines are designed to capture incident-relevant data with integrity protections (e.g., immutable log storage, tamper-evident audit trails using services such as AWS CloudTrail with log file validation, S3 Object Lock, or equivalent write-once storage)
- The design includes mechanisms to isolate or contain affected components (e.g., security group rules, network ACLs, auto-scaling termination policies, or equivalent isolation primitives)
- Escalation and triage paths are defined in the architecture (e.g., alerting integrations with ticketing or on-call systems such as PagerDuty, OpsGenie, or equivalent incident management platforms)
- Stakeholder notification channels are identified and integrated (e.g., SNS topics, email/SMS alerting, or equivalent communication mechanisms)
- Forensic data retention periods and metadata preservation are addressed in the design
- Design specifies criteria or automation triggers for initiating recovery workflows

NON-COMPLIANT: The architecture lacks observable telemetry, has no defined containment mechanisms, provides no escalation or notification paths, or fails to address forensic data integrity — without documented justification or compensating controls.
