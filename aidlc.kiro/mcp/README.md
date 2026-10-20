# Hosted MCP Workflows

The AI-DLC Center of Excellence (CoE) at MSC Labs hosts four Model Context Protocol (MCP) workflow
servers in AWS Asia Pacific (Thailand), `ap-southeast-7`. Each published PyPI package is a local
standard input/output (stdio) bridge; workflow steps, policy, references, and templates remain on the
hosted service.

## Choose a workflow

| Server | Use it to | Package | Version | Tools | Guide |
| --- | --- | --- | --- | --- | --- |
| `aidlc.devsecops-cicd` | Prepare applications, review policy, observe pipelines, and hand off deployment | [aidlc.devsecops-cicd-mcp](https://pypi.org/project/aidlc.devsecops-cicd-mcp/) | 1.0.0 | 14 | [Open](devsecops-cicd/README.md) |
| `aidlc.html-creator` | Build offline bilingual sites from AWS Transform assessments | [aidlc.html-creator-mcp](https://pypi.org/project/aidlc.html-creator-mcp/) | 1.0.0 | 14 | [Open](html-creator/README.md) |
| `aidlc.bpmn-creator` | Model BPMN 2.0 swimlanes and run departmental review | [aidlc.bpmn-creator-mcp](https://pypi.org/project/aidlc.bpmn-creator-mcp/) | 1.0.0 | 12 | [Open](bpmn-creator/README.md) |
| `aidlc.deck-creator` | Build HTML presentations, executive summaries, and progress reports | [aidlc.deck-creator-mcp](https://pypi.org/project/aidlc.deck-creator-mcp/) | 1.0.0 | 16 | [Open](deck-creator/README.md) |

Versions were checked against the linked PyPI project pages on 20 October 2026. The sample
[`mcp.json`](mcp.json) tracks `@latest`; use the [runbook](RUNBOOK.md#6-upgrade-and-roll-back) to pin,
upgrade, or roll back a bridge. The former `msclabs.*-mcp-server` packages are retired.

### Terms used in these documents

| Term | Meaning |
| --- | --- |
| **Hosted workflow** | The server-side steps, references, policy content, and session state controlled by the CoE |
| **Bridge** | A small local PyPI package that carries JSON-RPC messages between an stdio MCP client and the hosted service |
| **Access key** | The credential supplied by the service owner and sent by the bridge in the `x-api-key` header |
| **Human gate** | A recorded person-supplied decision; it does not replace repository or pipeline approval |

## Prerequisites

1. Kiro IDE, the documented and tested client. Other stdio MCP clients may require different command,
   environment-variable, or variable-expansion settings.
2. [uv](https://docs.astral.sh/uv/getting-started/installation/) for `uvx`.
3. Python 3.10 or later (`uv python install 3.10`).
4. An access key from the service owner; see [Getting access](../../README.md#getting-access).
5. Outbound HTTPS access to `*.execute-api.ap-southeast-7.amazonaws.com`.
6. For `bpmn-creator` only, Node.js and the
   [draw.io MCP server](https://www.npmjs.com/package/@drawio/mcp).

## Configure Kiro

1. Store the access key as `MCP_API_TOKEN`; never put the raw value in `mcp.json`.
2. Choose only the servers you need. [`mcp.json`](mcp.json) is an all-server example with all four
   entries enabled; it is not a least-privilege install-as-is baseline. Copy only approved entries,
   or set unused entries to `"disabled": true`. A service owner may provide a reduced copy.
3. Merge the selected entries into the existing `mcpServers` object in
   `~/.kiro/settings/mcp.json` or the project's `.kiro/settings/mcp.json`.
4. Add `MCP_API_TOKEN` to `kiroAgent.mcpApprovedEnvVars` in Kiro user settings.
5. Ensure the Kiro process receives the variable, then quit and reopen Kiro completely.

For BPMN, also add the separate draw.io server entry shown in the
[BPMN installation guide](bpmn-creator/README.md#installation).

Platform-specific key storage, direct-URL configuration, connectivity checks, rotation, upgrades,
and diagnostics are maintained in the [MCP client runbook](RUNBOOK.md). Before a shared or CI
rollout, review the linked package metadata and pin each bridge to an exact approved version;
`@latest` intentionally checks for a newer bridge when the client starts.

## Architecture

![Registry architecture: local MCP client and uvx bridge, API Gateway with x-api-key, four Lambda MCP servers, DynamoDB sessions, S3 presigned scaffold assets, and the team-side Git and pipeline boundary](../../docs/diagrams/registry-architecture.drawio.png)

Workflow diagrams are in the server guides. Editable sources are in
[`docs/diagrams/`](../../docs/diagrams/).

The bridge reads JSON-RPC messages from stdin, sends tool arguments to the hosted service over HTTPS,
and writes responses to stdout. Diagnostics use stderr. Sessions are represented by service-managed
identifiers and state; they are not persistent transport connections.

## Common tool pattern

The servers share a core pattern, but their tool sets and sessions are not interchangeable.
`<prefix>` is `cicd`, `html`, `bpmn`, or `deck`.

| Tool pattern | Purpose | Availability |
| --- | --- | --- |
| `<prefix>_start` | Start a workflow session | All servers |
| `<prefix>_step_get` | Retrieve the current step and its references | All servers |
| `<prefix>_step_submit` | Submit findings and advance | All servers |
| `<prefix>_step_skip` | Skip a step marked optional | All servers |
| `<prefix>_session_status` | Retrieve resumable session status | All servers |
| `<prefix>_run_log` | Record an iteration and result | All servers |
| `<prefix>_request_draft` | Draft a request for work outside the user's control | All servers |
| `<prefix>_catalogue_list`, `_reference_get`, `_asset_get` | Retrieve hosted references and templates | All servers |
| `<prefix>_gate_confirm` | Record a human decision at a workflow gate | DevSecOps, HTML, and deck only |

BPMN has no `gate_confirm` tool; user review occurs in workflow step 6. Each server also provides
specialized tools such as `cicd_changeset_validate`, `html_scaffold_manifest`, `bpmn_validate`,
`deck_scaffold_manifest`, and `deck_text_map`.

## Operational boundaries

- The local client may run approved read-only AWS discovery with credentials on the user's machine.
- The hosted service does not receive local AWS credentials, call AWS on the user's behalf, push
  source code, or deploy applications.
- Tool arguments are transmitted to the hosted service. Validation tools inspect the supplied data;
  they do not directly read the user's local filesystem.
- File creation, local builds, source-control operations, and deployment remain under local approval
  and independent repository or pipeline controls.
- Human gates record a person's decision; they are not substitutes for required repository or
  pipeline approvals.

## Data handling and privacy

Do not send secrets, credentials, or regulated or sensitive data unless the organization has approved
the service for that use. This repository does not document retention, service-side logging, or
data-residency guarantees. Obtain those details from the deploying organization or service owner
before submitting data with specific handling requirements.

## License

Apache-2.0. See [LICENSE](../../LICENSE).
