# Completed examples: open after building

These are inactive answer-key files, not workshop setup. Copilot does not
discover agents or skills from this `reference` directory.

Build your own definitions by following [the modules](../README.md#workshop-modules).
Each lab includes the content to write, explains the choices, and shows how to
use what you created. Do not bulk-copy this directory into `.github` at the
start; that skips the learning objective.

After completing a lab, compare your work with:

| Lab | Completed example |
|---|---|
| 1.1: Review skill and report template | [code-checklist](skills/code-checklist/SKILL.md) |
| 1.2: Review-refactor agent | [review-refactor.agent.md](agents/review-refactor.agent.md) |
| 2.2: Issue-resolver agent | [issue-resolver.agent.md](agents/issue-resolver.agent.md) |

Part 1 creates the checklist skill in Module 1.1, then reuses it in the
review-refactor agent in Module 1.2. The agent saves review and plan reports,
waits for implementation approval, and makes small edits without executing code.

Part 2 uses GitHub MCP with the default agent in Module 2.1, then creates the
issue-resolver in Module 2.2. It diagnoses a selected issue's root cause and
implements an approved minimal fix without unrelated refactoring or publishing.
It does not require Part 1's skill.

Additional examples retained for the archived exercises:

- [Code-reviewer agent](agents/code-reviewer.agent.md)
- [Review-handoff skill](skills/review-handoff/SKILL.md)
- [Safe-refactoring skill](skills/safe-refactoring/SKILL.md)
- [Dev-workflow agent](agents/dev-workflow.agent.md)
- [Test-generation skill](skills/test-generation/SKILL.md)

Your wording may differ. Compare behavior, report
contracts, and boundaries, not byte-for-byte equality.
