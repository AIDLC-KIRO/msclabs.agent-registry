# MCP client runbook

This runbook covers installation, verification, upgrade, access-key rotation, and diagnostics for
the MSC Labs hosted Model Context Protocol (MCP) services.

Base URL: `https://8a3gpe2ji0.execute-api.ap-southeast-7.amazonaws.com/v1`

The current clients are the `aidlc.*-mcp` packages. The former `msclabs.*-mcp-server` packages and
HTTP bearer-token configuration are retired. The current bridge sends credentials in the `x-api-key` header.
This repository does not document the service's authentication or authorization implementation;
therefore this runbook refers to the value as an access key or credential.

## 1. Prerequisites

| Requirement | Check |
| --- | --- |
| `uv` / `uvx` | `uvx --version` |
| Python 3.10 or later | `uv python install 3.10` |
| Access key | Obtain it through the route supplied by the deploying organization or service owner |
| Outbound HTTPS | Run the check in section 4 |
| draw.io MCP and Node.js | Required only for `bpmn-creator` |

Install `uv`:

```bash
# macOS, Linux, Windows Subsystem for Linux (WSL)
curl -LsSf https://astral.sh/uv/install.sh | sh
```

```powershell
# Windows
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

## 2. Store the access key

Use a separate key for each person or automated job where the service owner supports that model.
Do not put a raw key in `mcp.json` or commit it to source control.

### 2.1 macOS and zsh terminal sessions

The following setup prompts without displaying or recording the key in shell history, stores it in
a mode-600 file, and makes the variable available to new zsh terminal sessions:

```bash
mkdir -p ~/.aidlc
read -rs "MCP_API_TOKEN?Access key: " && printf '\n'
printf '%s' "$MCP_API_TOKEN" > ~/.aidlc/mcp-token
unset MCP_API_TOKEN
chmod 600 ~/.aidlc/mcp-token
echo 'export MCP_API_TOKEN=$(cat ~/.aidlc/mcp-token)' >> ~/.zshrc
source ~/.zshrc
```

A graphical application launched from Finder or the Dock does not normally inherit `.zshrc`.
Before launching Kiro from the graphical interface, set the variable for the current macOS login
session:

```bash
launchctl setenv MCP_API_TOKEN "$(cat ~/.aidlc/mcp-token)"
```

Quit Kiro with `Cmd+Q` before reopening it. Repeat `launchctl setenv` after signing out or restarting
macOS, unless your organization provides an approved persistent secret-management method.
Alternatively, launch Kiro from a terminal that already has the variable:

```bash
kiro ~/path/to/your/project
```

### 2.2 Linux and WSL

Use the zsh commands above when zsh is your shell. For another shell, place the equivalent export in
that shell's startup file and start the MCP client from an environment that receives it.

### 2.3 Windows

Enter the key at a secure prompt, convert it only for the environment-variable API, and remove the
PowerShell variables immediately afterward:

```powershell
$secureKey = Read-Host "Access key" -AsSecureString
$key = [System.Net.NetworkCredential]::new("", $secureKey).Password
[Environment]::SetEnvironmentVariable("MCP_API_TOKEN", $key, "User")
Remove-Variable key, secureKey
[Environment]::GetEnvironmentVariable("MCP_API_TOKEN", "User") -ne $null
```

This updates future processes, not currently running applications. Close every Kiro window, confirm
in Task Manager that no Kiro process remains, and then reopen Kiro. A Windows sign-out or restart
may be required if the new process still does not receive the variable.

The bridge checks `MCP_API_TOKEN` first and `MSCLABS_MCP_TOKEN` second.

## 3. Configure Kiro

### 3.1 MCP configuration

Run `Kiro: Open user MCP config (JSON)` from the command palette. Merge the four entries from
[`mcp.json`](mcp.json) into the existing `mcpServers` object. Do not create a nested second
`mcpServers` object, and do not replace `${MCP_API_TOKEN}` with a raw key.

When editing JSON from PowerShell, use UTF-8 encoding. A default `Set-Content` invocation can write
an encoding that the client cannot read.

### 3.2 Approve the variable name

Run `Preferences: Open User Settings (JSON)` and add or extend:

```json
"kiroAgent.mcpApprovedEnvVars": ["MCP_API_TOKEN"]
```

### 3.3 Restart completely

- macOS: quit with `Cmd+Q`, then reopen Kiro from the environment configured in section 2.
- Windows: close all windows, confirm no Kiro process remains, then reopen it.

Reloading a window is not sufficient because environment variables are inherited when the process
starts.

## 4. Verify connectivity and the key

In Kiro's MCP Server view, the four servers should report Connected with 14, 14, 12, and 16 tools.

The service has no documented unauthenticated health endpoint. The following `tools/list` request
checks network connectivity and whether the service accepts the supplied key; it does not establish
the service's broader authorization design.

```bash
B=https://8a3gpe2ji0.execute-api.ap-southeast-7.amazonaws.com/v1

