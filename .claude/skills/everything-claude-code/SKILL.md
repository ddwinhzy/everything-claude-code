```markdown
# everything-claude-code Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill introduces the core development patterns, coding conventions, and collaborative workflows used in the `everything-claude-code` repository. The project is a JavaScript codebase (no framework detected) that supports modular AI skills, agents, commands, and integrations. It emphasizes clear documentation, modular structure, and maintainable code with a focus on extensibility and reliability.

## Coding Conventions

- **File Naming:**  
  Use `camelCase` for JavaScript files and directories.  
  _Example:_  
  ```
  skills/textSummarizer/skillLogic.js
  agents/conversationAgent.md
  ```

- **Import Style:**  
  Use **relative imports** for local modules.  
  _Example:_  
  ```js
  const utils = require('../lib/utils');
  ```

- **Export Style:**  
  Mixed usage of CommonJS (`module.exports`) and ES module (`export`) styles depending on context.  
  _Example (CommonJS):_  
  ```js
  module.exports = function summarize(text) { ... }
  ```
  _Example (ESM):_  
  ```js
  export function summarize(text) { ... }
  ```

- **Commit Messages:**  
  Use prefixes like `fix:`, `feat:`, `docs:`, `chore:`.  
  _Example:_  
  ```
  feat: add text summarization skill with tests
  fix: correct agent registration in manifest
  ```

- **Documentation:**  
  Each skill or agent should have a `SKILL.md` or `<agent>.md` with clear usage and registration instructions.

## Workflows

### Add New Skill or Agent
**Trigger:** When introducing a new AI skill or agent to the system  
**Command:** `/add-skill`

1. Create or update `SKILL.md` in `skills/<skill-name>/` or `agents/<agent-name>.md`.
2. Optionally add supporting files (e.g., `rules/`, `references/`, `scripts/`).
3. Update `manifests/install-modules.json` to register the new skill/agent.
4. Update `AGENTS.md` and/or `README.md` to reflect the new addition.
5. Add or update tests as needed.

_Example:_
```bash
# Add a new skill
mkdir skills/textSummarizer
touch skills/textSummarizer/SKILL.md
# Register in manifest
vim manifests/install-modules.json
# Document in README.md
```

---

### Add or Extend Command Workflow
**Trigger:** When introducing or improving a CLI command  
**Command:** `/add-command`

1. Create or update `commands/<command-name>.md`.
2. Document usage, output, and YAML frontmatter.
3. Incorporate review feedback (fix placeholders, clarify sections, update templates).
4. Update references in `README.md` or related docs.

_Example:_
```markdown
# commands/summarize.md

---
name: summarize
description: Summarize input text using Claude
---

## Usage
...
```

---

### Add Install Target Workflow
**Trigger:** When integrating with a new external tool or platform  
**Command:** `/add-install-target`

1. Create a new directory for the install target (e.g., `.gemini/`, `.codebuddy/`).
2. Add install/uninstall scripts and documentation (`README.md`, `install.sh/js`, `uninstall.sh/js`).
3. Update `manifests/install-modules.json` to register the new target.
4. Update `schemas/ecc-install-config.schema.json` and/or `schemas/install-modules.schema.json`.
5. Update `scripts/lib/install-manifests.js` and `scripts/lib/install-targets/<target>.js`.
6. Update or add tests in `tests/lib/install-targets.test.js`.

---

### Refactor or Merge Skills/Agents
**Trigger:** When consolidating, merging, or refactoring skills or agents  
**Command:** `/merge-skill`

1. Update or move `SKILL.md` and related files in `skills/<name>/` or `agents/<name>.md`.
2. Update `manifests/install-modules.json` to reflect changes.
3. Update `AGENTS.md` and `README.md` to sync counts and descriptions.
4. Remove or archive deprecated files.

---

### CI Hook or Test Hardening
**Trigger:** When improving CI reliability, security, or test coverage  
**Command:** `/fix-ci`

1. Update `hooks/hooks.json` or scripts in `scripts/hooks/*.js/sh`.
2. Update or add related test files in `tests/hooks/` or `tests/scripts/`.
3. Update lockfiles (`package-lock.json`, `yarn.lock`) if dependencies change.
4. Update schemas if validation is involved.

---

### Dependency Update Workflow
**Trigger:** When updating npm or GitHub Actions dependencies  
**Command:** `/update-deps`

1. Update `package.json` and/or `yarn.lock`.
2. Update `.github/workflows/*.yml` for GitHub Actions dependencies.
3. Commit with a standard message (often via dependabot).

---

### Documentation Tightening or Expansion
**Trigger:** When clarifying, expanding, or improving documentation  
**Command:** `/docs-update`

1. Update `SKILL.md`, `README.md`, or other `docs/*.md` files.
2. Update `WORKING-CONTEXT.md` or similar context files.
3. Sync documentation across multiple language/localization files if needed.

---

## Testing Patterns

- **Test Files:**  
  Use the `*.test.js` pattern for test files.
- **Framework:**  
  No specific testing framework detected; use standard Node.js assertions or your preferred test runner.
- **Location:**  
  Place tests in the `tests/` directory, mirroring the structure of the codebase.
- **Example Test File:**
  ```js
  // tests/textSummarizer.test.js
  const summarize = require('../skills/textSummarizer/skillLogic');

  test('summarizes text correctly', () => {
    const result = summarize('This is a long text...');
    expect(result).toMatch(/summary/i);
  });
  ```

## Commands

| Command            | Purpose                                                        |
|--------------------|----------------------------------------------------------------|
| /add-skill         | Add a new skill or agent, including docs and registration      |
| /add-command       | Add or extend a CLI command with documentation                 |
| /add-install-target| Add a new install/integration target with scripts and schemas  |
| /merge-skill       | Refactor or merge skills/agents, updating docs and manifests   |
| /fix-ci            | Improve CI hooks, scripts, or test coverage                   |
| /update-deps       | Update dependencies and related workflow files                 |
| /docs-update       | Clarify, expand, or improve documentation                     |
```
