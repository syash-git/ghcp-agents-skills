# Facilitator guide

## Before delivery

Allow 65 minutes including setup (60 minutes for Modules 1-6). Use Python 3.10+ and a functioning Copilot CLI
installation. The selected `samples/book-app-project` sample declares pytest.
Do not require additional packages, a database server, or an MCP server.
This workspace is the workshop deliverable; publishing it to GitHub is a separate
action and is not needed to run it.

Modules 1-2 build and demonstrate the review skill and agent;
Module 3 builds refactoring skills; Module 4 builds the test-generation skill.
Modules 3-4 create skills without running them. Module 5 runs the combined
workflow. Keep the sample source, JSON data, and existing tests unchanged before
it; do not generate additional tests yet.

Keep a separate pristine copy before learner refactoring if you need another
session. Do not use destructive Git resets or overwrite learner edits to restore
the exercise.

The starting workshop has no active definitions in `.github`. Participants
create three agents, four skills, and their supporting templates in the
labs. Keep [completed examples](../reference/README.md) outside active
configuration; do not bulk-copy them before a session.

Keep completed examples as an answer key rather than an installation step.
In Modules 3-4, check discovery only; save execution for Module 5.

In Module 1, learners create the checklist skill and try it with the default
agent. In Module 2, they create the reviewer with an explicit instruction to use
that existing skill; no intermediate agent or later rewrite is required.
Module 3 creates both refactoring skills and their templates.
Module 4 creates the test-generation skill using the sample's existing pytest
framework and temporary-file fixtures.
Reload skills and confirm discovery, but do not generate plans, refactor source,
or create tests in these modules.

Module 5 combines the existing skills in one dev-workflow agent. Require a
human response approving report findings before source changes, then another
approving the changes before test generation. Do not treat the initial workflow
request as either approval. The existing skills are reused without new agents
for refactoring or testing.

Module 6 enables the built-in GitHub MCP server without additional packages.
Do not assume a repository or matching issues exist. Issue browsing and PR
publishing are optional and require the learner's chosen repository and access;
publishing also needs a matching Git checkout and explicit approval. Use the
default agent, without changing the existing custom agents' restrictions.

Module 7 is an additional issue-resolver exercise using `book-app-buggy`.
Learners provide a repository at runtime and select an applicable issue.
The agent directly traces the symptom to its root cause, proposes a minimal fix,
waits for explicit approval, then corrects the faulty code without unrelated
refactoring. It does not require Modules 1-5 or invoke their skills.
Require issue-specific acceptance conditions
instead of assuming the project sample's behavior contract applies. Ask about
ambiguous year ranges or author matching. No tests, publishing, or issue writes
are part of this exercise; no additional dependencies are needed.
The diagnosis and proposed fix share one report, followed by a results report.
Source inspection, syntax checks, and CLI help do not establish behavioral
correctness; require disclosure of unverified acceptance criteria.

If agents are not discovered, restart Copilot in the workshop root. For skills,
use `/skills reload` and check the file and folder names. Personal and
organization configuration may affect comparisons; do not delete it to prepare
the workshop. If this folder was previously used with active definitions,
restart Copilot after moving them out so cached agents do not mask the exercise.

## Suggested timing

| Segment | Minutes |
|---|---|
| Setup and concepts | 5 |
| Create the review skill and template | 8 |
| Create the code-review agent using the skill | 8 |
| Create refactoring skills and templates; check discovery | 12 |
| Create the test-generation skill; check discovery | 12 |
| Create the dev-workflow agent; practice both approval gates | 10 |
| Enable GitHub MCP; inspect tools and optional repository exercises | 10 |

## Intentional review targets

In Modules 1-5, review `samples/book-app-project`, not the buggy sample. Ground
findings in current source and [the behavior contract](behavior-contract.md).
Do not assume defects from the removed in-memory starter still exist.
Module 7 instead diagnoses and fixes only the selected issue in `samples/book-app-buggy`.

| Area | Review target | Expected direction after approval |
|---|---|---|
| Validation | Model and CLI permit blank values and unvalidated years | Agree exact requirements before changing validation |
| Persistence | `DATA_FILE` depends on the working directory | Preserve current behavior unless a path change is approved |
| Error handling | Missing/corrupt files recover; other I/O errors propagate | Keep warnings visible and avoid false success |
| CLI feedback | Removal message does not distinguish missing books | Change messages only within approved scope |
| Maintainability | UI helpers in `utils.py` are not used by the CLI | Consider bounded reuse, not a new architecture |
| Compatibility | Title/author lookup is already exact and case-insensitive | Do not invent substring matching or all-duplicate removal |

Do not prescribe a fixed number of findings or universal ID mapping.
A reviewer may group closely related defects. Require unique IDs and actionable
acceptance conditions rather than a particular answer key.

## Demonstration observations

From `samples/book-app-project`, run `python -B book_app.py help` or
`python -B book_app.py list`. Both read the sample without modifying it.
Do not run interactive add/remove commands against the copied `data.json`
during setup or verification.

The syntax command and demonstration do not verify the full contract.
Module 5 extends existing pytest cases after change approval. Tests must use
temporary JSON files and cover only the contract and explicitly approved changes.

## Common interventions

| Problem | Response |
|---|---|
| Workshop definitions appear before learners create them | Identify cached/personal definitions and restart; do not pre-install answer keys |
| Refactoring skills are missing | Finish Module 3 and reload skills |
| Review tries to fix source | Stop the edit; reinforce report-only review boundaries |
| Checklist never loads | Inspect invocation, description, enabled state, and skill reload |
| No eligible input report | The handoff skill asks the user to supply one; it does not generate findings |
| Several input reports qualify | Ask the user to select one; do not choose the newest or merge silently |
| Evidence changed after review | Refresh stale findings before implementation |
| Refactorer starts after plan-only request | Stop; require explicit ID/scope and behavior approval |
| Agent invents architecture | Point to contract invariants and defer Improvements |
| Refactorer changes the API or JSON schema | Preserve `BookCollection` signatures and stored fields unless explicitly approved |
| Catch-all remains | Ask which specific recovery path justifies it |
| "Everything passed" without evidence | Require actual observations and unverified conditions |

The reviewer has no shell execution or agent delegation. Refactoring and test
generation run through the dev-workflow agent in Module 5. Report-only and
source-scope limits are instructions, not security sandboxes.

## Test-generation interventions

| Problem | Response |
|---|---|
| Generated tests encode starter defects as expected behavior | Re-read the behavior contract; keep failing contract assertions |
| Tests touch sample data | Patch `books.DATA_FILE` to a `tmp_path` before constructing collections or importing the CLI |
| Search tests depend on add logic | Seed independent `Book` fixtures |
| Zero tests discovered | Check the output path and discovery command; do not call the run a pass |
| Test generator starts fixing production code | Stop the edit; require a separate approved correction task |
| Failing suite is hidden by skips or expected failures | Keep defects visible and distinguish test mistakes from source mismatches |

Discuss what generated coverage does and does not establish. A passing run
does not prove completeness; require mapping back to every contract requirement.
