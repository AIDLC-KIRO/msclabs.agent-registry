# Steering

Steering files give an assistant standing project context while it works. The AI-DLC Center of
Excellence (CoE) maintains the shared standards in this registry; delivery teams review and copy
only the files that apply to their workload.

Steering is guidance, not an enforcement boundary. It is the first layer described in
[How governance works](../../README.md#how-governance-works): steering shapes output, hosted MCP
workflows standardize processes and record human decisions, and repository or CI/CD controls decide
what can merge or deploy.

## Choose what to use

| Need | Start with | Inclusion |
| --- | --- | --- |
| Evidence-based assistant behavior | [`guardrails/guardrails.md`](guardrails/guardrails.md) | `always` |
| Workload security requirements | [`security-requirements/`](security-requirements/) | Requirement files use `fileMatch` with `**/*` |
| Architecture and operations guidance | [`best-practices/`](best-practices/) | `fileMatch` |
| Language, framework, and design conventions | [`development-practices/`](development-practices/) | `fileMatch` |
| Git and change-size guidance | [`project-standards/`](project-standards/) | Mixed; review each file |
| Spec-driven team delivery | [`team-collaboration/`](team-collaboration/) | Mixed; review each file |
| Optional TypeScript/React/AWS stack profile | [`tech.md`](tech.md) | `manual` |

The `devsecops/` and `knowledge-bases/` directories are placeholders and have no entries.

### Security requirement packs

| Pack | Requirements | Scope |
| --- | --- | --- |
| [ASA base pack](security-requirements/asa-base-pack/_index.md) | 10 | Authentication, authorization, audit logging, secret protection, tenant isolation, cryptography |
| [AWS Well-Architected](security-requirements/aws-well-architected/_index.md) | 32 | Well-Architected security guidance |
| [NIST CSF](security-requirements/nist-csf/_index.md) | 37 | Identify, protect, detect, respond, and recover |
| [PCI DSS](security-requirements/pci-dss/_index.md) | 50 | Payment-data scope, segmentation, logging, key management, secure development |

Each `_index.md` is a navigation page. Open it to review the pack, then select the linked requirement
files that apply; copying only the index does not apply the requirements.

> [!CAUTION]
> Every requirement file currently declares `fileMatchPattern: "**/*"`. Once copied, it can appear
> in context for any file. Do not install all 129 requirements by default. Select a pack or individual
> requirements only after the workload's security and compliance scope has been assessed.

## Install selected files

Run these examples from the root of a cloned registry. Replace `/path/to/project` with the target
project directory.

```bash
PROJECT=/path/to/project
mkdir -p "$PROJECT/.kiro/steering/security-requirements/pci-dss"

# Copy shared guardrails.
cp -R aidlc.kiro/steering/guardrails "$PROJECT/.kiro/steering/"

# Example: copy one requirement selected during the workload assessment.
REQUIREMENT=network-security-controls-for-traffic-segmentation.md
cp "aidlc.kiro/steering/security-requirements/pci-dss/$REQUIREMENT" \
   "$PROJECT/.kiro/steering/security-requirements/pci-dss/"
```

Copy an entire pack only when the workload assessment says that every requirement in that pack is
in scope.

For a global installation, copy only rules that genuinely apply to every project:

```bash
mkdir -p ~/.kiro/steering
cp -R aidlc.kiro/steering/guardrails ~/.kiro/steering/
```

Before starting a new Kiro session:

1. Read every selected file and confirm that its scope matches the project.
2. Record the registry commit, selected files, scope rationale, exclusions, conflicts, reviewer or
   owner, and next review date in a project document such as `.kiro/steering-selection.md`.
3. Remove optional or conflicting rules instead of copying them blindly.
4. Commit project-level steering and the selection record so the applicable version is auditable.
5. Start a new session so Kiro loads the newly copied steering.

A minimal selection record can use this structure:

```markdown
# Steering selection

- Registry commit: `<commit-sha>`
- Scope: `<workload and environment>`
- Selected: `<paths>`
- Excluded: `<paths and rationale>`
- Conflicts or exceptions: `<decision and owner>`
- Reviewed by: `<role or team>`
- Next review: `<date>`
```

To track the registry as a dependency, a team may use a Git submodule instead of copying files. Pick
one update model and apply it consistently.

## Inclusion modes

A steering file can declare when Kiro loads it:

```markdown
---
inclusion: fileMatch
fileMatchPattern: "buildspec/*.yml"
---
```

| Value | When it applies |
| --- | --- |
| `always` | Every request; also the default when frontmatter is absent |
| `fileMatch` | When a file matching `fileMatchPattern` is in context |
| `manual` | Only when referenced explicitly with `#` in chat |
| `auto` | When the request matches `description`; also requires `name` and `description` |

A steering file can include another document with `#[[file:<relative-path>]]`. This lets a schema or
other maintained source influence generated code without duplicating it in the steering file.

## Write and review steering

- Prefer `fileMatch`, `auto`, or `manual` over `always` unless a rule genuinely applies to every task.
- State the intended audience, scope, exceptions, and source of authority.
- Keep workload-specific safety rules separate from organization-wide behavior rules.
- Avoid hard-coded account IDs, ARNs, VPC or subnet IDs, internal URLs, and credentials.
- Re-read copied steering when upgrading; registry changes do not automatically update project copies.

## Contributing

Open a reviewed change against `main`. Content in this public registry must be reusable across teams.
Organization-specific identifiers and internal endpoints belong in private project steering, not here.
