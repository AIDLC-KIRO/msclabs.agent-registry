---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Workload Infrastructure Resilience Architecture

**Pack:** NIST CSF Pack  
**Description:** Workload security architectures should be designed to protect asset confidentiality, integrity, and availability while withstanding and recovering from adverse events such as cyberattacks, environmental disruptions, and demand surges. This encompasses four complementary dimensions: logical network protection to prevent unauthorized access and lateral movement; environmental threat mitigation to guard against physical risks; resilience mechanisms such as redundancy, failover, and disaster recovery that function under both normal and adverse conditions; and capacity management to ensure availability is maintained under stress or denial-of-service conditions. Without deliberate resilience design, a single incident can cascade into widespread operational failure.

## Domain / Applicability

Applies to all workloads and services across any deployment environment (cloud, on-premises, hybrid, or OT), particularly those with availability, integrity, or confidentiality requirements. Most relevant during architecture design, capacity planning, and disaster recovery planning phases.

## Evaluation Criteria

COMPLIANT: Design demonstrates resilience across all four dimensions — (1) network segmentation and access controls to limit unauthorized logical access and lateral movement; (2) environmental risk mitigations such as multi-zone/multi-region deployment or physical redundancy; (3) documented redundancy, failover, and disaster recovery mechanisms that address both normal and adverse scenarios; and (4) capacity management strategies (e.g., auto-scaling, rate limiting, load balancing, or DDoS protection) to sustain availability under load. Design may address these through different valid implementations provided the underlying resilience objectives are met and tradeoffs are documented.

NON-COMPLIANT: Design lacks resilience considerations in one or more dimensions without documented justification — e.g., single points of failure with no failover, no network segmentation, no capacity management strategy, or no disaster recovery plan — and does not provide compensating controls or risk acceptance rationale.
