# msclabs.bpmn-creator

[![PyPI](https://img.shields.io/pypi/v/msclabs.bpmn-creator-mcp-server)](https://pypi.org/project/msclabs.bpmn-creator-mcp-server/)

A hosted MCP server for mapping a **business process to a BPMN 2.0 swimlane diagram** — one lane
per department, role or system — saved as a `.drawio` file, then refined through per-department
review until it matches how the work actually happens.

Works for any process: ERP and approval flows, onboarding, order-to-cash, factory or government
procedures.

## Features

- **Workspace first** — reads the specs, documents and code you already have before asking you anything
- **One question at a time** — interviews with A–D plus Other options, answered in chat, in a questionnaire file, or skipped entirely
- **A model, not a picture** — `process-model.md` holds lanes, steps, inputs, outputs, systems, rules, SLAs and open questions, and is the source of truth the diagram is generated from
- **Validation that catches what the eye misses** — `bpmn_validate` finds invalid XML, duplicate ids, edges with missing ends
- **Review loop built in** — per-department forms feed answers back into the model for v2, v3, with a change log

## Prerequisites

1. The [common prerequisites](../README.md#prerequisites) — `uv`, Python 3.10+, an API key
2. **The [draw.io MCP server](https://www.npmjs.com/package/@drawio/mcp) and Node.js.** This
   server validates diagrams but does not draw them. Without draw.io, nothing is drawn.

## Installation

Both servers are needed:

```json
{
  "mcpServers": {
    "msclabs.bpmn-creator": {
      "command": "uvx",
      "args": ["msclabs.bpmn-creator-mcp-server==1.1.0"],
      "env": { "MCP_API_TOKEN": "${MCP_API_TOKEN}" }
    },
    "drawio": {
      "command": "npx",
      "args": ["-y", "@drawio/mcp@1.7.0"]
    }
  }
}
```

Environment variables are listed in the [registry README](../../../README.md#environment-variables).

## Available tools

### Session

| Tool | Description |
| --- | --- |
| `bpmn_start` | Open a session for the process being mapped |
| `bpmn_step_get` | Instructions and references for a step |
| `bpmn_step_submit` | Record findings and advance; held back if required findings are missing |
| `bpmn_step_skip` | Skip a step the workflow marks optional — step 3, the interview, is the usual one |
| `bpmn_session_status` | Current step, confirmed facts, files reported, rounds logged |
| `bpmn_run_log` | Log one iterate-and-verify round; three identical causes stop the session |

This server has no `gate_confirm` tool. Review happens in step 6, by walking the paths with the
people who do the work.

### Validation

| Tool | Description |
| --- | --- |
| `bpmn_validate` | Validate swimlane XML with the CoE's validator: invalid XML, duplicate ids, edges with missing ends |

### Content

| Tool | Description |
| --- | --- |
| `bpmn_catalogue_list` | Every step, reference, template and script this server serves |
| `bpmn_reference_get` | One reference document, or one numbered section of it |
| `bpmn_asset_get` | One template to adapt; `{{PLACEHOLDER}}` markers must be filled from evidence |
| `bpmn_script_get` | The source of a bundled script, when you need to read what it does |
| `bpmn_request_draft` | Draft the request to send when something is outside what you can do |

## Workflow

| Step | What happens |
| --- | --- |
| 1 Explore workspace | Read what already exists, so you do not ask what you could have found |
| 2 Scope | Confirm the context found in step 1, then ask only about the gaps |
| 3 Interview | Collect what only people know, one question at a time with options. **Optional** |
| 4 Model | Record lanes, steps, types, inputs, outputs, systems, rules, SLAs and open questions in `process-model.md` |
| 5 Draw | Turn the model into a swimlane `.drawio` that still reads well once exported |
| 6 Review | Walk every path from Start to End with the user, failure paths included, in sections |
| 7 Department forms | One review form per department, answered by the people who do that work daily |
| 8 Iterate | Feed the answers back into the model, redraw, and keep a change log of what changed and why |

## Usage

```text
Map the leave request process as BPMN
```

Everyday wording works — process map, workflow, as-is/to-be, swimlane, process interviews,
department questionnaires. Skip straight to drawing with:

```text
Skip the interview, just draw it
```

## Working with diagrams

Validate after every draw. And do not claim a page has no overlapping edges unless you have
actually looked at its exported image — the validator cannot see layout.

## Limitations

The drawing itself is done by the draw.io MCP server, which is a separate project, not part of
this registry. `process-model.md` is the source of truth; if the model and the diagram disagree,
the model wins and the diagram is regenerated.

## License

Apache-2.0. See [LICENSE](../../../LICENSE).
