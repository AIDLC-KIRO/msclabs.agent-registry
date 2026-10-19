# MSC Labs Agent Registry

_Read this in other languages: [ไทย](README.th.md)_

[![License: Apache-2.0](https://img.shields.io/badge/License-Apache%202.0-yellow.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![clients](https://img.shields.io/badge/clients-1.0.0-blue)](https://pypi.org/project/aidlc.devsecops-cicd-mcp/)

This repository is the organization's central configuration source for AI-assisted delivery. The
AI-DLC Center of Excellence (CoE) maintains shared guardrails, security requirements, architecture
standards, and hosted workflows. Delivery teams consume those controls and propose changes through
the organization's review process.

> [!IMPORTANT]
> Generative AI can make mistakes. Review generated output, infrastructure changes, and costs
> before acting. Steering influences assistant behavior but does not guarantee results. Independent
> repository and pipeline controls determine whether a change can be merged or deployed.

## Users and responsibilities

| Role | Access | Responsibility |
| --- | --- | --- |
| **AI-DLC CoE** — engineering, security, and architecture owners | Write through reviewed changes | Maintain organizational standards and hosted workflow services |
| **Delivery teams** | Read-only consumption | Apply relevant controls, run workflows, and propose corrections when standards need to change |

Server-side hosting prevents delivery teams from modifying hosted workflow and policy content on
their local machines. This does not by itself enforce deployment policy; enforcement depends on
independent repository permissions, approvals, and CI/CD pipeline controls.

## Repository contents

| Folder | Contents | Status |
| --- | --- | --- |
| [`aidlc.kiro/steering/`](aidlc.kiro/steering/) | Guardrails, conventions, and 129 security requirements across four compliance packs | Available |
| [`aidlc.kiro/mcp/`](aidlc.kiro/mcp/) | Four hosted workflow servers, published bridges, and an operations runbook | Available |
| [`aidlc.kiro/skills/`](aidlc.kiro/skills/) | Agent skills distributed by the CoE | No entries yet |
| [`aidlc.kiro/hooks/`](aidlc.kiro/hooks/) | Agent hooks for `.kiro/hooks/` | No entries yet |

### Compliance coverage

| Pack | Requirements | Coverage |
| --- | --- | --- |
| [ASA base pack](aidlc.kiro/steering/security-requirements/asa-base-pack/) | 10 | Authentication, authorization, audit logging, secret protection, tenant isolation, trusted cryptography |
| [AWS Well-Architected](aidlc.kiro/steering/security-requirements/aws-well-architected/) | 32 | Encryption, network segmentation, least privilege, credential management, threat modeling |
| [NIST CSF](aidlc.kiro/steering/security-requirements/nist-csf/) | 37 | Identify, protect, detect, respond, recover |
| [PCI DSS](aidlc.kiro/steering/security-requirements/pci-dss/) | 50 | Cardholder-data scope, segmentation, logging, key management, secure development |

ISO 27001 and Thailand's Personal Data Protection Act (PDPA) packs are not currently included.
Existing requirements may overlap with those frameworks, but this repository does not claim
coverage without a dedicated mapping. See [Contributing](#contributing).

Architecture and engineering standards are under
[`best-practices/`](aidlc.kiro/steering/best-practices/),
[`development-practices/`](aidlc.kiro/steering/development-practices/),
[`project-standards/`](aidlc.kiro/steering/project-standards/), and
[`guardrails/`](aidlc.kiro/steering/guardrails/).

## Use the central configuration

Clone the repository and copy only the controls relevant to the workload:

```bash
git clone --depth 1 https://github.com/AIDLC-KIRO/msclabs.agent-registry.git /tmp/registry
mkdir -p .kiro/steering
cp -R /tmp/registry/aidlc.kiro/steering/guardrails .kiro/steering/
cp -R /tmp/registry/aidlc.kiro/steering/development-practices .kiro/steering/
cp -R /tmp/registry/aidlc.kiro/steering/security-requirements/pci-dss \
      .kiro/steering/security-requirements/
```

Commit copied controls so the applicable version is recorded with the project. The
[steering README](aidlc.kiro/steering/README.md) explains inclusion modes. A team may instead use a
Git submodule where its dependency-management policy permits one.

Organization-specific account identifiers, Amazon Resource Names (ARNs), network identifiers,
internal URLs, and credentials must remain in approved private systems, not this public repository.

## MCP servers

| Server | Purpose | Tools | Documentation |
| --- | --- | --- | --- |
| **aidlc.devsecops-cicd** | Guide application preparation, policy review, pipeline observation, and deployment handoff | 14 | [devsecops-cicd](aidlc.kiro/mcp/devsecops-cicd/README.md) |
| **aidlc.html-creator** | Produce offline bilingual documentation from AWS Transform assessments | 14 | [html-creator](aidlc.kiro/mcp/html-creator/README.md) |
| **aidlc.bpmn-creator** | Model a process as a BPMN 2.0 swimlane diagram and support departmental review | 12 | [bpmn-creator](aidlc.kiro/mcp/bpmn-creator/README.md) |
| **aidlc.deck-creator** | Produce an HTML presentation, executive summary, or progress report from project evidence | 16 | [deck-creator](aidlc.kiro/mcp/deck-creator/README.md) |

Each PyPI package is a local standard input/output (stdio) bridge to a hosted service. Workflow
steps, references, templates, and policy content remain hosted.

## Prerequisites

1. Kiro IDE, the documented and tested client. Other stdio MCP clients may require client-specific
   command, environment-variable, and variable-expansion configuration.
2. [uv](https://docs.astral.sh/uv/getting-started/installation/) for `uvx`.
3. Python 3.10 or later (`uv python install 3.10`).
4. An access key supplied by the deploying organization or service owner.
5. Outbound HTTPS to `*.execute-api.ap-southeast-7.amazonaws.com`.

BPMN also requires Node.js and the
[draw.io MCP server](https://www.npmjs.com/package/@drawio/mcp).

## Getting access

Reading this repository requires no access key. The hosted services require a credential that the current
bridge sends in the `x-api-key` request header. This repository does not document the service's
complete authentication or authorization architecture and does not claim that the header alone
provides authorization.

No public key-request route is documented here. The deploying organization or service owner must
provide organization-specific issuance, revocation, and support contacts. Do not share a key.
Report a suspected disclosure through the private incident route supplied by the service owner.

Every newly issued key has an expiry date: 7, 30, 60, or 90 days, or a custom date chosen by the
service owner. A key is valid through its expiry date (Asia/Bangkok time) and is revoked by a job
that runs daily at 00:00 Asia/Bangkok; from then on the service answers `403`. Keys issued before
expiry was introduced have no date and do not expire. Request a replacement before the date.

With the key, the service owner hands over an `mcp.json` that lists only the servers you need. It
uses the `uvx` bridge by default; a direct URL form is also available (see [Installation](#installation)).

![API key lifecycle: the service owner issues a key with an expiry date and hands over mcp.json; the client calls API Gateway with x-api-key; EventBridge Scheduler runs a Lambda every day at 00:00 Asia/Bangkok that disables keys past their date](docs/diagrams/key-lifecycle.drawio.png)

## Installation

Store the key in a protected local file. The following zsh commands prompt without displaying or
recording the key in shell history:

```bash
# macOS, Linux, and WSL with zsh
mkdir -p ~/.aidlc
read -rs "MCP_API_TOKEN?Access key: " && printf '\n'
printf '%s' "$MCP_API_TOKEN" > ~/.aidlc/mcp-token
unset MCP_API_TOKEN
chmod 600 ~/.aidlc/mcp-token
echo 'export MCP_API_TOKEN=$(cat ~/.aidlc/mcp-token)' >> ~/.zshrc
source ~/.zshrc
```

For Kiro launched from Finder or the Dock on macOS, `.zshrc` is not sufficient. Set the variable
for the current graphical login session, then quit Kiro with `Cmd+Q` and reopen it:

```bash
launchctl setenv MCP_API_TOKEN "$(cat ~/.aidlc/mcp-token)"
```

On Windows, enter the key at the secure prompt rather than placing it in the command history:

```powershell
$secureKey = Read-Host "Access key" -AsSecureString
$key = [System.Net.NetworkCredential]::new("", $secureKey).Password
[Environment]::SetEnvironmentVariable("MCP_API_TOKEN", $key, "User")
Remove-Variable key, secureKey
```

The setting affects future processes. Close all Kiro windows, confirm no Kiro process remains in
Task Manager, and reopen it; sign out or restart Windows if necessary.

Merge [`aidlc.kiro/mcp/mcp.json`](aidlc.kiro/mcp/mcp.json) into Kiro's user or project MCP
configuration. Add `MCP_API_TOKEN` to `kiroAgent.mcpApprovedEnvVars`. Keep
`${MCP_API_TOKEN}` in `mcp.json`; do not paste the raw key into that file.

Clients that support remote MCP servers can skip the bridge and connect straight to the endpoint.
Each entry then uses `url` and sends the key in the `x-api-key` header:

```json
"aidlc.devsecops-cicd": {
  "url": "https://8a3gpe2ji0.execute-api.ap-southeast-7.amazonaws.com/v1/devsecops-cicd/mcp",
  "headers": { "x-api-key": "${MCP_API_TOKEN}" },
  "disabled": false
}
```

The provided configuration uses `@latest`. Use an exact version such as
`"aidlc.devsecops-cicd-mcp==1.0.0"` for reproducible team or CI configuration. Full platform setup,
verification, upgrade, and rotation procedures are in the [runbook](aidlc.kiro/mcp/RUNBOOK.md).

## Usage

Describe the intended result in chat. For example:

```text
Prepare repo my-org/my-service for the development pipeline
Build a documentation site from ./ATXDocumentation
Map the leave request process as BPMN
Build an executive summary from .kiro/specs/order-service
```

The servers share a common core tool pattern, not identical sessions. All provide start, step,
status, run-log, request-draft, catalogue, reference, and asset operations. DevSecOps, HTML, and
deck provide human gate confirmation. BPMN is the exception: it performs review in workflow step 6
and has no `gate_confirm` tool. See the [MCP overview](aidlc.kiro/mcp/README.md) for the tool matrix.

## Architecture and operational boundary

![Registry architecture: the MCP client and uvx bridge on the local machine call API Gateway with x-api-key; four Lambda MCP servers keep sessions in DynamoDB and hand out S3 presigned URLs; Git push, read-only AWS discovery and the team pipeline stay on the team side](docs/diagrams/registry-architecture.drawio.png)

Diagram source: [`docs/diagrams/`](docs/diagrams/). The PNG files embed the draw.io diagram, so they open and edit directly in draw.io.

The local client or assistant may run read-only AWS commands with credentials on the user's machine.
The hosted MCP service does not receive those AWS credentials, call AWS on the user's behalf, push
source code, or deploy. Source-control and deployment actions remain subject to local approval,
repository permissions, and independent pipeline controls.

Tools receive the arguments submitted by the client. For example,
`cicd_changeset_validate` evaluates proposed change-set data sent in its arguments; it does not
inspect local files remotely. Review the relevant server README before submitting content.

## Data handling and privacy

JSON-RPC tool arguments are sent from the local bridge to the hosted service over HTTPS. Do not
send secrets, credentials, or regulated or sensitive data unless your organization has approved
the service for that use. This repository does not document retention, service-side logging, or
data residency. Obtain those details from the service owner before submitting data with specific
handling requirements.

## Environment variables

| Variable | Description | Default |
| --- | --- | --- |
| `MCP_API_TOKEN` | Access key; required | — |
| `MSCLABS_MCP_TOKEN` | Alternative access-key variable | — |
| `MSCLABS_MCP_BASE_URL` | Alternative service deployment | CoE endpoint |
| `MSCLABS_MCP_TIMEOUT` | Request timeout in seconds | `120` |

## Troubleshooting

| Symptom | Guidance |
| --- | --- |
| `Dynamic Client Registration rejected (HTTP 404)` | Confirm Kiro received the variable, approved its name, and was fully restarted |
| `No API key` | Neither supported access-key variable reached the bridge |
| `403 … the API key was rejected` | Check for a truncated, mistyped, revoked, or expired key; request a replacement if the expiry date has passed |
| `429` | Retry with backoff; a per-key usage plan is possible, but shared API, stage, or account limits may also apply |
| `could not reach the registry` | Check proxy, VPN, firewall, and DNS access |
| `uvx: command not found` | Use the absolute `uvx` path or provide an appropriate `PATH` |
| BPMN diagram is not created | Install and configure the separate draw.io MCP server |

There is no documented unauthenticated health route. Use the `tools/list` key and connectivity
check in the [runbook](aidlc.kiro/mcp/RUNBOOK.md#4-verify-connectivity-and-the-key).

## Getting help

No guaranteed public support or private security contact is documented in this repository. Obtain
those routes from the deploying organization or service owner. If public issues are enabled, never
include credentials, sensitive tool arguments, or unredacted logs.

## Contributing

Delivery teams propose changes through the review route established by their organization. New
compliance packs belong under `aidlc.kiro/steering/security-requirements/<pack>/` and must state
both their coverage and limitations. Do not add secrets, credentials, account identifiers, ARNs,
or internal endpoints to this public repository.

## License

Apache-2.0. See [LICENSE](LICENSE).
