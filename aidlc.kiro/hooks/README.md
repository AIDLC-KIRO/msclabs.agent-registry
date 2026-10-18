# Hooks

Agent hooks for `.kiro/hooks/`. No entries yet.

A hook runs automatically when something happens in the editor — a file is saved, a tool is about
to run, a task completes — so a check does not depend on anyone remembering it.

## Layout

```
hooks/<hook-id>.json     the hook
hooks/<hook-id>.md       what it does, when it fires, and its side effects
```

```json
{
  "version": "v1",
  "hooks": [{
    "name": "Lint on save",
    "trigger": "PostFileSave",
    "matcher": "\\.(ts|tsx)$",
    "action": { "type": "command", "command": "npm run lint" }
  }]
}
```

### Triggers

`SessionStart`, `UserPromptSubmit`, `PreToolUse`, `PostToolUse`, `Stop`, `PreTaskExec`,
`PostTaskExec`, `PostFileCreate`, `PostFileSave`, `PostFileDelete`

`matcher` is an optional regex, tested against the tool name for `PreToolUse` and `PostToolUse`,
against the file path for the `PostFile*` triggers, and ignored otherwise.

### Actions

| Type | Behaviour |
| --- | --- |
| `command` | Runs a shell command and receives session context as JSON on stdin |
| `agent` | Appends a fixed prompt to the model's context |

Exit codes for `command`: `0` succeeds, and stdout is forwarded for `SessionStart`,
`UserPromptSubmit` and `PreToolUse`. `2` blocks the action for `PreToolUse`, `UserPromptSubmit`
and `PreTaskExec`, forwarding stderr. Anything else fails silently without blocking.

## Installation

Copy the `.json` file to `.kiro/hooks/` and confirm it appears in the Agent Hooks panel.

Hooks run commands on your machine, with your permissions, in a folder you have trusted. Read a
hook before installing it.

## Contributing

Open a pull request against `main`. A hook needs:

- a command that can be read and understood in full — no fetching and executing a remote script
- no transmission of source code or secrets off the machine
- a stated failure mode: what happens when the command is missing or the check fails
- a `matcher` narrow enough that it does not fire on unrelated files

Prefer a hook that reports over one that blocks, unless blocking is the point.
