# Workshop: Code Review, Refactoring, and Test-Generation Skills

**Duration:** 60 minutes for Modules 1-6, plus 5 minutes for setup; Module 7 is an additional exercise | **Format:** build-it-yourself labs | **Runtime:** Python 3.10+

Create three custom agents and four reusable skills from scratch. First create a
checklist skill, then a reviewer that explicitly uses it. Create dedicated
skills for report-based refactoring and contract-based test generation without
running them yet. Refactoring validates completed reports against
[the review template](reference/skills/code-checklist/templates/code-review.md)
and current source evidence.
Finally, combine the existing skills in a dev-workflow agent with human approval
before refactor planning, before implementation, and before test generation.
Module 7 adds an issue-resolver agent that uses GitHub MCP, diagnoses the root
cause, and makes a human-approved minimal local fix in `book-app-buggy` without
the review/refactoring skills.

**Nothing is pre-installed in `.github`.** You create every agent, skill, and
supporting template during the labs. Completed examples live outside the active
configuration in [reference](reference/README.md); use them as an answer key
after attempting each lab, not as a setup step.

The review exercises follow the main agent-plus-checklist approach in
[syash-git/agents-and-skills-workshop](https://github.com/syash-git/agents-and-skills-workshop).

## Learning outcomes

By the end, you will have created:

| You build | Role in the workflow |
|---|---|
| `code-checklist` skill + report template | Apply five review categories and record stable finding IDs |
| `code-reviewer` agent | Explicitly use the checklist to review source without implementing fixes |
| `review-handoff` skill + plan template | Validate findings and separate planning from approval |
| `safe-refactoring` skill + results template | Make bounded edits and account for each finding |
| `test-generation` skill | Extend the sample's pytest cases in the dev workflow without modifying production code |
| `dev-workflow` agent | Review, approve planning, approve the refactor plan, refactor, approve test generation, then generate tests |
| `issue-resolver` agent | Read related GitHub issues, diagnose one selected issue's root cause, and apply an approved minimal local fix |

An **agent** defines a role and its boundaries. A **skill** defines a reusable
procedure. You will create each separately, then connect them and observe how
they compose.

**Out of scope:** additional test frameworks and delegation between agents.
Module 6 introduces GitHub MCP, with optional issue/PR steps once you choose
a repository. The review checklist retains
Testability as a design-only discussion; test generation is a separate track
using the sample's existing pytest dependency.

## Setup (5 minutes)

Use an editor, PowerShell, an authenticated GitHub Copilot CLI installation,
and Python 3.10+. Clone the repository and enter its directory before running
the workshop commands:

```powershell
git clone https://github.com/syash-git/ghcp-agents-skills.git
Set-Location .\ghcp-agents-skills
```

```powershell
copilot --version
python --version
Push-Location .\samples\book-app-project
python -B .\book_app.py help
Pop-Location
copilot
```

Use [the book-app-project sample](samples/book-app-project/README.md) for
Modules 1-5. Module 7 uses
[book-app-buggy](samples/book-app-buggy/README.md).
The project sample has a JSON-backed `BookCollection`, a CLI, and existing pytest
tests. Run app commands from its directory because `DATA_FILE` is relative to
the working directory. Review the code without changing it yet.
Pytest is declared in the sample's project manifest and is needed only if you
choose to run tests.
Read [the behavior contract](docs/behavior-contract.md) to understand the target.

In Copilot, inspect `/agent` and `/skills`. The workshop's three agents and four
skills should **not** be present before you create them. Personal or organization
configuration may supply similarly named definitions; identify or temporarily
disable those through the menus, if permitted, so your baseline is meaningful.
Do not remove another configuration or grant unrestricted permissions.

Use the default agent for initial comparisons. When a lab asks you to author a
definition, create it in your editor yourself rather than asking an existing
agent to install all of the finished examples.

## Workshop route

| Module | Time | What you create |
|---|---|---|
| [1. Create a code-review checklist skill](modules/01-create-code-review-skill.md) | 8 min | A quality checklist and report template, used with the default agent |
| [2. Create a code-review agent](modules/02-create-code-review-agent.md) | 8 min | A reviewer that explicitly uses the existing checklist skill |
| [3. Create refactoring skills](modules/03-create-refactoring-skills.md) | 12 min | Refactoring skills and templates, created but not run |
| [4. Create a test-generation skill](modules/04-create-test-generation-skill.md) | 12 min | A test-generation skill, created but not run |
| [5. Create a dev-workflow agent](modules/05-create-dev-workflow-agent.md) | 10 min | A single agent combining the skills with three human approval gates |
| [6. Use the GitHub MCP server](modules/06-mcp-server.md) | 10 min | Built-in MCP tools, with optional repository-dependent issue and PR exercises |
| [7. Create an issue-resolver agent](modules/07-create-issue-resolver-agent.md) | Additional exercise | GitHub issue reads, root-cause analysis, and an approved minimal local bug fix without refactoring |

**Modules 1-2** demonstrate code review. **Modules 3-4** create the remaining
skills and check discovery only. **Module 5** runs review, approved planning,
approved refactoring, and approved test generation through the dev-workflow
agent. A review with no findings ends after the report.
There is no pre-created-agent fast path: authoring the definitions is the goal,
not just running them. Modules 2, 5, and 7 create custom agents.
Module 6 uses the default agent separately; it does not change their boundaries
or select a repository for you.
Module 7 asks for the repository at runtime, diagnoses one selected issue, and
fixes its root cause after approval. It requires Module 6, not the earlier
skills. It does not refactor unrelated code, generate or run tests, or publish changes.

## Starting layout

```text
samples\
  book-app-project\
    books.py
    book_app.py
    utils.py
    data.json
    pyproject.toml
    tests\test_books.py
  book-app-buggy\   # Module 7 issue-resolution sample
docs\
modules\
reference\          # Inactive completed examples; not an installation folder
reports\README.md   # Output descriptions, not completed review findings
```

## What you will add during the labs

```text
.github\
  agents\
    code-reviewer.agent.md
    dev-workflow.agent.md
    issue-resolver.agent.md
  skills\
    code-checklist\
      SKILL.md
      templates\code-review.md
    review-handoff\
      SKILL.md
      templates\refactor-plan.md
    safe-refactoring\
      SKILL.md
      templates\refactor-results.md
    test-generation\
      SKILL.md
samples\book-app-project\tests\test_books.py  # Extended during Module 5
```

Create only the files requested by the current module. Restart Copilot after
creating/changing an agent; use `/skills reload` after creating/changing skills.
Discovery in a menu is not evidence of invocation: inspect the conversation
and output when you use a skill.

Refactoring selects a completed findings report under `reports`, records its
path, validates it against current source, and waits for your approval. With no
eligible report it asks for one; with several it asks you to choose. It does not
invoke another agent to create missing input. Preview plans and result ledgers
are not input findings reports.

Use the reviewer for Module 2. In Modules 3-4, author skills without changing
source or generating tests. Module 5 uses the dev-workflow agent and preserves
all three human approval gates.

## Resources

- [Copilot CLI setup](https://docs.github.com/en/copilot/get-started/cli-quickstart)
- [Custom agent configuration](https://docs.github.com/en/copilot/reference/custom-agents-configuration)
- [CLI skills](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills)
- [Facilitator guide](docs/facilitator-guide.md)
