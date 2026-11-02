# Workshop outputs

The review, refactoring, and issue-resolution exercises use this folder.
Refactoring accepts completed
findings reports from any producer; it does not require a review agent.

| File | Producer | Consumer |
|---|---|---|
| `code-review.md` | Review exercise | Learner inspecting source findings |
| `refactor-input.md` (or another selected report) | User-supplied report or explicit preparation step | Refactoring input |
| `follow-up-review.md` | `code-reviewer` + `code-checklist` | Learner closing open IDs |
| `dev-review.md` | Dev-workflow agent + `code-checklist` (Module 5) | Human reviewing findings |
| `dev-plan.md` | Dev-workflow agent + `review-handoff` | Human approving implementation scope |
| `dev-results.md` | Dev-workflow agent + `safe-refactoring` | Human reviewing changes before test generation |
| `issue-diagnosis.md` | Issue-resolver (Module 7) | Human reviewing the root cause and approving the proposed fix and behavior changes |
| `issue-results.md` | Issue-resolver | Human inspecting the minimal local fix and verification limits |

There are deliberately no completed reports here yet. Supply refactoring input
findings grounded in current source and matching
[the input contract](../docs/report-contract.md).
An agent or workflow's identity is not a required report field.

Modules 3-4 create definitions only. The dev-workflow agent generates the
review, plan, and results in Module 5. A plan is not implementation approval.
Module 7 saves an issue diagnosis/proposed fix and a results report, both
including the GitHub issue URL. These are not refactoring input reports and do
not use the findings contract, finding IDs, or review/refactoring templates.
It does not post reports to GitHub or close the issue.

When no input path is supplied, the handoff skill selects the sole eligible
completed findings report or asks the user if none or several qualify. README
files, templates, drafts, plans, previews, and results are not eligible input.

Preserve selected input reports and original reviews. Reports contain
source excerpts, so review them before sharing outside your project.
