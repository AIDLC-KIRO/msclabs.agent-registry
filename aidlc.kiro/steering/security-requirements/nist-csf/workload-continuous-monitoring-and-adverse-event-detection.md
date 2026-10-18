---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Workload Continuous Monitoring And Adverse Event Detection

**Pack:** NIST CSF Pack  
**Description:** Workloads should be designed with comprehensive, continuous monitoring capabilities that enable timely detection and analysis of anomalies, indicators of compromise, and other potentially adverse events. This includes monitoring across network traffic, runtime environments, application behavior, data access patterns, and external service provider interactions. Detected signals should be correlated from multiple sources, analyzed for impact and scope, enriched with threat intelligence where available, and escalated to authorized personnel or automated response tools when defined incident criteria are met. The goal is to reduce dwell time and support effective incident response.

## Domain / Applicability

Applies to any workload that processes, stores, or transmits sensitive data, or that operates in an environment where compromise could have significant impact. Particularly relevant during architecture design, when defining observability strategy, and when integrating with centralized security operations capabilities.

## Evaluation Criteria

COMPLIANT: Design identifies the monitoring surface areas relevant to the workload (e.g., network flows, API calls, authentication events, runtime behavior, data access, external dependencies) and specifies how signals from these sources are collected and made available for analysis. Design demonstrates a mechanism for correlating events across multiple sources (using SIEM platforms such as Amazon Security Lake, Splunk, Microsoft Sentinel, or equivalent aggregation tools). Design describes how adverse events are analyzed for impact and scope, how threat intelligence is incorporated, and how incidents are declared and routed to authorized staff or automated response systems. OR design provides documented rationale for any monitoring gaps with compensating controls.

NON-COMPLIANT: Design lacks defined monitoring coverage for key workload assets without documented justification. Design relies on isolated, uncorrelated log sources with no aggregation or analysis layer. Design has no defined criteria or pathway for declaring and escalating incidents from detected adverse events.
