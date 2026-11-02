# Review of the reference workshop

Reference: [syash-git/agents-and-skills-workshop](https://github.com/syash-git/agents-and-skills-workshop)

Inspected on October 20, 2026. The default branch was `master`; inspected commit:
`47646a819ad11c1ad49891d72902565099a4ef14`.

## What the repository teaches

The root README offers Python, JavaScript, and C# book-collection starters.
The main modules progress from a custom reviewer, to a reusable quality skill,
to running them together, followed by a separate GitHub MCP exercise.

The relevant source of truth for this workshop is:

| Reference file | What is retained here |
|---|---|
| `modules/01-custom-agent.md` | `code-reviewer`, evidence-led senior-engineer persona, Bug/Risk/Improvement severity vocabulary |
| `modules/02-custom-skill.md` | `code-checklist`, five categories in a fixed order, explicit no-finding sections, final overall assessment |
| `modules/03-combine-agent-and-skill.md` | Explicit reviewer selection with a checklist-matching prompt; skill supplies structure and agent supplies judgment |
| Root README's Python starter | Book-collection domain; the active sample now comes from Copilot-CLI-Dev-Workflow |

These are adaptations of the reference's teaching approach, not a wholesale
copy of its source or a claim of byte-for-byte equivalence.

## Important distinctions found during inspection

The separately supplied `samples/agents/python-reviewer.agent.md` and
`samples/skills/code-checklist/SKILL.md` are not identical to the main labs:
the former uses another severity vocabulary; the latter includes a testing
checklist and pytest expectations. There is also a separate pytest helper
agent and test-generation skill. Those pytest-based definitions are not brought
into this workshop. The selected
[book-app-project sample](../samples/book-app-project/README.md) comes from
[Copilot-CLI-Dev-Workflow](https://github.com/syash-git/Copilot-CLI-Dev-Workflow/tree/main/samples)
and already includes pytest tests. Module 4 defines a skill that extends them.

The main reviewer groups findings by severity while the main skill groups them
by category. The reference's composition lab resolves this by using checklist
categories with severity labels inside them. This workshop makes that precedence
explicit in both definitions.

The reference's main flow does not define a producer-independent report contract
or a standalone approval-aware refactoring consumer. Those are the additions here.

## Deliberate changes

- Pick Python as the single workshop track. Use `samples/book-app-project`
  and its existing pytest dependency; the alternate copied sample is not used.
- Start without active agent/skill definitions. Learners author two agents,
  four skills, and the supporting templates in creation-first labs.
  Completed examples stay in the inactive `reference` directory.
- Teach the checklist skill before the reviewer agent. The first module uses
  the skill with the default agent; the second creates the reviewer with its
  skill instruction included from the start. The four-part teaching format is
  retained, but the reference's agent-first order is deliberately reversed.
- Retain the five main-lab categories, including design-only Testability, but
  keep test-generation and test-runner activities out of the review/refactoring
  exercises. Module 4 defines the pytest skill; Module 5 runs test generation.
- Add stable finding IDs, exact source evidence, acceptance conditions, and
  behavior-change declarations to make reports actionable without identifying
  their producer.
- Save the review without editing source; require user approval before changes.
- Add separate handoff and refactoring skills, completion accounting, and
  optional follow-up review that preserves original IDs. Teach both refactoring skills
  in Module 3 without running them.
- Combine the existing skills in Module 5's dev-workflow agent, with human
  approval before refactoring and again before test generation.
- Keep refactoring independent. Its skills select completed reports from
  `reports`, not output from a known agent, and never invoke another agent
  to supply input.
- Define the expected API behavior instead of leaving search/removal semantics
  for the implementing agent to invent.
- Use an explicit CLI agent switch rather than assuming automatic handoff
  buttons or orchestration.
- Adapt the reference's MCP lab as Module 6 without selecting a repository.
  Keep repository-dependent issue/PR steps optional and preserve the existing
  agents' boundaries by using the default agent for that exercise.

## Configuration references

The agent files use `.agent.md` profiles and documented tool aliases. Skills use
named folders with `SKILL.md` frontmatter. Skills are selected based on task
relevance; merely being available does not guarantee invocation. Named skill
requests in the exercises make the intended use explicit.

- [Custom agent configuration](https://docs.github.com/en/copilot/reference/custom-agents-configuration)
- [CLI skill creation and usage](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills)
- [CLI quickstart](https://docs.github.com/en/copilot/get-started/cli-quickstart)

The reviewer can save reports because it has the `edit` tool. Its report-only
restriction is an instruction, not a path-level permission enforcement.
Participants must still inspect tool requests and the source diff.
