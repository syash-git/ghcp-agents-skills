# Module 1: Create a code-review checklist skill (8 minutes)

> **Prerequisite:** Complete [setup](../README.md#setup-5-minutes). You should
> have `samples\book-app-project\books.py` and no workshop agents or skills installed.
> Keep the sample source unchanged.

## 1. What you're building

A reusable quality-review procedure that Copilot can load when a request matches
its description. You will create `code-checklist` and try it with the default
agent. No custom agent is needed yet: the checklist is a reusable procedure
that can later be used by the code-review agent you build in Module 2.

The skill combines two parts:

- **A code-review checklist** that tells Copilot what to inspect across five
  quality categories.
- **A reporting contract backed by a report template** that requires consistent
  sections and finding fields, including IDs, evidence, impact, and acceptance
  conditions.

You will write the skill first, then its supporting report template, and finally
try them together in a code review.

## 2. Create the skill file

Use a directory matching the skill name and a file named `SKILL.md`.
Create the skill directory:

**PowerShell**

```powershell
New-Item -ItemType Directory -Force -Path .\.github\skills\code-checklist
```

**Bash**

```bash
mkdir -p .github/skills/code-checklist
```

Create `.github\skills\code-checklist\SKILL.md` in your editor:

```markdown
---
name: code-checklist
description: Team code quality checklist. Use for a code review, quality check, pre-merge review, or follow-up review of source code; produce structured findings, not implementation.
---

# Code Quality Checklist

Read the requested source, callers, and behavior contract before reporting.
Apply all five categories in order. Write "No issues found" for empty categories.

## 1. Input validation

- Check null, blank, whitespace-only, and incorrectly typed arguments.
- Check relevant domain limits and validation before state mutation.

## 2. Error handling

- Identify catch-all handlers that suppress unexpected failures.
- Check visible error paths, resource cleanup, and genuine recovery behavior.

## 3. Correctness

- Check loop termination, duplicate results, and mutation during iteration.
- Check consistent case comparisons and truthful success/failure return values.
- Compare behavior with the supplied contract and callers.

## 4. Readability & maintainability

- Prefer meaningful names, focused functions, and understandable control flow.
- Flag repeated logic only when a small extraction would make changes safer.
- Avoid style-only findings and speculative redesigns.

## 5. Testability

- Discuss global state, side effects, and I/O separation as design properties only.
- Do not request coverage, create tests, run test frameworks, or use testing
  agents or skills.

## Report contract

Use [the report template](templates/code-review.md). Replace all placeholders.

- Assign unique, stable IDs: CR-001, CR-002, and so on.
- Each finding needs a category, Bug/Risk/Improvement severity, source path
  and line range, exact snippet, impact, suggested change, acceptance condition,
  and behavior-change statement.
- Give each finding one primary category; cross-reference rather than duplicate.
- Separate verified defects, uncertain risks, and optional improvements.
  Do not invent requirements or call a behavior correction a pure refactor.
- Record approval as "Pending user decision"; never authorize implementation.
- Save only to the requested report path; otherwise reply in chat.
- On follow-up, preserve the original report and IDs. Mark each original ID
  Resolved, Still open, or Needs clarification using current source evidence.
  Give new findings IDs after the highest existing ID.
- End with one Summary assessment: Good, Needs work, or Blocking issues.
```

**Why the description matters:** It explains which requests the skill applies
to. The body supplies the procedure, while the supporting template defines
the report. The folder name and the frontmatter `name` must match.

### Supporting report template

Now create the template directory:

**PowerShell**

```powershell
New-Item -ItemType Directory -Force -Path .\.github\skills\code-checklist\templates
```

**Bash**

```bash
mkdir -p .github/skills/code-checklist/templates
```

Create `.github\skills\code-checklist\templates\code-review.md`:

````markdown
# Code Review

Report state: <Completed review, or Draft if evidence is missing>
Reviewed scope: <source paths>
Behavior contract: <path>
Source baseline: <revision if available; otherwise exact excerpts below>
Approval: Pending user decision

## 1. Input validation

<Findings, or No issues found.>

### CR-001: <specific title>

- Severity: <Bug | Risk | Improvement>
- Location: <file and line range>
- Evidence:

```text
<exact current source excerpt>
```

- Impact: <observable failure>
- Suggested change: <bounded recommendation>
- Acceptance condition: <observable expected result>
- Behavior change: <None, or current behavior -> contract-required target>

## 2. Error handling

<Same finding fields with unique IDs, or No issues found.>

## 3. Correctness

<Same finding fields with unique IDs, or No issues found.>

## 4. Readability & maintainability

<Same finding fields with unique IDs, or No issues found.>

## 5. Testability

<Design-only findings, or No issues found. No testing work.>

## Findings index

| ID | Severity | Source path | Suggested scope |
|---|---|---|---|
| <ID> | <severity> | <path> | <bounded change> |

Summary: <Good | Needs work | Blocking issues> - <brief reason>
````

The outer four-backtick fence lets this template include a three-backtick source
excerpt. Save only the content inside the outer fence. A template is not a
completed review and must not be presented as actual findings.

## 3. Try it out

From a terminal at the workshop root, start Copilot CLI if it is not already running:

**PowerShell**

```powershell
copilot
```

**Bash**

```bash
copilot
```

Start a fresh conversation with `/new`, then use `/agent` to choose the default
agent. Reload the new skill:

```text
/skills reload
```

Ask for a task matching the skill's description:

```text
Perform a code quality check of samples/book-app-project/books.py against docs/behavior-contract.md. Reply in chat only; do not change files or create tests.
```

## 4. What to look for

- The default agent uses `code-checklist` without needing a custom agent.
- Five numbered checklist sections appear in order, with a final **Summary**.
- Categories without findings explicitly state **No issues found**.
- Findings use the report fields, including stable IDs, evidence,
  and acceptance conditions.
- Source files remain unchanged; Testability stays a design discussion, not
  a test-generation task.

Use `/skills` to confirm discovery, and inspect the conversation for actual
invocation. Being listed as available does not establish that the skill ran.
If the checklist is ignored, verify its file location, description, and enabled
state, then reload and repeat the request. You can explicitly name
`code-checklist` in the prompt to request it directly.

You have created and used the checklist skill. Next, create a reviewer whose
instructions explicitly require this existing skill.

---

**Next module:** [02 - Create a code-review agent](02-create-code-review-agent.md).
