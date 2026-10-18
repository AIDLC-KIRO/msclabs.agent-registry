# Runbook

Operating the MSC Labs MCP servers from a developer machine: install, verify, upgrade, rotate a
key, and diagnose a failure.

Base URL: `https://rh7x5fl9j3.execute-api.ap-southeast-7.amazonaws.com`

## 1. Prerequisites

| Requirement | Check |
| --- | --- |
| uv / uvx | `uvx --version` |
| Python 3.10+ | uv installs one if needed: `uv python install 3.10` |
| An API key from the CoE | shaped `aidlcmcp_<12 chars>_<long random part>` |
| Outbound HTTPS to the base URL | step 4 below |
| draw.io MCP and Node.js | `bpmn-creator` only |

Install uv:

```bash
# macOS, Linux, WSL
curl -LsSf https://astral.sh/uv/install.sh | sh
```

```powershell
# Windows
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

## 2. Set the API key

One key per consumer — per person, or per automated job. A key owns the sessions it opens, so a
shared key means shared sessions.

### macOS, Linux, WSL

```bash
mkdir -p ~/.aidlc
printf '%s' 'PASTE_YOUR_KEY' > ~/.aidlc/mcp-token
chmod 600 ~/.aidlc/mcp-token
echo 'export MCP_API_TOKEN=$(cat ~/.aidlc/mcp-token)' >> ~/.zshrc
```

### Windows

```powershell
setx MCP_API_TOKEN "PASTE_YOUR_KEY"
[Environment]::GetEnvironmentVariable('MCP_API_TOKEN','User')   # confirm it stuck
```

The bridge reads `MCP_API_TOKEN` first, then `MSCLABS_MCP_TOKEN`.

## 3. Configure the client

### 3.1 MCP configuration

Open the command palette, run `Kiro: Open user MCP config (JSON)`, and merge the three entries
from [`mcp.json`](mcp.json) into the `mcpServers` object already there. Do not nest a second
`mcpServers`.

Editing this file from a PowerShell script needs `-Encoding utf8`; a bare `Set-Content` writes an
encoding the client cannot read.

### 3.2 Approve the variable name

Run `Preferences: Open User Settings (JSON)` and add — or extend, if the key exists:

```json
"kiroAgent.mcpApprovedEnvVars": ["MCP_API_TOKEN"]
```

This step is not optional. Without it the client never substitutes `${MCP_API_TOKEN}` and you get
the misleading error in [section 8](#8-troubleshooting).

### 3.3 Restart completely

- macOS: `Cmd+Q`, then reopen. Reload Window is not enough.
- Windows: close every window, confirm in Task Manager that no Kiro process remains, then reopen.

A process inherits its environment only at launch. If you are unsure the restart was complete,
launch from a terminal, which passes the shell's environment directly:

```bash
kiro ~/path/to/your/project
```

## 4. Verify

In the client, open the MCP Server view. All three should report Connected with 14, 14 and 12
tools.

From a terminal, before opening the client:

```bash
B=https://rh7x5fl9j3.execute-api.ap-southeast-7.amazonaws.com

# Health needs no key.
curl -s "$B/devsecops-cicd/health"

# 200 means the key works; 401 means it is wrong or revoked.
curl -s -o /dev/null -w "%{http_code}\n" -X POST "$B/devsecops-cicd/mcp" \
  -H "Authorization: Bearer $MCP_API_TOKEN" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'
```

Test the bridge itself, end to end:

```bash
echo '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}' \
  | uvx msclabs.devsecops-cicd-mcp-server==1.1.0
```

Expect a JSON object containing `result.tools` on stdout, and a `bridging stdio to …` line on
stderr. Replace `devsecops-cicd` with `html-creator` or `bpmn-creator` for the others.

## 5. Environment variables

| Variable | Description | Default |
| --- | --- | --- |
| `MCP_API_TOKEN` | Your API key. Required. | — |
| `MSCLABS_MCP_TOKEN` | Alternative name for the key | — |
| `MSCLABS_MCP_BASE_URL` | Point at a different deployment, such as a test stage | the CoE endpoint |
| `MSCLABS_MCP_TIMEOUT` | Seconds to wait for one call | `120` |

## 6. Upgrade and roll back

Versions are pinned with `==1.1.0` on purpose. `@latest` means every machine silently takes a new
bridge whenever one is published.

1. Check the current version in [README.md](README.md) or on PyPI
2. Change the number in `args` for each server
3. If uvx still serves the old build, clear its cache:
   `uv cache clean msclabs.devsecops-cicd-mcp-server`
4. Click Retry in the MCP Server view, or restart the client

Rolling back is the same procedure with the previous number.

Workflow content is updated server-side and reaches you without any package change. Upgrading the
package matters only when the bridge itself changes.

## 7. Rotate or revoke a key

| Situation | Action |
| --- | --- |
| Key is near expiry | Ask the CoE for a new one, replace it per section 2, restart the client |
| Key leaked, or the machine is lost | Tell the CoE to revoke it. Revocation applies on the next call and affects only that key |
| Moving to a new machine | Request a key for the new machine, then have the old one revoked |

Only a SHA-256 digest of each key is stored, so a lost key cannot be recovered. It has to be
reissued.

## 8. Troubleshooting

### `Dynamic Client Registration rejected (HTTP 404)`

Not an OAuth problem, despite how it reads. The client sent the header as the literal text
`Bearer ${MCP_API_TOKEN}` because the variable was never substituted, the server answered 401,
and the client then assumed OAuth and tried to register — for which there is no endpoint, hence
404.

Check, in order:

1. `MCP_API_TOKEN` is listed in `kiroAgent.mcpApprovedEnvVars`
2. The variable has a value in a newly opened terminal (`echo $MCP_API_TOKEN`)
3. The client was fully restarted — the most commonly missed step

### `No API key` in the server log

The bridge found neither `MCP_API_TOKEN` nor `MSCLABS_MCP_TOKEN` and exited with code 2. Set it
per section 2 and restart the client.

### `401` or `403 … the API key was rejected`

The key is truncated, mistyped, expired, revoked, or not scoped to that server. Ask the CoE to
check its status.

### `could not reach the registry`

The network cannot reach the endpoint. Check corporate proxy, VPN and firewall, then run the
health check in section 4.

### `uvx: command not found`, or the server never starts

The client cannot see `uvx` on `PATH`. Use an absolute path in `command`, for example
`/Users/<you>/.local/bin/uvx`, or add a `PATH` entry to that server's `env`.

### Calls time out

Raise `MSCLABS_MCP_TIMEOUT` in that server's `env`, for example `"300"`.

### A session stops on its own

`run_log` counted the same cause three times. This is deliberate: it stops an assistant from
guessing at a fix indefinitely. Find the real cause, then start a new session.

### Using a key without setting an environment variable

Paste the key in place of `${MCP_API_TOKEN}` in `mcp.json`. It works immediately, with no
restart. The cost is that the key now sits in a config file readable by anyone with access to the
machine. Fine for a trial, not for regular use, and never commit that file.

## 9. Getting help

Open an issue with:

- the server name and package version
- the `[msclabs.<server>]` lines from the MCP output panel
- the result of the health check in section 4
- when it happened

**Never attach an API key.** For a suspected key leak, contact the CoE directly rather than
opening a public issue.
