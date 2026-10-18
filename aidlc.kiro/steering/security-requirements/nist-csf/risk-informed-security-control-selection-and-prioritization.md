---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Risk Informed Security Control Selection And Prioritization

**Pack:** NIST CSF Pack  
**Description:** Workload security controls should be selected and prioritized through a structured, risk-informed process rather than ad hoc decisions. The security design is expected to demonstrate how identified risks map to specific security controls, drawing on recognized frameworks and standards (such as NIST SP 800-53, CSF Core outcomes, CIS Controls, or equivalent) to ensure coverage is outcome-driven and traceable. This approach ensures that control choices reflect the workload's threat landscape, data sensitivity, and operational context, and that gaps or tradeoffs are explicitly acknowledged and documented.

## Domain / Applicability

Workload security architecture and design — applicable when defining, reviewing, or updating the security control set for a workload, particularly during threat modeling, security design reviews, or compliance assessments.

## Evaluation Criteria

COMPLIANT: The design document demonstrates a risk-informed rationale for security control selection, referencing a recognized control framework or standard (e.g., NIST SP 800-53, CSF, CIS Controls, ISO 27001 Annex A) and showing traceability between identified risks or threats and the controls chosen to address them. Gaps or accepted risks are documented with justification.

NON-COMPLIANT: The design lists security controls without any documented rationale, risk mapping, or framework alignment — controls appear selected arbitrarily or by convention without evidence of risk-based prioritization. No traceability exists between identified threats and implemented controls.
