---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Ai Component Risk Assessment And Security Integration

**Pack:** NIST CSF Pack  
**Description:** Workloads that incorporate AI or machine learning components — such as inference endpoints, LLM integrations, ML training pipelines, or AI-assisted decision systems — should proactively identify and address the unique security and privacy risks those components introduce. AI systems can expand a workload's attack surface through adversarial input manipulation, data poisoning of training or fine-tuning datasets, model inversion attacks, and large-scale privacy exposure from data processing. Security risk assessment for AI components is recommended to be integrated with the workload's broader threat model and risk management approach, covering the full AI lifecycle from design through deployment and ongoing evaluation.

## Domain / Applicability

Workloads that design, develop, deploy, or consume AI/ML capabilities — including generative AI APIs, embedded ML models, retrieval-augmented generation (RAG) pipelines, or AI-driven automation — where novel threat vectors such as prompt injection, model tampering, or training data compromise are relevant architectural concerns.

## Evaluation Criteria

COMPLIANT: Architecture documentation identifies AI/ML components and addresses their specific risk profile, including at least a subset of: adversarial input risks, data integrity of training/inference data, model access controls, output validation, and privacy implications of data processed by the AI system. The design demonstrates that AI-related risks are considered alongside conventional cybersecurity risks (e.g., within a threat model, risk register, or security design review). Alternative risk frameworks (e.g., NIST AI RMF, MITRE ATLAS, OWASP LLM Top 10) are acceptable as complementary references.

NON-COMPLIANT: Architecture incorporates AI/ML components but provides no documented consideration of AI-specific threats or risks. Design lacks any threat modeling, risk assessment, or compensating controls addressing adversarial manipulation, data poisoning, or privacy risks unique to the AI components in use.
