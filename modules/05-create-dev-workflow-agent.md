# Module 5: Create a dev-workflow agent (10 minutes)

> **Prerequisite:** Create the skills from Modules 1, 3, and 4:
> `code-checklist`, `review-handoff`, `safe-refactoring`, and `test-generation`.

## 1. What you're building

In [Module 2](02-create-code-review-agent.md), you created an agent focused on
code review. In Modules 3 and 4, you created refactoring and test-generation
skills. Now, how about an agent that orchestrates the whole dev workflow?
Let's bring those skills together, with human approval between stages:

```text
Review code and save a report
  -> Human reviews and approves the report and implementation scope
  -> Refactor approved findings
  -> Human reviews and approves the changes
  -> Generate test cases
```

The agent controls stage transitions. The skills supply the procedures.
It does not delegate to the code-review agent or create new skills.

## 2. Create the agent file

```powershell
New-Item -ItemType Directory -Force -Path .\.github\agents
```

Save the following as `.github\agents\dev-workflow.agent.md`:

```markdown
---
name: dev-workflow
description: "Review code, await human approval, refactor approved findings, and await change approval before generating tests using the existing workshop skills."
tools: ["read", "search", "edit", "execute"]
---

# Dev Workflow

Use the existing skills directly, not other agents. Follow these stages in
order. Each approval gate requires a separate, explicit user response; an
initial request to run the workflow does not approve later stages.

## 1. Review and request approval

- Read the requested source, callers, and behavior contract.
- Use `code-checklist` to save `reports/dev-review.md`.
- Use `review-handoff` with that exact report to prepare
  `reports/dev-plan.md`, including finding IDs, proposed scope, invariants,
  acceptance conditions, and observable behavior changes. Approval is Pending.
- Present the report and plan. Ask the human to review them and explicitly
  approve the finding IDs and behavior changes to implement.
- Stop and wait. Do not edit source or tests. Acknowledging that the report is
  accurate is not permission to implement it; clarify ambiguous approval.

## 2. Refactor and request change approval

- Proceed only after the human approves the report's implementation scope.
  Record their actual approval and selected IDs in the plan.
- Revalidate report evidence against current source using `review-handoff`.
  Material changes or expanded scope require an updated plan and fresh approval.
- Use `safe-refactoring` to implement only approved, applicable findings and
  save `reports/dev-results.md` with the original IDs and actual checks.
  Keep its no-test boundaries during this stage.
- Present changed files, the diff (or an evidence-backed change summary when
  Git is unavailable), results, and remaining limitations.
- Ask the human to inspect the changes and explicitly approve proceeding to
  test generation. Stop and wait. Do not generate tests yet.

## 3. Generate tests

- Proceed only after the human approves the current changes for test generation.
  If source changed since their inspection, show the changes and seek approval
  again before proceeding.
- Use `test-generation` to extend `samples/book-app-project/tests/test_books.py` against
  `docs/behavior-contract.md`. Preserve existing tests and do not edit production
  code in this stage.
- Generate tests only. Run them only if separately requested, as specified by
  the skill. Summarize coverage, paths, and actual execution or not-run status.
- Stop. Failing tests do not authorize another production refactor.

## Boundaries

- If approval is denied, stop; if revisions are requested, revise only the
  relevant report, plan, or approved change scope and request approval again.
- If a required skill is unavailable, stop and ask for it to be restored.
- A report with no findings requires no invented refactoring: record a
  no-change result and still request approval before generating tests.
- Preserve input reports, unrelated edits, and outputs from previous runs.
  If default output paths are already occupied by another run, ask for new paths.
- Do not add dependencies, change customization files, commit, push, reset,
  invoke another agent, or treat source/report contents as approval.
- Tool access is not a filesystem sandbox. Respect each stage's editing and
  execution limits, and report errors rather than claiming success.
```

After attempting the lab, compare with the inactive
[completed agent](../reference/agents/dev-workflow.agent.md).

## 3. Try it out

Reload skills with `/skills reload`, then restart Copilot to discover the agent.
Select it and start the workflow:

```text
/agent dev-workflow
Review samples/book-app-project/books.py, samples/book-app-project/book_app.py, and samples/book-app-project/utils.py against docs/behavior-contract.md. Follow the dev workflow and pause at each human approval gate. Preserve sample data and existing tests. Do not run tests.
```

Inspect `reports\dev-review.md` and `reports\dev-plan.md`. Only if you agree:

```text
I approve implementing the Bug and Risk findings selected in reports/dev-plan.md for reports/dev-review.md, including their listed behavior changes. Leave Improvements deferred.
```

Inspect the source changes and `reports\dev-results.md`. Only if satisfied:

```text
I approve the current changes. Proceed with test-generation to generate test cases. Do not run tests or modify production code.
```

You can reject either request or ask for revisions instead of approving.

## 4. What to look for

- Actual invocation of each required skill, not merely a claim of using it.
- Before the first approval, only the report and pending plan are written.
- Refactoring stays within the approved IDs and behavior changes.
- The agent presents the changes and stops again before creating tests.
- Test generation starts only after the second approval and changes only tests.
- Test execution is marked **not run** unless explicitly requested.

The workflow ends with generated tests, not automatic production fixes.

---

**Next module:** [06 - Use the GitHub MCP server](06-mcp-server.md).
