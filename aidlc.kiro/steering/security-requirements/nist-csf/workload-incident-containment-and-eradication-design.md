---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Workload Incident Containment And Eradication Design

**Pack:** NIST CSF Pack  
**Description:** Workloads should be designed to support rapid containment and eradication of cybersecurity incidents. This means the architecture should enable isolation of affected components (e.g., network segmentation, quarantine zones), revocation of compromised identities, and blocking of malicious traffic without requiring full system shutdown. Eradication capabilities — such as credential rotation, vulnerability patching, and malware removal — should be achievable independently per component to minimize operational disruption. Recovery should not begin until containment and eradication are confirmed complete and the environment is verified clean.

## Domain / Applicability

Incident Response — applicable during workload design and architecture review, and exercised during active security incidents or incident response planning.

## Evaluation Criteria

COMPLIANT: Design demonstrates containment-ready architecture through one or more of: network segmentation or micro-segmentation enabling component isolation, identity/credential mechanisms that support rapid revocation or rotation, traffic control capabilities (security groups, firewall rules, WAF policies, or equivalent) that can block malicious actors, and documented eradication procedures (credential reset, patch application, backup integrity verification) tied to workload components. Design includes or references criteria that gate recovery on confirmed containment and eradication completion.

NON-COMPLIANT: Design lacks any architectural provisions for isolating affected components, revoking compromised credentials, or blocking malicious traffic during an incident. Design allows recovery to begin without documented verification that the threat has been removed, or uses tightly coupled components with no isolation boundary that would prevent incident spread.
