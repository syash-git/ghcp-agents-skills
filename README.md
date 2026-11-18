# Agents & Skills Workshop

Welcome! In this workshop, you’ll use a small Python book app to
learn how to create reusable Copilot agents and skills.
## The story

It’s your first week on a new team. Your team lead points you to the **book
app**—a Python CLI for managing a collection of books. It works, but it hasn’t
been reviewed, tested, or hardened before shipping.

Rather than asking Copilot to fix everything in one go, you’ll create reusable
assets: **skills** that capture repeatable procedures and **agents** that give
Copilot a role and clear boundaries.

## Before you begin

- **Python 3.10 or later**
- **Git** and a code editor
- **GitHub Copilot CLI**, installed and signed in with an account that can
  access the repository you’ll use for the GitHub exercises

The sample has no bundled tests or third-party runtime dependencies.
No testing framework is required for the current modules.

## Setup

Clone the workshop and check that Python and Copilot CLI are available:

```sh
git clone https://github.com/syash-git/ghcp-agents-skills.git
cd ghcp-agents-skills
python3 --version
copilot --version
```

## Workshop Guide

Open [book-app-project](samples/book-app-project) and explore the code before starting the modules.

### The book app

The workshop uses a simple Python CLI application for managing a book collection. Both versions
are in `samples/`:

- `book-app-project/` is the main version for the review and refactoring modules.

  You can run this app:

```sh
cd samples/book-app-project
python3 -B book_app.py list
python book_app.py help
```

- `book-app-buggy/` is intentionally broken and used in Part 2's debugging
  exercises.



### Workshop modules

The workshop has two parts: review and refactor local code, then debug issues
using GitHub MCP.

#### Part 1: Review and refactor code

| Module | Description |
|---|---|
| [1.1. Create a code-review checklist skill](<modules/1.1 Create a Code Review Skill.md>) | Create a reusable quality checklist and code review template |
| [1.2. Create a review-refactor agent](<modules/1.2 Create a Review Refactor Agent.md>) | Create an agent that uses the skill and makes approved, statically inspected edits |

#### Part 2: Debug issues using an MCP server

| Module | Description |
|---|---|
| [2.1. Use the GitHub MCP server](<modules/2.1 Use the GitHub MCP Server.md>) | Read GitHub issues and make a local fix using the default agent |
| [2.2. Create an issue-resolver agent](<modules/2.2 Create an Issue Resolver Agent.md>) | Diagnose and fix an approved issue in the buggy sample |

## Helpful links

- [Copilot CLI setup](https://docs.github.com/en/copilot/get-started/cli-quickstart)
- [Custom agent configuration](https://docs.github.com/en/copilot/reference/custom-agents-configuration)
- [Add skills to Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills)
- [Facilitator guide](docs/facilitator-guide.md)
