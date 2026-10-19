# aidlc.deck-creator

[![PyPI](https://img.shields.io/pypi/v/aidlc.deck-creator-mcp)](https://pypi.org/project/aidlc.deck-creator-mcp/)

A hosted Model Context Protocol (MCP) server that guides the creation of a self-contained HTML
presentation, executive summary, or progress report from project specifications.

## Features

- **Separated content and rendering** — presentation text is supplied through `overrides.json`;
  report content is supplied through `src/content/deck.js`. The scaffold controls rendering.
- **Offline output** — the generated deliverable is a single HTML file that does not require a
  network connection.
- **Evidence-based content** — specifications are the primary source; source-code assessment is an
  optional workflow step.
- **Local build checks** — `npm run check`, `npm run build`, and `npm run verify` validate the local
  project and output.
- **Hosted assets** — `deck_scaffold_manifest` provides asset paths and short-lived download URLs
  where an asset is too large or binary for a tool response.

## Prerequisites

1. The [common prerequisites](../README.md#prerequisites): `uv`, Python 3.10 or later, and an access key.
2. Node.js and `npm` for the local build.
3. Project specifications such as requirements, design documents, or `.kiro/specs/**`.

## Installation

```json
{
  "mcpServers": {
    "aidlc.deck-creator": {
      "command": "uvx",
      "args": ["aidlc.deck-creator-mcp@latest"],
      "env": { "MCP_API_TOKEN": "${MCP_API_TOKEN}" }
    }
  }
}
```

For an exact version, use `"args": ["aidlc.deck-creator-mcp==1.0.0"]`. See
[Upgrade and roll back](../RUNBOOK.md#6-upgrade-and-roll-back). Environment variables are listed
in the [registry README](../../../README.md#environment-variables).

## Available tools

### Session

| Tool | Description |
| --- | --- |
| `deck_start` | Start a session for a presentation or report |
| `deck_step_get` | Retrieve instructions, references, and gate questions |
| `deck_step_submit` | Record findings and advance when required findings are complete |
| `deck_step_skip` | Skip an optional step, including source-code assessment |
| `deck_gate_confirm` | Record a human's gate decision |
| `deck_session_status` | Retrieve the current step, gates, facts, reported files, and logged rounds |
| `deck_run_log` | Record an iteration and its result |
| `deck_request_draft` | Draft a request for an action outside the user's control |

### Scaffolding and content

| Tool | Description |
| --- | --- |
| `deck_new` | Create the initial scaffold data for the selected output type |
| `deck_scaffold_manifest` | Retrieve template assets and short-lived download URLs where applicable |
| `deck_text_map` | Retrieve editable presentation text slots and their override identifiers |
| `deck_check_overrides` | Check `overrides.json` against the hosted template contract |
| `deck_catalogue_list` | List hosted steps, references, templates, and scripts |
| `deck_reference_get` | Retrieve a hosted reference document or numbered section |
| `deck_asset_get` | Retrieve a template asset |
| `deck_script_get` | Retrieve the source of a bundled script for review |

## Workflow

| Step | Activity |
| --- | --- |
| 1 Job plan | Confirm language, output type, and destination. **Gate 1** |
| 2 Get resources | Confirm authoritative specifications and whether to assess source code. **Gate 2** |
| 3 Discover resources | Map source material to the proposed content and identify gaps |
| 4 Assess code | Add source-backed facts when specifications are insufficient. **Optional** |
| 5 Prepare | Plan the presentation or report and obtain approval. **Gate 3** |
| 6 Generate HTML | Populate the scaffold, build locally, verify, and review the output |

## Usage

```text
Build an AI-DLC presentation deck for this project
Write an executive summary from .kiro/specs/order-service
Build a progress report from the sprint notes in ./status
```

## Presentation template text

The presentation template keeps all 32 slide layouts, cards, diagrams and animations, but every
text slot holds placeholder wording (`Lorem ipsum…`, `ข้อความ ตัวอย่าง…`), sections are named
`หัวข้อ 1`–`หัวข้อ 7`, and the terminal demo is a placeholder recording. Supply all wording through
`overrides.json`; a slot left unchanged shows the placeholder. The deck controls (theme names,
navigation, contents overlay) are unchanged.

## Output types

| Output type | Purpose | Primary reader |
| --- | --- | --- |
| **HTML Presentation** | A structured deck populated with project-specific text | A presenter and live audience |
| **Executive Summary Report** | A concise scrolling report that can be read independently | An executive reader |
| **Progress Report** | A status-oriented report using a fixed status vocabulary | A sponsor reviewing delivery status |

The output-type reference is hosted. Use `deck_catalogue_list` to locate it and
`deck_reference_get` to retrieve it. Producing all three output types creates three distinct
structures from the same evidence; it does not wrap identical text in three formats.

## Boundaries and data handling

The hosted service provides workflow guidance, references, template contracts, and scaffold
assets. The assistant writes and builds the deliverable locally. Design changes outside the hosted
contract are not supported; unsupported content is reported as a gap rather than invented.

Tool arguments are sent over HTTPS. Do not include secrets, credentials, internal endpoints,
private addresses, personal data, or other unapproved sensitive information. See the
[common data-handling guidance](../README.md#data-handling-and-privacy).

## License

Apache-2.0. See [LICENSE](../../../LICENSE).
