# Agents & Skills Workshop

Welcome! Over the next **60 minutes**, you’ll use a small Python book app to
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
- **pytest** for running the sample tests (optional until you want to run them):
  `python -m pip install pytest`

## Setup

Clone the workshop and check that Python and Copilot CLI are available:

```sh
git clone https://github.com/syash-git/ghcp-agents-skills.git
cd ghcp-agents-skills
python3 --version
copilot --version
```

## Workshop Guide

### The book app

The workshop uses a simple Python CLI application for managing a book collection. Both versions
are in `samples/`:

- `book-app-project/` is the main version for the review, refactoring, and
  testing modules.

  You can run this app:

```sh
cd samples/book-app-project
python3 -B book_app.py list
python book_app.py help
```

- `book-app-buggy/` is intentionally broken and used in the optional issue
  resolution module.



### Workshop modules

Developers regularly review and refactor code, write tests, and debug issues.
In this workshop, you’ll create skills for review, refactoring, and testing,
then build an agent to orchestrate that workflow. You’ll also explore issue
debugging with GitHub tools.

| Module | Time | You’ll make |
|---|---:|---|
| [1. Create a code-review checklist skill](modules/01-create-code-review-skill.md) | 8 min | A reusable quality checklist and code review template |
| [2. Create a code-review agent](modules/02-create-code-review-agent.md) | 8 min | Your first reviewer agent, explicitly connected to the checklist |
| [3. Create refactoring skills](modules/03-create-refactoring-skills.md) | 12 min | Skills and templates for planning and carrying out approved refactors |
| [4. Create a test-generation skill](modules/04-create-test-generation-skill.md) | 12 min | A procedure for adding contract-based tests |
| [5. Create a dev-workflow agent](modules/05-create-dev-workflow-agent.md) | 10 min | One agent that coordinates the skills with approval gates |
| [6. Use the GitHub MCP server](modules/06-mcp-server.md) | 10 min | Use GitHub tools from Copilot CLI |
| [7. Create an issue-resolver agent](modules/07-create-issue-resolver-agent.md) | Extra | Diagnose and fix an approved issue in a separate sample |

Modules 1–6 take about 60 minutes. Module 7 is optional.

## Helpful links

- [Copilot CLI setup](https://docs.github.com/en/copilot/get-started/cli-quickstart)
- [Custom agent configuration](https://docs.github.com/en/copilot/reference/custom-agents-configuration)
- [Add skills to Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills)
- [Facilitator guide](docs/facilitator-guide.md)
