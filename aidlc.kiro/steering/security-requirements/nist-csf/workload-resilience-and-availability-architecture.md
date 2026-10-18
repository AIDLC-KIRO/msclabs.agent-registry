---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Workload Resilience And Availability Architecture

**Pack:** NIST CSF Pack  
**Description:** Workloads should be designed with resilience mechanisms that protect against environmental threats, component failures, and capacity constraints. The architecture is expected to define recovery objectives (RTO and RPO) based on business impact analysis, and implement redundancy, failover, and geographic distribution commensurate with those objectives. Capacity planning should account for both normal operating conditions and stress scenarios such as unexpected demand spikes or partial infrastructure loss, to reduce the risk of service degradation or outage.

## Domain / Applicability

Applies during workload architecture and design phases, particularly for systems with availability or continuity requirements. Relevant whenever a workload hosts critical data, serves external users, or supports mission-critical operations that have defined recovery expectations.

## Evaluation Criteria

COMPLIANT: Design specifies defined RTO and RPO targets derived from business impact analysis, AND demonstrates resilience mechanisms (such as multi-AZ/multi-region deployment, redundant data paths, auto-scaling, or failover capabilities) aligned to those targets. Design addresses capacity management for normal and adverse conditions, OR provides documented rationale for a reduced resilience posture with compensating controls.

NON-COMPLIANT: Design lacks defined recovery objectives, fails to address redundancy or failover for critical components, or does not consider capacity under stress conditions without documented justification. Design relies on single points of failure for critical workload functions without compensating controls.
