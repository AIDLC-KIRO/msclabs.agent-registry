# Steering

Shared steering files for `.kiro/steering/`. Steering adds standing context and instructions to
every request, or to requests that match a condition — team standards, project facts, security
requirements, how to build and test.

## What's here

| Directory | Contents | Inclusion |
| --- | --- | --- |
| [`guardrails/`](guardrails/) | The non-negotiables: source code is the source of truth, no invented facts | `always` |
| [`security-requirements/`](security-requirements/) | 129 security requirements in four packs, each with an `_index.md` | `fileMatch` `**/*` |
| [`best-practices/`](best-practices/) | Twelve-Factor, Terraform practices, Well-Architected context | `fileMatch` |
| [`development-practices/`](development-practices/) | Assessment, code, design, JavaScript and React conventions | `fileMatch` |
| [`project-standards/`](project-standards/) | Git commit standards, minimal-engineering approach | `fileMatch` |
| [`team-collaboration/`](team-collaboration/) | Spec-driven development in a team | `fileMatch` |
| `tech.md` | A Node.js/TypeScript stack opinion | `always` (no frontmatter) |
| `devsecops/`, `knowledge-bases/` | Placeholders, no entries yet | — |

### Security requirement packs

| Pack | Requirements | Source |
| --- | --- | --- |
| [`asa-base-pack/`](security-requirements/asa-base-pack/) | 10 | AWS Security Agent base pack — authentication, authorization, audit logging, secret protection, tenant isolation, trusted cryptography |
| [`aws-well-architected/`](security-requirements/aws-well-architected/) | 32 | Well-Architected security pillar — encryption, segmentation, least privilege, key and credential management, threat modelling |
| [`nist-csf/`](security-requirements/nist-csf/) | 37 | NIST Cybersecurity Framework — identify, protect, detect, respond, recover |
| [`pci-dss/`](security-requirements/pci-dss/) | 50 | PCI DSS — cardholder data scope, CDE segmentation, logging, key management, secure development |

Each pack's `_index.md` lists its requirements. Start there rather than loading a whole pack.

> [!NOTE]
> Every file in the four packs declares `fileMatch` with `fileMatchPattern: "**/*"`, which matches
> any file in context — effectively always on. Copying all 129 into one project puts a large
> amount of standing text in front of every request. Take the packs, or the individual
> requirements, that your workload is actually assessed against.

## Installation

Copy what you need to `.kiro/steering/` for one project, or `~/.kiro/steering/` for every
project. Directory structure is preserved; Kiro reads the tree.

```bash
# one pack
cp -R aidlc.kiro/steering/security-requirements/pci-dss \
      your-project/.kiro/steering/security-requirements/

# the guardrails, which most teams want everywhere
cp -R aidlc.kiro/steering/guardrails ~/.kiro/steering/
```

## Writing a steering file

```markdown
---
inclusion: fileMatch
fileMatchPattern: "buildspec/*.yml"
---
```

| Value | When it applies |
| --- | --- |
| `always` | Every request. The default when frontmatter is absent |
| `fileMatch` | When a file matching `fileMatchPattern` is in context |
| `manual` | Only when referenced with `#` in chat |
| `auto` | When the request matches the file's `description`; needs `name` and `description` too |

A steering file can pull in another document with `#[[file:<relative-path>]]`, which is how an
OpenAPI or GraphQL schema can influence generated code without being pasted into a prompt.

## Contributing

Open a pull request against `main`. Steering here has to be a standard any team can apply.
Organisation-specific values — account IDs, ARNs, VPC and subnet IDs, internal URLs — belong in
your own repository's steering, not in a public registry.

Prefer `fileMatch` or `auto` over `always` unless the content genuinely applies to every request.
Everything marked `always` is paid for on every turn.
