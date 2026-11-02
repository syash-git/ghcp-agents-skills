---
name: safe-refactoring
description: Plan and implement small, approved source refactors from validated report findings, preserve public contracts, and report an ID-by-ID change ledger without testing agents, testing skills, or test generation.
---

# Safe Refactoring

Use alongside `review-handoff`; never bypass its intake and approval checks.

## Plan

1. Read the approved plan and the relevant source/callers. If the plan, source,
   or approval disagrees, stop and clarify before implementation.
2. Separate structural refactors from defect corrections. Structural changes
   preserve behavior; corrections may change it and must be approved against
   the behavior contract.
3. Prefer existing helpers. Extract a small helper only for genuinely repeated
   logic, not to introduce a framework for this sample.

## Implement

- Make the smallest coherent edits that fully satisfy each approved finding.
- Preserve public classes, method signatures, return shapes, and JSON record
  format required by the sample contract.
- Validate before mutation. Do not partially add or delete data before rejecting
  an invalid input.
- Handle only exceptions with a real recovery path. Propagate unexpected errors
  instead of returning empty results or success.
- Keep caller changes tied to the relevant finding and disclose them.
- Do not modify unrelated source, dependencies, templates, or customization files.
- Do not create tests, invoke testing skills/agents, run test frameworks, or
  delegate any work to another agent.
- If an issue cannot be resolved within approved scope, leave it blocked and
  explain why. Do not silently expand the plan.

## Inspect and report

1. Re-read changed functions and their callers against each approved acceptance
   condition. Inspect the diff when Git is available; otherwise compare with the
   report excerpts and inspected original source.
2. Select syntax and read-only CLI checks for the approved source scope and
   record their working directory in the plan. For `samples/book-app-project`,
   use `python -m py_compile books.py book_app.py utils.py` and
   `python -B book_app.py help`. For `samples/book-app-buggy`, use
   `python -m py_compile books_buggy.py book_app_buggy.py` and
   `python -B book_app_buggy.py help`. Run only the selected sample's commands
   if execution is available; record actual observations and failures.
   Do not run add/remove commands against sample data. These are syntax and
   CLI smoke checks, not a regression suite or proof of complete correctness.
3. Check that the implementation does not add a catch-all handler, false success
   result, dependency, or unrelated API change.
4. Use [the completion template](templates/refactor-results.md). Include every
   original finding ID with **Addressed**, **Deferred**, **Blocked**, or
   **Stale**, the evidence, and any remaining work.
5. "Addressed" means code was changed and the stated inspection/demonstration
   supports the correction. Never claim independent acceptance or
   complete behavioral verification. Explicitly list acceptance conditions not
   exercised by the demonstration.
6. Preserve the input report and record its path. Finish with the results ledger
   for the user; do not assume a separate workflow or invoke another agent.