curl -s -o /dev/null -w "%{http_code}\n" -X POST "$B/devsecops-cicd/mcp" \
  -H "x-api-key: $MCP_API_TOKEN" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'
```

Typical responses are `200` when the request is accepted, `403` when the key is rejected, and `429`
when a throttle or quota applies. A `429` can result from a per-key usage plan, but shared API,
stage, or account limits may also apply. Confirm the configured limits and service metrics before
assuming that other consumers are unaffected.

Test the bridge end to end:

```bash
echo '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}' \
  | uvx aidlc.devsecops-cicd-mcp@latest
```

Expect a JSON object containing `result.tools` on stdout and bridge diagnostics on stderr. Replace
`devsecops-cicd` with `html-creator`, `bpmn-creator`, or `deck-creator` to test another server.

## 5. Environment variables

| Variable | Description | Default |
| --- | --- | --- |
| `MCP_API_TOKEN` | Access key; required | — |
| `MSCLABS_MCP_TOKEN` | Alternative access-key variable | — |
| `MSCLABS_MCP_BASE_URL` | Alternative service deployment | CoE endpoint |
| `MSCLABS_MCP_TIMEOUT` | Request timeout in seconds | `120` |

## 6. Upgrade and roll back

| Form | `args` | Behavior |
| --- | --- | --- |
| Track latest | `["aidlc.devsecops-cicd-mcp@latest"]` | Checks for the newest bridge when the client starts |
| Pin | `["aidlc.devsecops-cicd-mcp==1.0.0"]` | Keeps each machine on an explicit bridge version |

Use exact versions for shared team or CI configuration where reproducibility is required. Use
`@latest` only where automatic bridge updates are intentional. Workflow and policy content remain
hosted in both cases.

To update or roll back a pinned version:

1. Confirm the intended published version.
2. Change each package version in `args`.
3. If necessary, clear the package cache, for example
   `uv cache clean aidlc.devsecops-cicd-mcp`.
4. Retry the server in Kiro or restart the client.

## 7. Rotate or revoke a key

This repository documents no automatic key expiry. Plan periodic rotation according to your
organization's policy rather than waiting for an expiry warning.

| Situation | Action |
| --- | --- |
| Planned rotation | Request a replacement through the organization-specific route, update section 2, restart Kiro, verify, then request revocation of the old key |
| Suspected disclosure or lost device | Use the private incident route supplied by the service owner and request immediate revocation |
| New device | Request a separate key if supported, verify it, and retire the previous key when appropriate |

The issuance, storage, propagation, and revocation implementation is not documented in this public
repository. Do not rely on a specific propagation interval or on assumptions about whether an
administrator can retrieve an existing value. Obtain operational details from the service owner.

## 8. Troubleshooting

### `Dynamic Client Registration rejected (HTTP 404)`

This can occur when the access-key variable is not expanded and the client subsequently attempts an
OAuth discovery or registration path that the service does not provide. Check that:

1. `MCP_API_TOKEN` appears in `kiroAgent.mcpApprovedEnvVars`.
2. The process that launches Kiro receives a non-empty variable.
3. Kiro was fully restarted after the variable was set.
4. On macOS, GUI-launched Kiro received the value through `launchctl`; a terminal-only `.zshrc`
   export is insufficient for Finder or Dock launches.

### `No API key` in the server log

The bridge found neither supported access-key variable. Set it as described in section 2 and restart
Kiro completely.

### `403 … the API key was rejected`

Check for a truncated, mistyped, or revoked value. If the value is correct, contact the service
owner; this repository does not document propagation timing or rejection diagnostics.

### `429`

Slow down and retry with backoff. A per-key usage plan is one possible cause. Shared API, stage, or
account limits may also cause the response. The service owner must inspect deployed limits and
metrics to identify the scope.

### `could not reach the registry`

Check the corporate proxy, virtual private network (VPN), firewall, and Domain Name System (DNS),
then run the connectivity check in section 4.

### `uvx: command not found`, or the server does not start

Use the absolute `uvx` path in `command`, or provide an appropriate `PATH` in the server environment.

### Calls time out

Increase `MSCLABS_MCP_TIMEOUT` for the affected server, for example to `"300"`.

### A session stops after repeated failures

Review the session status and run log, investigate the recorded cause, and resolve it before
starting another session.

## 9. Data handling, access, and support

JSON-RPC tool arguments are transmitted from the local bridge to the hosted service over HTTPS. Do
not send secrets or regulated or sensitive data unless your organization has approved the service
for that use. Retention, service-side logging, and data residency are not documented here; obtain
those details from the service owner.

No public access-key request, private incident contact, or guaranteed public support route is
documented in this repository. The deploying organization or service owner must provide those
organization-specific details. If public issues are enabled for your deployment, include only the
server name, package version, relevant redacted `[aidlc.<server>]` log lines, and the result of
section 4. Never include credentials, sensitive tool arguments, or unredacted logs in a public
issue.
