# Completed examples: open after building

These are inactive answer-key files, not workshop setup. Copilot does not
discover agents or skills from this `reference` directory.

Build your own definitions by following [the modules](../README.md#workshop-route).
Each lab includes the content to write, explains the choices, and shows how to
use what you created. Do not bulk-copy this directory into `.github` at the
start; that skips the learning objective.

After completing a lab, compare your work with:

| Lab | Completed example |
|---|---|
| 1: Review skill and report template | [code-checklist](skills/code-checklist/SKILL.md) |
| 2: Code-review agent | [code-reviewer.agent.md](agents/code-reviewer.agent.md) |
| 3: Intake and approval skill | [review-handoff](skills/review-handoff/SKILL.md) |
| 3: Implementation and reporting skill | [safe-refactoring](skills/safe-refactoring/SKILL.md) |
| 4: Test-generation skill | [test-generation](skills/test-generation/SKILL.md) |
| 5: Dev-workflow agent | [dev-workflow.agent.md](agents/dev-workflow.agent.md) |
| 7: Issue-resolver agent | [issue-resolver.agent.md](agents/issue-resolver.agent.md) |

The checklist skill is created first in Module 1. The reviewer in Module 2
explicitly uses that existing skill from its first version. Module 3 creates
both refactoring skills and their templates. Module 4 creates the
test-generation skill. Neither module runs these skills.
Module 5 runs them through one dev-workflow agent, with approval before
refactoring and again before test generation.
Module 7 defines a standalone debugging procedure in the issue-resolver agent:
diagnose a human-selected GitHub issue's root cause, propose a minimal fix,
and implement it after approval without unrelated refactoring or publishing.
It does not require the review/refactoring skills.
Your wording may differ. Compare behavior, report
contracts, and boundaries, not byte-for-byte equality.
