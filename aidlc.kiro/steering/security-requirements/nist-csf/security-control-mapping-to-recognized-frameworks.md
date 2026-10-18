---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Security Control Mapping To Recognized Frameworks

**Pack:** NIST CSF Pack  
**Description:** Workload security designs are expected to align with and be traceable to recognized security standards, guidelines, and frameworks (such as NIST CSF, SP 800-53, CIS Controls, ISO 27001, or sector-specific equivalents). Grounding architectural security decisions in established references helps ensure completeness, supports risk communication, and enables consistent assessment of the workload's cybersecurity posture. Where gaps exist between framework guidance and workload-specific needs, those deviations should be documented with rationale.

## Domain / Applicability

Security architecture and design phases, particularly when defining workload security requirements, threat models, or control selection rationale.

## Evaluation Criteria

COMPLIANT: Design documentation references one or more recognized security frameworks or standards to justify control selections, OR provides documented rationale for an alternative approach. Security decisions demonstrate awareness of relevant informative references (e.g., NIST SP 800-53 controls, CIS Benchmarks, cloud provider security frameworks) appropriate to the workload's sector and technology stack.

NON-COMPLIANT: Design lacks any traceability to recognized security standards, with no documented justification for control selections, leaving security decisions without a defensible baseline or risk rationale.
