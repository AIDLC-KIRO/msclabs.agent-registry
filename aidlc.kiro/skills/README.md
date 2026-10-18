# Skills

Agent skills distributed by the MSC Labs CoE. No entries yet.

## Layout

```
skills/<skill-name>/
  README.md      what it does, how to install it, example prompts
  SKILL.md       frontmatter (name, description) then the instructions
  references/    documents SKILL.md points at, if any
  scripts/       helper scripts, if any
```

## Installation

Copy the skill directory to `.kiro/skills/<skill-name>/` for one project, or
`~/.kiro/skills/<skill-name>/` for every project. Start a new session afterwards; a running
session does not pick up a new skill.

If a skill does not activate on its own, name it in the prompt: "use the \<skill-name\> skill
to …". Intent matching is not guaranteed.

## Contributing

Open a pull request against `main`. A skill needs:

- a `description` specific enough to trigger on the right requests and stay quiet otherwise
- instructions that work without the authoring machine's context
- no secret, account ID, ARN or internal endpoint

Workflows that must enforce policy or hold an approval gate belong in [`../mcp`](../mcp) as a
hosted server instead. A skill lives on a laptop and can be edited; a guardrail that can be
edited by the person it constrains is not a guardrail.
