---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Incident Response Recovery Communication Planning

**Pack:** NIST CSF Pack  
**Description:** Workloads should incorporate a structured communication strategy as part of their incident response and recovery design. This includes pre-identifying internal and external stakeholders (such as customers, regulators, partners, and supply chain contacts), defining notification timelines and escalation paths, and establishing approved channels and messaging templates for both incident response and recovery updates. Timely, accurate communication during and after an incident is critical to meeting legal breach-notification obligations, enabling coordinated response, and preserving stakeholder trust. Failure to plan communication pathways in advance can result in delayed notifications, regulatory penalties, and reputational harm.

## Domain / Applicability

Incident response and recovery planning for any workload that processes sensitive data, serves external users, or operates under regulatory obligations requiring breach or disruption notification.

## Evaluation Criteria

COMPLIANT: The workload's architecture or incident response design documents a stakeholder communication plan that identifies internal and external notification targets (including relevant third parties and supply chain partners), defines escalation and notification timelines, specifies approved communication channels and pre-approved messaging templates, and addresses ongoing recovery progress updates — OR provides documented rationale for any gaps with compensating controls.

NON-COMPLIANT: The design lacks any defined stakeholder notification strategy, omits external or regulatory notification requirements without justification, or provides no mechanism for communicating recovery progress to affected parties.
