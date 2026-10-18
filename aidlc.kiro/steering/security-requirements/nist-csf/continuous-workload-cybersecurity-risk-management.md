---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Continuous Workload Cybersecurity Risk Management

**Pack:** NIST CSF Pack  
**Description:** Workload security posture should be treated as a living, continuously evolving state rather than a fixed point-in-time assessment. The workload architecture is expected to reflect an ongoing understanding of its current security posture, a defined target state, and a documented path for closing identified gaps. This approach acknowledges that the workload's threat landscape, dependencies, and risk tolerance may shift over time due to changes in functionality, infrastructure, regulatory requirements, or organizational priorities. Continuous risk management enables the workload to maintain mission-essential functions while adapting security controls to emerging risks and opportunities.

## Domain / Applicability

Applies during initial workload design, major architectural changes, periodic security reviews, and whenever significant changes occur to the workload's threat environment, dependencies, or business context.

## Evaluation Criteria

COMPLIANT: Design documentation includes a current-state security posture assessment, a defined target security state, and a gap analysis or improvement roadmap — OR provides documented rationale for why a simplified risk profile is appropriate given the workload's scope and risk appetite. Design demonstrates awareness of the workload's unique risk factors (e.g., data sensitivity, exposure surface, dependencies) and shows evidence of iterative security improvement over time.

NON-COMPLIANT: Design lacks any documented security posture assessment, shows no awareness of the workload's specific risk profile, or treats security controls as static with no mechanism for periodic review or improvement. Design fails to address how security decisions will be revisited as the workload or its threat environment evolves.
