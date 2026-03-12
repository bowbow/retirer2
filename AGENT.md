## Overview

This `AGENT.md` describes how AI agents (like Cursor's) should work in this repository. It is meant to be a lightweight "operator manual" so future agents can be productive and consistent without needing extra instructions from the human.

### Goals

- **Keep changes small and safe**: Prefer incremental, testable changes over large rewrites.
- **Be explicit**: Clearly state assumptions and decisions in commit messages, PR descriptions, and user-facing explanations.
- **Preserve existing behavior** unless the user explicitly requests a change or there is a clearly-identified bug.

## Project Assumptions

As of now this project has no documented architecture or stack in the repository root (no `README.md` or obvious source tree). When you, as an agent, first work on functionality:

- **Discover the stack**: Use file searches and existing code to infer language, frameworks, and build tools.
- **Document what you learn**: If you add substantial structure (e.g. first `src/` tree, first backend service, first frontend app), update or create a `README.md` with:
  - High-level purpose of the project.
  - Tech stack choices and why.
  - How to set up and run the project (commands, prerequisites).

If these assumptions become outdated, prefer updating this `AGENT.md` rather than ignoring it.

## Agent Workflow

### 1. Understand the request

- **Restate the task** in your own words (briefly) before making changes.
- **Identify constraints**: OS (Windows), tools (e.g. PowerShell), and any instructions in this `AGENT.md`.
- **Assume action is desired**: If a user asks "should we do X?" and the answer is yes, go ahead and implement X rather than waiting for further permission.

### 2. Explore the codebase

- Use recursive file search tools (`Glob`, `Grep`, or equivalent) instead of ad-hoc shell `find/grep`.
- Prefer **reading existing files** before creating new ones in that area.
- When adding new modules, keep structure coherent with whatever conventions already exist (naming, folders, test placement).

### 3. Make changes

- **Small, focused edits**:
  - Keep each change set logically cohesive (one feature or fix at a time).
  - Avoid drive-by refactors unless they are directly related and low risk.
- **No redundant comments**:
  - Only add comments that explain non-obvious intent, trade-offs, or constraints.
  - Do not narrate what each line of code does.
- **Follow language/tool best practices**:
  - For Node/TypeScript: use `npm` or `pnpm` with a lockfile, and honor existing tooling (eslint, prettier, tsconfig).
  - For Python: use `requirements.txt` or `pyproject.toml`.
  - For other stacks: align with existing conventions in the repo.

### 4. Testing and validation

- If tests or linters exist, **run them** after making non-trivial changes.
- If no tests exist:
  - Write at least minimal tests for critical logic when you introduce it.
  - Otherwise, add quick manual verification steps in your explanation (e.g. "Run `npm test`" or "Open `http://localhost:3000` and do X").

## Documentation & Files Agents Should Maintain

- **`AGENT.md` (this file)**:
  - Keep it up to date when introducing new major technologies, architectures, or workflows.
  - Add short sections instead of long essays; focus on what the *next* agent actually needs to know.
- **`README.md`**:
  - Ensure it always explains how to install dependencies, run the app, and run tests.
  - Update when adding or changing entrypoint commands.
- **Configuration files** (`package.json`, `tsconfig.json`, `pyproject.toml`, etc.):
  - Extend them conservatively; try not to break existing scripts or flows.

## Interaction Style Guidelines

When talking to the user:

- Be **concise and information-dense** by default.
- Use **clear section headings** and **bold** key points.
- Show only the **most relevant code snippets**; avoid pasting huge blocks unless explicitly requested.
- Clearly separate:
  - **What you changed**
  - **Why you changed it**
  - **How to run or verify it**

## When in Doubt

- Prefer **asking for forgiveness rather than permission** within the scope of the user’s request.
- Bias toward **creating missing structure** that is obviously needed (e.g. adding a basic `README.md`, test folder, or config) rather than leaving the project half-configured.
- If there are multiple reasonable approaches, briefly mention the trade-offs and choose one, rather than stalling.

