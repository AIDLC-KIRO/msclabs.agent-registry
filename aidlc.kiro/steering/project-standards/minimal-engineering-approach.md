---
inclusion: manual
---

# Minimal-Change Engineering Profile

Use this optional profile for maintenance or narrowly scoped delivery where the goal is to solve the
problem with the smallest coherent change. Do not use it to override architecture, security,
compliance, or documentation requirements.

## Principles

- **Solve the requested problem:** Avoid unrelated cleanup and speculative features.
- **Preserve established design:** Reuse existing patterns unless they are the cause of the problem.
- **Fix the cause:** Do not bypass validation, tests, policy checks, or failure handling.
- **Keep the change coherent:** Create every file needed for clear ownership, testing, operation, and
  maintenance; there is no arbitrary maximum file count.
- **Minimize dependencies:** Add a dependency only when its value outweighs maintenance and security
  cost.

## Decision process

1. Confirm the required behavior and current evidence.
2. Identify the smallest existing component that owns the behavior.
3. Modify that component and its directly affected tests or documentation.
4. Add a new abstraction only when duplication, coupling, or a stable boundary justifies it.
5. Run the most relevant validation and report anything not verified.

## Avoid false minimalism

A one-file solution is not simpler when it mixes unrelated responsibilities or makes testing and
operation harder. Keep separate files when the repository's architecture, security controls,
deployment tooling, or maintainability require separation.
