---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Privacy Cybersecurity Coordinated Risk Management

**Pack:** NIST CSF Pack  
**Description:** Workloads that collect, process, store, or transmit personal data should address both cybersecurity risks (confidentiality, integrity, and availability of personal data) and privacy risks (harms arising from how data is collected, used, and shared). These two disciplines are complementary but distinct — cybersecurity controls alone are insufficient to protect individuals from privacy harms such as discrimination, stigma, or economic loss that can result from lawful but inappropriate data processing. The workload's design is expected to identify applicable privacy-related legal and regulatory obligations (e.g., GDPR, CCPA, HIPAA, or sector-specific requirements) and ensure that both cybersecurity and privacy controls are coordinated to provide comprehensive protection for personal data throughout its lifecycle.

## Domain / Applicability

Applies to any workload that processes personal or sensitive data, including data collection, storage, transformation, sharing, or analytics pipelines. Particularly relevant during initial architecture design, threat modeling, and when onboarding new data categories or processing purposes.

## Evaluation Criteria

COMPLIANT: Design demonstrates awareness of both cybersecurity and privacy risk dimensions for personal data — for example, it identifies applicable regulatory obligations (GDPR, CCPA, HIPAA, or equivalent), documents data flows and processing purposes, and specifies controls addressing both breach prevention (encryption, access control, logging) and privacy governance (data minimization, purpose limitation, retention policies, consent mechanisms). Design need not implement every possible control but should show that privacy risks beyond breach scenarios have been considered and addressed proportionally.

NON-COMPLIANT: Design addresses only technical security controls (e.g., encryption, authentication) without any consideration of privacy obligations, data governance, or the regulatory landscape applicable to the personal data being processed. Design lacks documented rationale for how personal data processing aligns with legal or contractual privacy requirements.
