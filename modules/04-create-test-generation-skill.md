# Module 4: Create a test-generation skill (25 minutes)

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

Author `.github\skills\test-generation\SKILL.md` with this frontmatter:

```yaml
---
name: test-generation
description: "Use when generating test cases, writing unit tests, or adding regression coverage for samples/book-app-project using its existing pytest tests and the behavior contract."
---
```

Write a procedure below the frontmatter that:

1. Reads the contract, source, callers, and any existing tests.
2. Maps requirements to named cases before extending
   `samples\book-app-project\tests\test_books.py`.
3. Uses pytest, precise assertions, and the existing fixture pattern.
4. Uses `tmp_path` and `monkeypatch` to redirect `books.DATA_FILE` before
   constructing a `BookCollection`. Never write to the sample's `data.json`.
5. Uses fresh collections and independent `Book` fixtures so add failures do
   not mask search/removal behavior.
6. Runs tests only when requested and reports actual counts, failures/errors,
   and exit status. Treat zero discovered tests as a validation problem.
7. Leaves contract-revealing failures visible and production code untouched.

Include a coverage checklist for:

- Add: returned `Book`, title/author/year fields, unread default, duplicate
  titles, and persistence.
- Lookup: case-insensitive exact title/author matching, no matches, and order.
- Mark as read: only the first matching book changes; missing titles return
  `False`, and changes persist.
- Removal: remove the first exact case-insensitive title match, preserve
  survivors, and report missing titles accurately.
- Persistence: save/reload round trip, missing files, malformed JSON, and
  visible unexpected I/O errors using temporary files.
- CLI: numbering, input handling, and user messages with mocked input/output.
- Validation or search changes: test only explicitly approved requirements;
  do not impose new year limits, trimming, or substring matching.

Add a completion format: test paths, coverage, actual execution or **not run**,
remaining gaps, and production mismatches. Do not treat generated tests as a
correctness claim.

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
