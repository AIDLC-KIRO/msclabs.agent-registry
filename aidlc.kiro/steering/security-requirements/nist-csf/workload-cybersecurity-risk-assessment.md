---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Workload Cybersecurity Risk Assessment

**Pack:** NIST CSF Pack  
**Description:** Workloads should incorporate a structured cybersecurity risk assessment process to identify, analyze, and respond to threats and vulnerabilities relevant to the workload's assets, data, and dependencies. This includes identifying vulnerabilities in workload components, assessing the likelihood and potential impact of threats exploiting those vulnerabilities, and using that understanding to prioritize risk responses. Risk assessments should also account for changes and exceptions to the workload, ensuring that architectural or configuration modifications are evaluated for their risk impact before being adopted.

## Domain / Applicability

Applies during workload design, architecture review, and any significant change to the workload's components, data flows, integrations, or dependencies. Also applies when new threat intelligence or vulnerability disclosures are received that may affect the workload.

## Evaluation Criteria

COMPLIANT: The architecture document includes or references a threat model or risk assessment for the workload that identifies relevant threats, vulnerabilities, likelihoods, and potential impacts; documents how risk findings inform design decisions and security control prioritization; and describes a process for reassessing risk when changes or exceptions occur. Alternative risk assessment methodologies (e.g., STRIDE, PASTA, OCTAVE, or NIST SP 800-30-aligned approaches) are acceptable when they address the same objectives.

NON-COMPLIANT: The design lacks any documented risk assessment, threat model, or risk-informed rationale for security control selection, with no justification for the omission. The design shows no evidence that threats, vulnerabilities, or impacts were considered in architectural decisions.
