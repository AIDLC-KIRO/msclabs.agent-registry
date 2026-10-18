# msclabs.devsecops-cicd

[![PyPI](https://img.shields.io/pypi/v/msclabs.devsecops-cicd-mcp-server)](https://pypi.org/project/msclabs.devsecops-cicd-mcp-server/)

A hosted MCP server for the **AI-DLC DevSecOps CI/CD deploy workflow** — taking an application
from source to a green pipeline, with the CoE's policy packs applied to every file before it is
pushed.

## Features

- **Read-only discovery** — reads the account, pipeline, region and network you actually have before proposing anything
- **Evidence-bound assessment** — every claim about the codebase is checked against the code, with a source
- **Policy validation before push** — `cicd_changeset_validate` runs the CoE packs over files you are about to write
- **Approval gates** — three named decision points: the application identity, the target region, the change set
- **Pipeline triage** — reads pipeline state, iterates on failing actions, and renders a status page
- **Request drafting** — produces the ask for another team when something is outside your permissions

## Prerequisites

1. The [common prerequisites](../README.md#prerequisites) — `uv`, Python 3.10+, an API key
2. AWS credentials on your machine with read access to the target account, for discovery
3. Push rights on the application repository, and a person who can approve the push

## Installation

```json
{
  "mcpServers": {
    "msclabs.devsecops-cicd": {
      "command": "uvx",
      "args": ["msclabs.devsecops-cicd-mcp-server==1.1.0"],
      "env": { "MCP_API_TOKEN": "${MCP_API_TOKEN}" }
    }
  }
}
```

Environment variables are listed in the [registry README](../../../README.md#environment-variables).

## Available tools

### Session

| Tool | Description |
| --- | --- |
| `cicd_start` | Open a session for the repository being deployed, as `org/repo` |
| `cicd_step_get` | Instructions, references and gate questions for a step |
| `cicd_step_submit` | Record findings and advance; held back if required findings are missing |
| `cicd_step_skip` | Skip a step the workflow marks optional, with a reason |
| `cicd_gate_confirm` | Record the answer a human gave at a gate and unlock what is behind it |
| `cicd_session_status` | Current step, confirmed gates and facts, files reported, rounds logged |
| `cicd_run_log` | Log one iterate-and-verify round; three identical causes stop the session |

### Policy and validation

| Tool | Description |
| --- | --- |
| `cicd_policy_get` | The policy packs in force: naming, writable paths, IaC limits, artifact contract, gate severities |
| `cicd_changeset_validate` | Run those packs over the files you are about to write; returns every finding with severity and owner |

### Content

| Tool | Description |
| --- | --- |
| `cicd_catalogue_list` | Every step, reference, template and script this server serves, with their paths |
| `cicd_reference_get` | One reference document, or one numbered section of it |
| `cicd_asset_get` | One template to adapt; `{{PLACEHOLDER}}` markers must be filled from evidence |

### Reporting

| Tool | Description |
| --- | --- |
| `cicd_render_pipeline_status` | Turn `aws codepipeline get-pipeline-state` output into a self-contained HTML status page |
| `cicd_request_draft` | Draft the request to send when something is outside what your team can do |

## Workflow

| Step | What happens |
| --- | --- |
| 1 Plan | Confirm the application name and language. Every later file depends on these. **GATE 1** |
| 2 Get resources | Read the real account, pipeline shape, region and network, read-only |
| 3 Discover | Read the AI-DLC documents and collect every claim with its source, to check against code in step 4. **GATE 2** |
| 4 Assess | Inspect the workspace part by part: what exists, whether it matches the claims, whether it passes the contract, who must fix what |
| 5 Prepare | Write the whole change set — buildspecs, portability fixes, IaC, per-environment values, the git plan, and the team actions that block the push. **GATE 3** |
| 6 Generate | Write the approved files and verify locally, before anything is pushed |
| 7 Deploy | Push to dev once the team agrees, watch, and iterate on every failing action until the pipeline is green |
| 8 Summary | URLs, per-action results, what was changed, and what the team still owes |

## Usage

```text
Deploy repo my-org/my-service to the dev pipeline
The pipeline is red, can you look at it
```

Validate files against policy at any point, without waiting for step 5:

```text
Run the CoE policy packs over the buildspecs I just wrote
```

## Gates

| Gate | The question | Why it stops here |
| --- | --- | --- |
| 1 | Application name and language | Every generated file is named and shaped from these two values |
| 2 | Which region you intend to deploy to | The server compares your answer with the pipeline's real configuration and refuses to continue if they disagree |
| 3 | The change set | The last point before files are written and pushed |

## Limitations

The server does not call AWS for you and cannot deploy. Deployment happens only through
`git push` from your own repository, after your team's explicit approval. Everything here is
advice, generated files, and policy findings.

Never pass a secret value to a tool. Pass the name of the SSM parameter or Secrets Manager
entry instead.

## License

Apache-2.0. See [LICENSE](../../../LICENSE).
