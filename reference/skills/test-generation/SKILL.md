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
