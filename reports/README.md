# Workshop outputs

The review and refactoring exercises use this folder. Refactoring accepts completed
findings reports from any producer; it does not require a review agent.

| File | Producer | Consumer |
|---|---|---|
| `code-review.md` | Review exercise | Learner inspecting source findings |
| `refactor-input.md` (or another selected report) | User-supplied report or explicit preparation step | Refactoring input |
| `follow-up-review.md` | `code-reviewer` + `code-checklist` | Learner closing open IDs |
| `dev-review.md` | Dev-workflow agent + `code-checklist` (Module 5) | Human reviewing findings |
| `dev-plan.md` | Dev-workflow agent + `review-handoff` | Human approving implementation scope |
| `dev-results.md` | Dev-workflow agent + `safe-refactoring` | Human reviewing changes before test generation |
| `issue-review.md` | Issue-resolver + `code-checklist` (Module 7) | Human reviewing issue evidence |
| `issue-plan.md` | Issue-resolver + `review-handoff` | Human approving finding IDs and behavior changes |
| `issue-results.md` | Issue-resolver + `safe-refactoring` | Human inspecting the local fix and verification limits |

There are deliberately no completed reports here yet. Supply findings grounded
in current source and matching [the input contract](../docs/report-contract.md).
An agent or workflow's identity is not a required report field.

Modules 3-4 create definitions only. The dev-workflow agent generates the
review, plan, and results in Module 5. A plan is not implementation approval.
Module 7 saves separate issue-specific reports, including the GitHub issue URL.
It does not post reports to GitHub or close the issue.

When no input path is supplied, the handoff skill selects the sole eligible
completed findings report or asks the user if none or several qualify. README
files, templates, drafts, plans, previews, and results are not eligible input.

Preserve selected input reports and original reviews. Reports contain
source excerpts, so review them before sharing outside your project.
