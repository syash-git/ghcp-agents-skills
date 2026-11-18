# Module 4: Create a test-generation skill

> **Prerequisite:** Complete setup and read
> [the behavior contract](../samples/book-app-project/behavior-contract.md). Modules 1-3 are not
> required. Use current source; do not reset learner edits.

## 1. What you're building

This optional exercise creates a skill that writes pytest tests from the
behavior contract. The sample has no bundled tests or pytest dependency;
the skill creates the test file and isolation fixtures from scratch.
Preserve any learner-created tests. Test failures do not authorize production fixes.

Generating tests does not require pytest to be installed. To run them later,
install it yourself with `python -m pip install pytest`. The skill does not
install packages.

## 2. Create the skill

Create the `test-generation` skill folder using either shell:

**PowerShell**

```powershell
New-Item -ItemType Directory -Force -Path .\.github\skills\test-generation
```

**Bash**

```bash
mkdir -p .github/skills/test-generation
```

In the `test-generation` folder, save the following as `SKILL.md`:

```markdown
---
name: test-generation
description: "Use when generating test cases, writing unit tests, or adding regression coverage for samples/book-app-project."
---

# Test Generation

## Procedure

1. Read `samples/book-app-project/behavior-contract.md`, the requested source, and any existing tests.
   Derive expected behavior from the contract and explicitly approved changes,
   not from the implementation. Flag unclear requirements rather than inventing them.
2. Create the `tests` folder and `samples/book-app-project/tests/test_books.py`
   using pytest. If tests already exist, extend them without overwriting learner changes.
3. Map each contract requirement in the requested scope to a named test or
   parameterized case, covering normal, edge, and failure cases as applicable.
   Use precise assertions for returned values, state changes, and exceptions.
   Keep tests independent so one broken operation does not mask another.
4. Create or reuse an autouse fixture with `tmp_path` and `monkeypatch` to
   redirect `books.DATA_FILE` before constructing collections or importing the
   CLI. Seed temporary data per test. Patch the CLI collection and input/output
   when needed. Never modify the sample's `data.json`.
5. Change tests only. Do not install packages or fix production code.
   Distinguish test/setup errors from production mismatches; do not weaken
   assertions or add skips/expected failures to hide contract violations.
6. Run tests only when explicitly requested. From `samples/book-app-project`,
   use `python -m pytest tests/test_books.py -v`.
   Otherwise provide the command and state that tests were not run.
   If pytest is unavailable, report the missing prerequisite; do not install it.

## Completion

Report:
- Test files changed and behaviors covered.
- Actual execution command and results, including test count, failures/errors,
  and exit status when available; or explicitly "Not run". Surface execution
  errors; zero collected tests is not a pass.
- Remaining coverage gaps, unclear requirements, and production mismatches.

Stop after generation and any requested execution. Production fixes require
separate approval.
```

After your attempt, compare with the inactive
[completed skill](../reference/skills/test-generation/SKILL.md).

## 3. Try it out

In Copilot CLI, run `/skills reload` to reload the newly created skill:

```text
/skills reload
```

Use `/skills` to confirm `test-generation` is available. Use `/agent` to select
the default agent, not `review-refactor`, which does not generate tests.

```text
Generate tests for samples/book-app-project.
```

Inspect the generated tests and temporary-file fixtures. Tests are not run
unless you request execution separately:

```text
Run the generated tests.
```

## 4. What to look for

- The skill exists at the specified path and is discoverable.
- Its instructions derive expected values from the behavior contract.
- Its procedure covers temporary-file isolation, precise assertions, and honest reporting.
- Tests and isolation fixtures are created from scratch; production source and
  sample data remain unchanged.
- Execution is reported as Not run unless requested. Missing pytest is surfaced
  rather than installed automatically.

If discovery fails, verify file locations, frontmatter, skill name/folder
agreement, and skill reload. Do not bypass an unavailable skill.

## Completion checkpoint

The skill can generate tests with the default agent or through the archived
dev-workflow exercise. Neither generation nor failing tests authorize production fixes.

---

**Optional continuation:** [Archived dev-workflow exercise](../.archive/05-create-dev-workflow-agent.md).
