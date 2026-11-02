# Refactoring Plan

Input report: <selected path under reports>
Behavior contract: <contract path>
Source scope: <paths>
Mode: <Plan only | Approved implementation>
Approval evidence: <exact user instruction, or Pending>
Approved finding IDs: <explicit IDs, or None>

## Invariants

<Public names, signatures, state identity, valid-input results, and other
contract requirements that must remain unchanged.>

## Finding disposition

| ID | Severity | Current evidence | Disposition | Reason |
|---|---|---|---|---|
| <original ID> | <severity> | <current path and excerpt match> | <Selected / Deferred / Stale / Needs clarification / Out of scope> | <reason> |

## Proposed changes

| ID | Files | Change | Observable behavior change | Acceptance condition |
|---|---|---|---|---|
| <selected ID> | <source paths> | <bounded edit> | <None, or old -> new> | <observable outcome> |

## Verification approach

<Source/caller inspection, syntax check, and direct demonstration only.
No testing skills, agents, generated tests, or test runners.>

## Stop conditions

<Missing approval, stale evidence, conflicting contracts, unrelated dirty
changes, unavailable required skills, or scope expansion.>
