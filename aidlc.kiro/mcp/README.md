# MCP servers

MSC Labs Center of Excellence (CoE) hosts four Model Context Protocol (MCP) workflow servers in
AWS Asia Pacific (Thailand), `ap-southeast-7`. The published PyPI packages are local standard
input/output (stdio) bridges. Workflow steps, policy, and reference content remain hosted.

| Server | Package | Version | Tools | Documentation |
| --- | --- | --- | --- | --- |
| `aidlc.devsecops-cicd` | [aidlc.devsecops-cicd-mcp](https://pypi.org/project/aidlc.devsecops-cicd-mcp/) | 1.0.0 | 14 | [README](devsecops-cicd/README.md) |
| `aidlc.html-creator` | [aidlc.html-creator-mcp](https://pypi.org/project/aidlc.html-creator-mcp/) | 1.0.0 | 14 | [README](html-creator/README.md) |
| `aidlc.bpmn-creator` | [aidlc.bpmn-creator-mcp](https://pypi.org/project/aidlc.bpmn-creator-mcp/) | 1.0.0 | 12 | [README](bpmn-creator/README.md) |
| `aidlc.deck-creator` | [aidlc.deck-creator-mcp](https://pypi.org/project/aidlc.deck-creator-mcp/) | 1.0.0 | 16 | [README](deck-creator/README.md) |

[`mcp.json`](mcp.json) tracks `@latest`. For reproducible team or continuous integration (CI)
configuration, replace each package argument with an exact version, for example
`"aidlc.devsecops-cicd-mcp==1.0.0"`. See [Upgrade and roll back](RUNBOOK.md#6-upgrade-and-roll-back).
The former `msclabs.*-mcp-server` packages are retired.

## Prerequisites

1. Kiro IDE, the documented and tested client. Other stdio MCP clients may work but can require
   client-specific command, environment-variable, and variable-expansion configuration.
2. [uv](https://docs.astral.sh/uv/getting-started/installation/) for `uvx`.
3. Python 3.10 or later (`uv python install 3.10`).
4. An access key from the service owner; see [Getting access](../../README.md#getting-access).
5. Outbound HTTPS access to `*.execute-api.ap-southeast-7.amazonaws.com`.
6. For `bpmn-creator` only, Node.js and the
   [draw.io MCP server](https://www.npmjs.com/package/@drawio/mcp).

## Installation

1. Set `MCP_API_TOKEN` without placing the raw value in `mcp.json`.
2. Merge the four entries from [`mcp.json`](mcp.json) into the existing `mcpServers` object in
   `~/.kiro/settings/mcp.json` or a project's `.kiro/settings/mcp.json`.
3. Add `MCP_API_TOKEN` to `kiroAgent.mcpApprovedEnvVars` in Kiro user settings.
4. Ensure the Kiro process receives the variable, then quit and reopen Kiro completely.

Platform-specific setup, verification, rotation, upgrades, and diagnostics are in the
[runbook](RUNBOOK.md).

## Architecture

![Registry architecture: local MCP client and uvx bridge, API Gateway with x-api-key, four Lambda MCP servers, DynamoDB sessions, S3 presigned scaffold assets, and the team-side Git and pipeline boundary](../../docs/diagrams/registry-architecture.drawio.png)

Workflow diagrams for each server are in the server READMEs; sources are in [`docs/diagrams/`](../../docs/diagrams/).

The bridge reads JavaScript Object Notation Remote Procedure Call (JSON-RPC) messages from stdin,
sends tool arguments to the hosted service over HTTPS with the current bridge's `x-api-key`
request header, and writes responses to stdout. Diagnostics use stderr. The hosted servers use stateless
request/response transport; workflow sessions are represented by service-managed identifiers and
state rather than a persistent transport connection.

Server-side hosting prevents a user from changing the hosted workflow or policy locally.
Independent pipeline controls determine whether generated changes can be merged or deployed.

## Common tool pattern

The servers share a core pattern, but their tool sets and workflow sessions are not identical.
`<prefix>` is `cicd`, `html`, `bpmn`, or `deck`.

| Tool pattern | Purpose | Availability |
| --- | --- | --- |
| `<prefix>_start` | Start a workflow session | All servers |
| `<prefix>_step_get` | Retrieve the current step and its references | All servers |
| `<prefix>_step_submit` | Submit required findings and advance | All servers |
| `<prefix>_step_skip` | Skip a step that the workflow marks optional | All servers |
| `<prefix>_session_status` | Retrieve resumable session status | All servers |
| `<prefix>_run_log` | Record an iteration and its result | All servers |
| `<prefix>_request_draft` | Draft a request for work outside the user's control | All servers |
| `<prefix>_catalogue_list`, `_reference_get`, `_asset_get` | Retrieve hosted references and templates | All servers |
| `<prefix>_gate_confirm` | Record a human decision at a workflow gate | DevSecOps, HTML, and deck only |

BPMN is the exception: it has no `gate_confirm` tool and performs user review in workflow step 6.
Each server also provides specialized tools, including `cicd_changeset_validate`,
`html_scaffold_manifest`, `bpmn_validate`, `deck_scaffold_manifest`, and `deck_text_map`.

## Operational boundaries

- The local client or assistant may run read-only AWS commands with credentials available on the
  user's machine when a workflow requires local discovery.
- The hosted MCP service does not receive local AWS credentials, call AWS on the user's behalf,
  push source code, or deploy an application.
- Tool arguments are transmitted to the hosted service. For example, policy-validation tools
  evaluate the proposed change-set data supplied in their arguments; they do not directly read the
  user's local filesystem.
- File creation, validation with local build tools, source-control operations, and deployment
  remain under the user's local environment and independent pipeline controls.
- Human gates record decisions supplied by a person; they are not substitutes for repository or
  pipeline approvals.

## Data handling and privacy

JSON-RPC tool arguments are sent from the local bridge to the hosted service over HTTPS. Do not
send secrets, credentials, or regulated or sensitive data unless your organization has approved
the service for that use. This repository does not document retention, service-side logging, or
data residency guarantees. Obtain those details from the deploying organization or service owner
before submitting data that requires specific handling.

## License

Apache-2.0. See [LICENSE](../../LICENSE).
