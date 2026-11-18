# Facilitator guide

## Before delivery

Use Python 3.10+ and a functioning Copilot CLI installation. The
`samples/book-app-project` sample has no bundled tests or
third-party runtime dependencies. No testing framework or test-generation
skill is required for the current modules.
Do not require other packages, a database server, or a separately hosted MCP server.
This workspace is the workshop deliverable; publishing it to GitHub is a separate
action and is not needed to run it.

Part 1 builds and demonstrates the review skill and review-refactor agent.
Part 2 uses GitHub MCP to debug issues, first with the default agent and then
with the issue-resolver agent. Keep sample source unchanged until an exercise
authorizes edits, and preserve JSON data and any learner-created tests.
No starter tests are supplied.

Keep a separate pristine copy before learner refactoring if you need another
session. Do not use destructive Git resets or overwrite learner edits to restore
the exercise.

The starting workshop has no active definitions in `.github`. Participants
create one skill, its report template, and two agents in the core modules.
Keep [completed examples](../reference/README.md) outside active
configuration; do not bulk-copy them before a session.

Keep completed examples as an answer key rather than an installation step.

## Part 1: Review and refactor code

In [Module 1.1](<../modules/1.1 Create a Code Review Skill.md>), learners create the
checklist skill and try it with the default agent.
[Module 1.2](<../modules/1.2 Create a Review Refactor Agent.md>) creates the
review-refactor agent, which explicitly uses that skill rather than duplicating
its procedure.

Review and Refactor are capabilities, not a fixed sequence. Let learners discuss
findings and alternatives without rerunning reviews or treating questions as
approval. Reviews produce a report; requested refactoring produces a saved plan.
Source changes require explicit plan approval, and changed scope needs renewed
approval. The agent inspects edits statically and does not execute code or tests.
No actionable findings means no forced edits.

## Part 2: Debug issues using an MCP server

[Module 2.1](<../modules/2.1 Use the GitHub MCP Server.md>) enables the built-in GitHub MCP server.
Use the default agent to read issues and make a local fix. Do not assume a
repository or matching issues exist. Keep the exercise local: no new branches,
commits, pushes, PRs, or issue closure.

[Module 2.2](<../modules/2.2 Create an Issue Resolver Agent.md>) creates the
issue-resolver agent using `book-app-buggy`.
Learners provide a repository at runtime and select an applicable issue.
The agent directly traces the symptom to its root cause, proposes a minimal fix,
waits for explicit approval, then corrects the faulty code without unrelated
refactoring. It does not require Part 1 or invoke its skill.
Require issue-specific acceptance conditions
instead of assuming the project sample's behavior contract applies. Ask about
ambiguous year ranges or author matching. No tests, publishing, or issue writes
are part of this exercise; no additional dependencies are needed.
The diagnosis and proposed fix share one report, followed by a results report.
Source inspection, syntax checks, and CLI help do not establish behavioral
correctness; require disclosure of unverified acceptance criteria.

## Discovery

If agents are not discovered, restart Copilot in the workshop root. For skills,
use `/skills reload` and check the file and folder names. Personal and
organization configuration may affect comparisons; do not delete it to prepare
the workshop. If this folder was previously used with active definitions,
restart Copilot after moving them out so cached agents do not mask the exercise.

## Workshop route

| Part | Modules | Sample |
|---|---|---|
| 1: Review and refactor code | 1.1 Review skill; 1.2 Review-refactor agent | `book-app-project` |
| 2: Debug issues using an MCP server | 2.1 GitHub MCP; 2.2 Issue-resolver agent | `book-app-buggy` |

## Intentional review targets

In Part 1, review `samples/book-app-project`, not the buggy sample. Ground
findings in current source and the
[behavior contract](../samples/book-app-project/behavior-contract.md).
Do not assume defects from the removed in-memory starter still exist.
Module 2.2 instead diagnoses and fixes only the selected issue in `samples/book-app-buggy`.

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

These are facilitator demonstrations, not commands for the review-refactor agent.
They do not verify the full contract. Test generation and execution are outside
the current workshop route.

## Common interventions

| Problem | Response |
|---|---|
| Workshop definitions appear before learners create them | Identify cached/personal definitions and restart; do not pre-install answer keys |
| Review skill is missing | Finish Module 1.1 and reload skills |
| Review tries to fix source | Stop the edit; reinforce report-only review boundaries |
| Checklist never loads | Inspect invocation, description, enabled state, and skill reload |
| No current review report | Ask the user to provide one or request a review before planning |
| Several input reports qualify | Ask the user to select one; do not choose the newest or merge silently |
| Evidence changed after review | Refresh stale findings before implementation |
| Refactorer starts after plan-only request | Stop; require explicit ID/scope and behavior approval |
| Agent invents architecture | Point to contract invariants and defer Improvements |
| Refactorer changes the API or JSON schema | Preserve `BookCollection` signatures and stored fields unless explicitly approved |
| Catch-all remains | Ask which specific recovery path justifies it |
| "Everything passed" without evidence | Require actual observations and unverified conditions |

The review-refactor agent has no shell execution or agent delegation and does
not generate tests. Report-only and source-scope limits are instructions, not
security sandboxes.
