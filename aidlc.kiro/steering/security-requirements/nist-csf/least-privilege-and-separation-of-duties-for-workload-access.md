---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Least Privilege And Separation Of Duties For Workload Access

**Pack:** NIST CSF Pack  
**Description:** Workload access permissions, entitlements, and authorizations should be designed and enforced according to the principles of least privilege and separation of duties. Each user, service identity, and component should be granted only the minimum permissions necessary to perform its authorized function — no more. Sensitive or high-impact operations (such as data deletion, privilege escalation, or production deployments) should require involvement from more than one role or identity, preventing any single actor from completing a critical action unilaterally. Access permissions should also be reviewed periodically to ensure they remain appropriate as the workload evolves, roles change, and team members transition.

## Domain / Applicability

Applies to any workload that defines IAM roles, service accounts, API authorization policies, or resource-level access controls — including cloud-native applications, microservices, data pipelines, and serverless workloads. Particularly critical for workloads handling sensitive data, financial transactions, or privileged infrastructure operations.

## Evaluation Criteria

COMPLIANT: The architecture defines distinct, narrowly scoped roles or policies for each workload component (e.g., separate read/write/admin roles), demonstrates that no single identity holds permissions sufficient to complete a sensitive end-to-end action alone, and describes a process or mechanism for periodic access review. Alternative implementations (such as attribute-based access control, policy-as-code, or just-in-time privilege elevation) are acceptable when they demonstrably achieve least-privilege and separation-of-duties outcomes.

NON-COMPLIANT: The design uses overly broad permissions (e.g., wildcard actions, administrator-level roles for routine operations), allows a single identity to perform sensitive transactions without a second-party check, or lacks any mechanism for reviewing and revoking stale permissions over time.
