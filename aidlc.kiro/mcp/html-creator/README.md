# aidlc.html-creator

[![PyPI](https://img.shields.io/pypi/v/aidlc.html-creator-mcp)](https://pypi.org/project/aidlc.html-creator-mcp/)

A hosted Model Context Protocol (MCP) server that guides the creation of a bilingual Thai/English,
self-contained HTML documentation site from AWS Transform assessment outputs: comprehensive
codebase analysis (CCA), business rules extraction (BRE), and modernization readiness analysis
(MRA).

## Features

- **Hosted scaffold** — `html_scaffold_manifest` provides the site structure and asset manifest.
- **Offline output** — generated pages do not require a content delivery network (CDN).
- **Evidence-based content** — system claims include `file:line` citations; unknowns are identified
  as "not determined," and inferences as `INFERRED`.
- **Interface normalization** — OpenAPI 2/3 and Postman v2 inputs are converted to cited Markdown,
  with credential headers redacted from the normalized output.
- **Code-to-report assessment** — the local source is compared with assessment reports, and gaps
  are reported explicitly.

## Prerequisites

1. The [common prerequisites](../README.md#prerequisites): `uv`, Python 3.10 or later, and an access key.
2. An `ATXDocumentation/`, `business-rules-extraction/`, or MRA output on the local filesystem.
3. The source code described by the report.
4. Optional inputs such as OpenAPI/Swagger documents, Postman collections, or database schema DDL.

## Installation

```json
{
  "mcpServers": {
    "aidlc.html-creator": {
      "command": "uvx",
      "args": ["aidlc.html-creator-mcp@latest"],
      "env": { "MCP_API_TOKEN": "${MCP_API_TOKEN}" }
    }
  }
}
```

For an exact version, use `"args": ["aidlc.html-creator-mcp==1.0.0"]`. See
[Upgrade and roll back](../RUNBOOK.md#6-upgrade-and-roll-back). Environment variables are listed
in the [registry README](../../../README.md#environment-variables).

## Available tools

### Session

| Tool | Description |
| --- | --- |
| `html_start` | Start a session for an assessment documentation site |
| `html_step_get` | Retrieve instructions, references, and gate questions |
| `html_step_submit` | Record findings and advance when required findings are complete |
| `html_step_skip` | Skip an optional step with a reason |
| `html_gate_confirm` | Record a human's gate decision |
| `html_session_status` | Retrieve the current step, gates, facts, reported files, and logged rounds |
| `html_run_log` | Record an iteration and its result |

### Site generation and content

| Tool | Description |
| --- | --- |
| `html_scaffold_manifest` | Retrieve the site scaffold manifest and asset paths |
| `html_normalize_interfaces` | Normalize OpenAPI or Postman input into cited Markdown with credential headers redacted |
| `html_catalogue_list` | List hosted steps, references, templates, and scripts |
| `html_reference_get` | Retrieve a reference document or numbered section |
| `html_asset_get` | Retrieve a template whose placeholders must be completed from evidence |
| `html_script_get` | Retrieve the source of a bundled script for review |
| `html_request_draft` | Draft a request for an action outside the user's control |

## Workflow

| Step | Activity |
| --- | --- |
| 1 Job plan | Confirm the destination, job list, and collaboration method. **Gate 1** |
| 2 Get resources | Locate assessment reports, transform configuration, source, and supporting specifications |
| 3 Discover | Confirm the source repository, audience, scope, and page list. **Gate 2** |
| 4 Assess code | Compare source evidence with the report and identify coverage limitations |
| 5 Prepare | Confirm page content and obtain the scaffold. **Gate 3** |
| 6 Generate HTML | Populate, build, and review the site locally |

## Usage

```text
Build a documentation site from the ATX reports in ./ATXDocumentation
```

## Content requirements

The site must remain usable offline. Claims about the assessed system must be traceable to source
evidence. If a fact cannot be established, state the limitation rather than supplying an assumed
value.

## Boundaries and data handling

The hosted service supplies workflow guidance, references, normalization results, and scaffold
content. The local assistant reads source files, writes the site, and runs local checks. The hosted
service does not publish or host the generated site.

Normalization redacts credential headers from its output, but users must still review all input
before transmission and all output before commit. Do not send secrets or unapproved sensitive data.
See the [common data-handling guidance](../README.md#data-handling-and-privacy).

## License

Apache-2.0. See [LICENSE](../../../LICENSE).
