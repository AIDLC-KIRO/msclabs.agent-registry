# msclabs.html-creator

[![PyPI](https://img.shields.io/pypi/v/msclabs.html-creator-mcp-server)](https://pypi.org/project/msclabs.html-creator-mcp-server/)

A hosted MCP server that turns **AWS Transform assessment reports** — comprehensive codebase
analysis (CCA), business rules extraction (BRE), modernization readiness analysis (MRA) — into a
bilingual Thai/English documentation site that opens from the filesystem, months later, on a
machine with no internet.

## Features

- **Scaffold on demand** — `html_scaffold_manifest` returns the whole site skeleton; you never assemble it by hand
- **Fully self-contained output** — no page references a CDN, because the reader may have no route to one
- **Cited content only** — every claim about the system carries a `file:line`; unknowns are written as "not determined" and inferences are labelled `INFERRED`
- **Interface normalization with redaction** — OpenAPI 2/3 and Postman collections become cited Markdown with auth headers stripped before anything is written
- **Code-vs-report assessment** — the repository is analysed against the report, and coverage is stated plainly rather than implied

## Prerequisites

1. The [common prerequisites](../README.md#prerequisites) — `uv`, Python 3.10+, an API key
2. The assessment output on disk — an `ATXDocumentation/`, `business-rules-extraction/` or MRA report
3. The source code the report describes, so claims can be checked
4. Optional supporting inputs: OpenAPI/Swagger specs, Postman collections, schema DDL

## Installation

```json
{
  "mcpServers": {
    "msclabs.html-creator": {
      "command": "uvx",
      "args": ["msclabs.html-creator-mcp-server==1.1.0"],
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
| `html_start` | Open a session for the assessment being turned into a site |
| `html_step_get` | Instructions, references and gate questions for a step |
| `html_step_submit` | Record findings and advance; held back if required findings are missing |
| `html_step_skip` | Skip a step the workflow marks optional, with a reason |
| `html_gate_confirm` | Record the answer a human gave at a gate and unlock what is behind it |
| `html_session_status` | Current step, confirmed gates and facts, files reported, rounds logged |
| `html_run_log` | Log one iterate-and-verify round; three identical causes stop the session |

### Site generation

| Tool | Description |
| --- | --- |
| `html_scaffold_manifest` | The scaffold in two parts: text files listed with asset paths, binaries fetched separately |
| `html_normalize_interfaces` | Convert OpenAPI 2/3 or a Postman v2 collection into cited Markdown, credentials redacted |

### Content

| Tool | Description |
| --- | --- |
| `html_catalogue_list` | Every step, reference, template and script this server serves |
| `html_reference_get` | One reference document, or one numbered section of it |
| `html_asset_get` | One template to adapt; `{{PLACEHOLDER}}` markers must be filled from evidence |
| `html_script_get` | The source of a bundled script, when you need to read what it does |
| `html_request_draft` | Draft the request to send when something is outside what you can do |

## Workflow

| Step | What happens |
| --- | --- |
| 1 Job plan | Agree the destination folder, the job list and how you will work together. **GATE 1** |
| 2 Get resources | Locate the ATX reports, transform config, source code and supporting specs |
| 3 Discover | Identify the source repository, confirm the audience, the scope and the page list. **GATE 2** |
| 4 Assess code | Analyse the repository against the report; every claim gets a citation, and coverage is stated honestly |
| 5 Prepare | Confirm the page set and what each page will hold, then lay down the scaffold. **GATE 3** |
| 6 Generate HTML | Fill the scaffold, build the embedded content, verify, and read the result as a reader would |

## Usage

```text
Build a documentation site from the ATX reports in ./ATXDocumentation
```

## The two rules this workflow will not relax

**The site must open offline.** No page may point at a CDN. The deliverable is opened months
after the engagement ends, often on a machine with no route to the internet.

**Nothing enters the site that is not in the source.** A claim about the system carries a
`file:line` citation. An unknown is written as "not determined". An inference is labelled
`INFERRED`. One fabricated detail costs the reader their trust in everything else on the site.

## Limitations

The server returns the scaffold, references and normalized interface documents; your assistant
writes the files in your workspace. It does not publish or host the site.

Normalization redacts auth headers, but review the output before committing it. Never pass a
secret value to a tool.

## License

Apache-2.0. See [LICENSE](../../../LICENSE).
