---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Secure Software Development Lifecycle Integration

**Pack:** NIST CSF Pack  
**Description:** Workloads should be developed using security practices integrated throughout the entire software development lifecycle (SDLC), rather than applied only at the end. This includes incorporating threat modeling and security requirements during design, applying secure coding standards and peer review during development, and executing security testing (such as static analysis, dynamic analysis, and penetration testing) during validation and pre-deployment stages. Performance of these practices should be monitored to ensure they are applied consistently and effectively, providing evidence of security posture and supporting continuous improvement.

## Domain / Applicability

Applies to any workload undergoing active development, enhancement, or maintenance — including greenfield builds, iterative feature development, and significant refactoring efforts. Relevant from initial design through deployment and ongoing software updates.

## Evaluation Criteria

COMPLIANT: Design and development documentation demonstrates that security activities are embedded across SDLC phases — e.g., threat models or security requirements artifacts exist for design phases; CI/CD pipelines incorporate automated security scanning (using tools such as SAST/DAST scanners, dependency checkers, or equivalent); code review processes include security criteria; and metrics or evidence of security practice performance are tracked. Alternative or compensating approaches are acceptable when documented with rationale.

NON-COMPLIANT: Design lacks evidence of security integration across SDLC phases — e.g., no threat modeling or security requirements at design time, no automated security testing in the delivery pipeline, no code review security criteria, or no mechanism to monitor whether secure development practices are being consistently applied.
