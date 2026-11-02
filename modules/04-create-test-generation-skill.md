# Module 4: Create a test-generation skill (12 minutes)

> **Prerequisite:** Complete setup and read
> [the behavior contract](../docs/behavior-contract.md). Modules 1-3 are not
> required. Use current source; do not reset learner edits.

## 1. What you're building

In [Module 3](03-create-refactoring-skills.md), you created skills for approved
code changes. Now let's create a test-generation skill to check expected
behavior. Create it here; run it through the dev-workflow agent in Module 5.

Use the pytest framework and fixtures already present in
`samples\book-app-project\tests\test_books.py`. Preserve those tests and extend
them only in Module 5. Test failures do not authorize production fixes.

## 2. Create the skill

Create the project-local skill directory:

```powershell
New-Item -ItemType Directory -Force -Path .\.github\skills\test-generation
```

Create `.github\skills\test-generation\SKILL.md` with the following complete content:

```markdown
---
name: test-generation
description: "Use when generating test cases, writing unit tests, or adding regression coverage for samples/book-app-project."
---

# Test Generation

## Procedure

1. Read `docs/behavior-contract.md`, the requested source, and existing tests.
   Derive expected behavior from the contract and explicitly approved changes,
   not from the implementation. Flag unclear requirements rather than inventing them.
2. Extend `samples/book-app-project/tests/test_books.py` using existing pytest
   conventions. Preserve existing tests and learner changes.
3. Map each contract requirement in the requested scope to a named test or
   parameterized case, covering normal, edge, and failure cases as applicable.
   Use precise assertions for returned values, state changes, and exceptions.
   Keep tests independent so one broken operation does not mask another.
4. Reuse `tmp_path` and `monkeypatch` to redirect `books.DATA_FILE` before
   constructing collections or importing the CLI. Patch the CLI collection
   and input/output when needed. Never modify the sample's `data.json`.
5. Change tests only. Do not install packages or fix production code.
   Distinguish test/setup errors from production mismatches; do not weaken
   assertions or add skips/expected failures to hide contract violations.
6. Run tests only when explicitly requested. From `samples/book-app-project`,
   use `python -m pytest tests/test_books.py -v`.
   Otherwise provide the command and state that tests were not run.

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

## 3. Check discovery

Reload skills:

```text
/skills reload
```

Use `/skills` to confirm `test-generation` is available.
Do not invoke it or generate tests yet.

## 4. What to look for

- The skill exists at the specified path and is discoverable.
- Its instructions derive expected values from the behavior contract.
- Its procedure covers temporary-file isolation, precise assertions, and honest reporting.
- No tests have been generated, and source remains unchanged.

If discovery fails, verify file locations, frontmatter, skill name/folder
agreement, and skill reload. Do not bypass an unavailable skill.

## Completion checkpoint

The skill is ready. In Module 5, the dev-workflow agent will invoke it only
after the human approves the refactored changes.

---

**Next module:** [05 - Create a dev-workflow agent](05-create-dev-workflow-agent.md).
