# everything-claude-code Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches the development patterns for `everything-claude-code`, a cross-platform AI coding assistant system that works across multiple IDEs (Claude, Cursor, Codex, OpenCode). The codebase focuses on skill management, hook systems, continuous learning, and multi-language documentation synchronization. It emphasizes consistent behavior across different AI development environments and maintains a plugin-based architecture.

## Coding Conventions

### File Naming
- Use **camelCase** for JavaScript files: `multiExecute.js`, `skillManager.js`
- Use **kebab-case** for documentation: `SKILL.md`, `README.md`
- Test files follow pattern: `*.test.js`

### Import/Export Style
```javascript
// Mixed import styles accepted
import { skillManager } from './skillManager.js';
const { executeHook } = require('./hooks/hookManager');

// Mixed export styles
export default class SkillManager { }
module.exports = { executeWorkflow };
```

### Directory Structure
```
skills/[skill-name]/SKILL.md
.cursor/skills/[skill-name]/SKILL.md
.agents/skills/[skill-name]/SKILL.md
.agents/skills/[skill-name]/agents/openai.yaml
commands/[command-name].md
docs/[lang]/[section]/
```

## Workflows

### Version Release
**Trigger:** When ready to release a new version
**Command:** `/release`

1. Update version in `package.json`
2. Update plugin manifests in `.claude-plugin/marketplace.json` and `.claude-plugin/plugin.json`
3. Update `CHANGELOG.md` with new features and fixes
4. Create release documentation in `docs/releases/*/`
5. Update main `README.md` if needed
6. Tag and publish release

```json
// .claude-plugin/plugin.json
{
  "version": "1.2.3",
  "name": "everything-claude-code"
}
```

### Cross-Platform Skill Addition
**Trigger:** When adding a new skill to the system
**Command:** `/add-skill`

1. Create base skill in `skills/[skill-name]/SKILL.md`
2. Copy to `.cursor/skills/[skill-name]/SKILL.md`
3. Copy to `.agents/skills/[skill-name]/SKILL.md`
4. Create OpenAI agent config in `.agents/skills/[skill-name]/agents/openai.yaml`
5. Update main `README.md` with skill reference
6. Update `.opencode/README.md` for OpenCode platform

```yaml
# .agents/skills/[skill-name]/agents/openai.yaml
name: skill-name
model: gpt-4
temperature: 0.7
system_prompt: |
  You are a specialized agent for [skill-name]...
```

### Documentation Translation Sync
**Trigger:** When updating core documentation that needs translation
**Command:** `/sync-translations`

1. Update English documentation first
2. Sync changes to `docs/zh-CN/` (Chinese Simplified)
3. Sync changes to `docs/zh-TW/` (Chinese Traditional)  
4. Sync changes to `docs/ja-JP/` (Japanese)
5. Maintain consistent file structure across all language directories
6. Verify all cross-references are updated

### Hook System Enhancement
**Trigger:** When adding new hook functionality or fixing hook behavior
**Command:** `/add-hook`

1. Update `hooks/hooks.json` with new hook definition
2. Add/modify script in `scripts/hooks/[hook-name].js`
3. Update corresponding `.cursor/hooks/[hook-name].js`
4. Add tests in `tests/hooks/[hook-name].test.js` or `tests/integration/`
5. Update `hooks/README.md` documentation

```json
// hooks/hooks.json
{
  "pre-commit": {
    "script": "scripts/hooks/preCommit.js",
    "description": "Run linting and tests before commit"
  }
}
```

### Multi-Command Updates
**Trigger:** When modifying behavior of multi-plan, multi-execute, multi-workflow commands
**Command:** `/update-multi-commands`

1. Update base command in `commands/[multi-command].md`
2. Update all `multi-*` variants consistently
3. Sync translations in `docs/ja-JP/commands/multi-*.md`
4. Sync translations in `docs/zh-CN/commands/multi-*.md`
5. Test consistency across all variants

### Continuous Learning System Updates
**Trigger:** When improving the continuous learning loop functionality
**Command:** `/update-learning-system`

1. Update `skills/continuous-learning-v2/SKILL.md`
2. Modify observer agents in `skills/continuous-learning-v2/agents/`
3. Update instinct scripts in `skills/continuous-learning-v2/scripts/`
4. Add/update commands: `commands/instinct-*.md`, `commands/projects.md`, `commands/promote.md`
5. Update configuration files for learning parameters

### Plugin Manifest Sync
**Trigger:** When version changes or plugin capabilities are updated
**Command:** `/sync-plugin-manifests`

1. Update version in `.claude-plugin/plugin.json`
2. Update `.claude-plugin/marketplace.json` with matching version
3. Ensure `package.json` version is synchronized
4. Update component declarations if capabilities changed
5. Validate all plugin manifests for consistency

## Testing Patterns

```javascript
// Test file naming: *.test.js
// tests/hooks/preCommit.test.js
describe('Pre-commit hook', () => {
  it('should run linting before commit', async () => {
    const result = await executeHook('pre-commit');
    expect(result.success).toBe(true);
  });
});
```

## Commit Conventions

- **feat:** New features
- **fix:** Bug fixes  
- **docs:** Documentation updates
- **test:** Test additions/modifications
- **chore:** Maintenance tasks
- Average commit message length: ~69 characters

## Commands

| Command | Purpose |
|---------|---------|
| `/release` | Prepare and publish a new version release |
| `/add-skill` | Add a new skill across all IDE platforms |
| `/sync-translations` | Synchronize documentation translations |
| `/add-hook` | Add or modify hook system functionality |
| `/update-multi-commands` | Update multi-* command family consistently |
| `/update-learning-system` | Enhance continuous learning capabilities |
| `/sync-plugin-manifests` | Keep plugin manifests synchronized |