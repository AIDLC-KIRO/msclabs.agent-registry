---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Workload Network Protection And Continuous Monitoring

**Pack:** NIST CSF Pack  
**Description:** Workloads should be deployed within well-defined network boundaries that restrict unauthorized logical access and limit lateral movement between components. Network segmentation, access controls, and traffic inspection capabilities are recommended to enforce least-privilege connectivity between workload tiers, external services, and users. Complementing these protections, network traffic — both at the perimeter and between internal components — should be continuously monitored against a baseline of authorized communication flows, enabling timely detection of unauthorized access attempts, anomalous patterns, and potential data exfiltration.

## Domain / Applicability

Applies to any workload with networked components, including cloud-native, hybrid, on-premises, and multi-tier architectures. Particularly relevant where workloads handle sensitive data, expose APIs, or communicate with external services or third-party providers.

## Evaluation Criteria

COMPLIANT: Design defines network boundaries and segmentation strategy (e.g., subnets, security groups, VPCs, VLANs, or zero-trust segments) that restrict unauthorized access between workload components and external systems. Design identifies authorized network communication flows and specifies monitoring capabilities (such as VPC Flow Logs, network traffic analysis tools, IDS/IPS solutions, or equivalent) that detect deviations from those baselines. Both protection and detection aspects are addressed, or documented rationale explains compensating controls for any gaps.

NON-COMPLIANT: Design places workload components in flat, unsegmented networks without access controls. Design lacks any network monitoring strategy, or monitoring covers only the perimeter without visibility into internal traffic. Design fails to define authorized communication flows, making anomaly detection infeasible.
