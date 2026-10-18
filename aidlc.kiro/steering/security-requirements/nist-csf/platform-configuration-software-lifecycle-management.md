---
inclusion: fileMatch
fileMatchPattern: "**/*"
---

# Platform Configuration Software Lifecycle Management

**Pack:** NIST CSF Pack  
**Description:** Workloads should be designed so that all platform components — including operating systems, runtimes, container base images, application dependencies, and supporting services — are managed in a known, secure, and consistently configured state throughout their lifecycle. This includes establishing baseline configurations, maintaining software currency commensurate with risk, preventing unauthorized software execution, and integrating secure development practices from the start. Unmanaged or misconfigured platform components represent significant attack surfaces that adversaries can exploit to gain unauthorized access, execute malicious code, or disrupt availability.

## Domain / Applicability

Applies to all workloads that deploy software on physical or virtual platforms, including containerized applications, serverless functions, virtual machines, and managed services. Relevant at architecture design time and throughout the software development lifecycle.

## Evaluation Criteria

COMPLIANT: Design specifies a platform management strategy that addresses: (1) baseline configuration management for workload components (e.g., hardened AMIs, container image policies, infrastructure-as-code templates); (2) a software maintenance approach for patching and updating dependencies commensurate with risk; (3) controls to prevent unauthorized software execution (e.g., allowlisting, image signing, runtime enforcement); and (4) integration of security practices in the development lifecycle (e.g., SAST/DAST scanning, dependency vulnerability checks). Alternatively, design provides documented rationale for any gaps with compensating controls identified.

NON-COMPLIANT: Design lacks a defined approach to platform configuration management, makes no provision for software patching or lifecycle management, does not address unauthorized software prevention, and fails to integrate security into the development process — without documented justification or compensating controls.
