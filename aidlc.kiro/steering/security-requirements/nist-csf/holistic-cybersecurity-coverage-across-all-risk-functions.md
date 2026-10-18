---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Holistic Cybersecurity Coverage Across All Risk Functions

**Pack:** NIST CSF Pack  
**Description:** A workload's security architecture is expected to address cybersecurity risk management holistically, spanning all major functional domains: governance, asset identification, protection, detection, response, and recovery. These functions are not sequential phases but concurrent, continuous concerns — preventive and preparatory controls (govern, identify, protect) should operate continuously alongside detection capabilities, while response and recovery capabilities should be designed and ready before incidents occur. Treating security as a single-dimension concern (e.g., only perimeter protection) leaves critical gaps in the workload's overall risk posture.

## Domain / Applicability

Applies during workload architecture design and security review, particularly when evaluating whether the workload's security posture comprehensively addresses the full lifecycle of cybersecurity risk — from prevention and preparation through detection, response, and recovery.

## Evaluation Criteria

COMPLIANT: The architecture demonstrates security controls or design decisions that span multiple cybersecurity functional domains — including at minimum: asset/data identification and classification, protective controls, detection/monitoring capabilities, and documented response/recovery considerations. The design need not use identical terminology but should address the underlying security objectives of each domain.

NON-COMPLIANT: The architecture focuses exclusively on one or two security dimensions (e.g., only access control and encryption) without addressing detection, incident response readiness, or recovery, and provides no documented rationale or compensating context for the gaps.
