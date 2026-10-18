---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Software Supply Chain Integrity And Acquisition Verification

**Pack:** NIST CSF Pack  
**Description:** Workloads should verify the authenticity and integrity of software components, dependencies, and third-party artifacts before they are acquired, integrated, or deployed. This includes assessing the trustworthiness of suppliers and open-source sources prior to adoption, validating artifact integrity through cryptographic mechanisms (such as checksums, signatures, or attestations), and ensuring only verified, authorized software is permitted to execute within the workload environment. The goal is to reduce the risk of counterfeit, tampered, or maliciously modified components introducing backdoors or vulnerabilities that are difficult to detect post-deployment — a threat demonstrated by high-profile supply chain attacks.

## Domain / Applicability

Applies during workload design and architecture planning, CI/CD pipeline design, dependency management strategy, and any phase where third-party software components, libraries, container images, or infrastructure tooling are selected and integrated into the workload.

## Evaluation Criteria

COMPLIANT: Design demonstrates a strategy for verifying the integrity and authenticity of software components before use — for example, by enforcing cryptographic signature or checksum validation of dependencies (using package signing, artifact attestation, or SBOM-based verification), restricting execution to approved/verified software (via allowlisting, policy enforcement, or trusted registries), and documenting a pre-adoption assessment process for new third-party components or suppliers. Design also addresses ongoing monitoring of dependency risk (e.g., vulnerability scanning, license auditing, or supplier health checks) rather than one-time acquisition checks only. Alternative approaches are acceptable when justified with documented rationale and compensating controls.

NON-COMPLIANT: Design lacks any mechanism for verifying software component integrity prior to use, does not address how unauthorized or unverified software is prevented from executing in the workload, or relies entirely on implicit trust in upstream sources without documented risk assessment or compensating controls.
