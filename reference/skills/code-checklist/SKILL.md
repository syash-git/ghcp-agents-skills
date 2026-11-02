---
name: code-checklist
description: Team code quality checklist. Use for a code review, quality check, pre-merge review, or follow-up review of source code; produce structured findings, not implementation.
---

# Code Quality Checklist

Inspect the requested source and callers before making claims. Apply all five
categories in order. For categories without findings, write "No issues found."
Do not confuse a missing feature with a defect: use the supplied behavior
contract to establish expected behavior.

## 1. Input validation

- Check null, empty, whitespace-only, and incorrectly typed values before use.
- Identify relevant domain limits without inventing unsupported constraints.
- Explain what happens to existing state when validation fails.

## 2. Error handling

- Identify catch-all handlers that suppress unexpected failures.
- Check whether error paths are visible to callers and resources are released.
- Recommend specific exceptions only when there is a documented recovery path.

## 3. Correctness

- Examine loop termination, duplicate results, and mutation during iteration.
- Check consistent case handling and truthful success/failure return values.
- Compare implementation with caller expectations and the behavior contract.

## 4. Readability & maintainability

- Prefer meaningful names, focused functions, and understandable control flow.
- Identify repeated logic only when extraction would make changes safer.
- Avoid style-only findings and speculative large redesigns.

## 5. Testability

- Discuss global state, side effects, and separation of I/O from logic as design
  properties only.
- Do not request tests or coverage, create test artifacts, run a test framework,
  or invoke testing skills or agents. This category preserves the reference
  workshop's checklist, not a testing workstream.

## Report contract

Use [the report template](templates/code-review.md). A template is a schema, not
evidence; replace placeholders and create only findings supported by the code.

- Assign each finding a unique stable ID: `CR-001`, `CR-002`, and so on.
- Each finding needs: category, **Bug / Risk / Improvement**, file and line
  range, exact source excerpt, impact, suggested change, acceptance condition,
  and whether behavior changes. Distinguish verified defects from uncertainty.
- Give each finding one primary category; cross-reference IDs rather than
  double-counting it in other categories.
- Label current behavior, contract-required behavior, and optional design
  improvements distinctly. Do not call an approved bug fix behavior-preserving.
- Do not authorize implementation. Record approval as "Pending user decision."
- End with exactly one overall assessment: `Good`, `Needs work`, or
  `Blocking issues`, with a brief explanation. Do not invent blocking findings
  merely because this is a workshop.
- Save only to the requested report path; otherwise return the report in chat.
- On follow-up, retain original IDs and record **Resolved**, **Still open**, or
  **Needs clarification** with current source evidence. Put genuinely new
  findings under new IDs after the highest existing ID, and use a different
  report path. A completion report alone does not establish resolution.
