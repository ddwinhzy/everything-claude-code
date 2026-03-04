# everything-claude-code Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill covers development patterns for the everything-claude-code repository, a comprehensive collection of AI coding tools, skills, and agents designed to work across multiple platforms (Claude Code, Cursor, Codex, OpenCode). The codebase emphasizes multi-language documentation, cross-platform compatibility, and systematic skill management with continuous learning capabilities.

## Coding Conventions

### File Naming
- Use **camelCase** for JavaScript files: `skillManager.js`, `observerScript.js`
- Use **kebab-case** for directories: `continuous-learning-v2/`, `zh-CN/`
- Use **UPPERCASE** for main documentation: `SKILL.md`, `AGENTS.md`, `README.md`

### Import/Export Patterns
```javascript
// Mixed import styles are acceptable
import { skillManager } from './utils/skillManager.js';
const { observerUtils } = require('./scripts/observer');

// Mixed export styles
export default function createSkill() { ... }
module.exports = { hookHandler, processInstinct };
```

### Testing Conventions
- Test files follow pattern: `*.test.js`
- Place tests adjacent to source files or in dedicated `tests/` directories
- Focus on workflow automation and hook behavior testing

## Workflows

### Multi-Language Documentation Sync
**Trigger:** When core documentation is updated and needs to be propagated to all language variants  
**Command:** `/sync-docs-i18n`

1. Update the English source documentation in root or `docs/`
2. Sync Chinese translations in `docs/zh-CN/`
3. Update Traditional Chinese variants in `docs/zh-TW/`
4. Sync Japanese versions in `docs/ja-JP/`
5. Update all README files across language directories
6. Verify skill counts and links are consistent across all versions

```bash
# Example sync command structure
./scripts/sync-i18n.sh --source=README.md --targets=zh-CN,zh-TW,ja-JP
```

### Skill Addition Workflow
**Trigger:** When creating a new skill that needs to work across Claude Code, Cursor, Codex, and OpenCode  
**Command:** `/new-skill`

1. Create main `SKILL.md` file in `skills/[skill-name]/`
2. Add skill to primary skills directory with proper structure
3. Create `.cursor/skills/[skill-name]/SKILL.md` variant for Cursor IDE
4. Add `.agents/skills/[skill-name]/` with `openai.yaml` configuration
5. Update `README.md` skill count and directory listings
6. Test skill loading across all supported platforms

```markdown
<!-- Standard skill structure -->
skills/
  my-new-skill/
    SKILL.md
    agents/
      assistant.md
    scripts/
      helper.js
```

### PR Merge with Metadata Updates
**Trigger:** When merging significant features that require version bumps  
**Command:** `/merge-and-release`

1. Review and merge the pull request
2. Update version number in `package.json`
3. Update version in `.claude-plugin/plugin.json`
4. Modify metadata in `.claude-plugin/marketplace.json`
5. Update README with new features and capabilities
6. Run release script to publish changes

```json
// Version update pattern
{
  "version": "1.2.3",
  "description": "Updated with new skill management features"
}
```

### Hook Script Refactoring
**Trigger:** When inline hooks in hooks.json become too complex or cause parsing issues  
**Command:** `/extract-hook`

1. Create new script file in `scripts/hooks/[hook-name].js`
2. Extract inline JavaScript from `hooks/hooks.json`
3. Update `hooks.json` to reference external script file
4. Add comprehensive tests for hook behavior in `tests/hooks/`
5. Update hook documentation in `hooks/README.md`

```javascript
// External hook script example
// scripts/hooks/skillValidator.js
module.exports = function validateSkill(context) {
  const { filePath, content } = context;
  // Validation logic here
  return { valid: true, suggestions: [] };
};
```

### Continuous Learning System Updates
**Trigger:** When the observer background process or instinct management needs fixes  
**Command:** `/fix-observer`

1. Identify issues in observer script (`skills/continuous-learning-v2/agents/start-observer.sh`)
2. Update instinct CLI tool (`skills/continuous-learning-v2/scripts/instinct-cli.py`)
3. Modify agent prompts and behavior patterns
4. Update skill documentation with new capabilities
5. Add safety guards and error handling mechanisms

```python
# Example instinct CLI pattern
def process_instinct(observation, context):
    if validate_safety(observation):
        return generate_response(observation, context)
    return fallback_response()
```

### Cross-Platform Harness Sync
**Trigger:** When adding support for new AI tools or syncing existing configurations  
**Command:** `/sync-harnesses`

1. Update universal `AGENTS.md` file with new platform support
2. Sync configurations in `.cursor/` directory for Cursor IDE
3. Update `.codex/` setup files for GitHub Codex integration
4. Modify `.opencode/` tools for OpenCode platform
5. Add platform-specific adaptations and compatibility layers
6. Test installation script across all platforms

## Testing Patterns

### Hook Testing
```javascript
// tests/hooks/skillValidator.test.js
const validator = require('../../scripts/hooks/skillValidator');

test('validates skill structure', () => {
  const mockSkill = { name: 'test-skill', content: '# Test Skill' };
  const result = validator(mockSkill);
  expect(result.valid).toBe(true);
});
```

### Workflow Integration Testing
```javascript
// tests/workflows/skillAddition.test.js
test('new skill workflow creates all required files', async () => {
  await runWorkflow('new-skill', { name: 'test-skill' });
  expect(fs.existsSync('skills/test-skill/SKILL.md')).toBe(true);
  expect(fs.existsSync('.cursor/skills/test-skill/SKILL.md')).toBe(true);
});
```

## Commands

| Command | Purpose |
|---------|---------|
| `/sync-docs-i18n` | Synchronize documentation across all language versions |
| `/new-skill` | Create a new skill with cross-platform compatibility |
| `/merge-and-release` | Merge PR and update all version metadata |
| `/extract-hook` | Convert inline hooks to external script files |
| `/fix-observer` | Update continuous learning system components |
| `/sync-harnesses` | Synchronize configurations across AI tool platforms |
| `/validate-structure` | Check repository structure and file consistency |
| `/update-counts` | Update skill counts in README files |
| `/test-workflows` | Run integration tests for all workflows |