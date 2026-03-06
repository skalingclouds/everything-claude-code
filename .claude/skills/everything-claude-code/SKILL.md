# everything-claude-code Development Patterns

> Auto-generated skill from repository analysis

## Overview

The everything-claude-code repository is a comprehensive multi-platform development toolkit for AI-assisted coding environments. It provides agents, commands, skills, and configurations that work across various IDEs including Cursor, OpenCode, and VS Code extensions. The codebase emphasizes cross-platform compatibility, multi-language documentation support, and a sophisticated hook system for extensibility.

## Coding Conventions

### File Naming
- Use **camelCase** for all JavaScript files
- Skills follow pattern: `skills/[skill-name]/SKILL.md`
- Tests use suffix: `*.test.js`
- Documentation uses kebab-case: `release-notes.md`

### Import/Export Style
```javascript
// Mixed import styles supported
const { hookManager } = require('./hooks/hookManager');
import { validateConfig } from './utils/validator.js';

// Mixed export styles
module.exports = { processHooks };
export default ConfigManager;
```

### Commit Conventions
- Use conventional commit prefixes: `feat:`, `fix:`, `docs:`, `test:`, `chore:`
- Keep messages under 80 characters (average: 69 chars)
- Examples:
  ```
  feat: add new skill synchronization workflow
  fix: resolve hook loading issue in cursor integration
  docs: update multi-language documentation for v2.1
  ```

## Workflows

### Version Release
**Trigger:** When releasing a new version
**Command:** `/release`

1. Update version in `package.json`, `package-lock.json`
2. Update plugin manifests in `.claude-plugin/marketplace.json` and `.claude-plugin/plugin.json`
3. Update `.opencode/package.json` version
4. Update `README.md` with new features and changes
5. Update `CHANGELOG.md` with comprehensive release notes
6. Create release documentation in `docs/releases/[version]/release-notes.md`
7. Test across all supported platforms

**Example version update:**
```json
{
  "version": "2.1.0",
  "name": "everything-claude-code",
  "description": "Enhanced multi-platform AI coding toolkit"
}
```

### Cross-Platform Harness Sync
**Trigger:** When updating cross-platform compatibility
**Command:** `/sync-platforms`

1. Update core files in root directory (`agents/`, `commands/`, `skills/`)
2. Sync to `.cursor/` directory with Cursor-specific adaptations
3. Sync to `.opencode/` directory with OpenCode-specific TypeScript tools
4. Update `.codex/` and `.agents/` directories
5. Verify platform-specific configuration files are updated
6. Test functionality across all target platforms

**Sync pattern example:**
```bash
# Core skill created
skills/api-integration/SKILL.md
# Synced to platforms
.cursor/skills/api-integration/SKILL.md
.agents/skills/api-integration/SKILL.md
.agents/skills/api-integration/agents/openai.yaml
```

### Multi-Language Documentation
**Trigger:** When updating documentation that needs translation
**Command:** `/translate-docs`

1. Update English documentation in root directory
2. Update Chinese Simplified in `docs/zh-CN/`
3. Update Chinese Traditional in `docs/zh-TW/`
4. Update Japanese in `docs/ja-JP/`
5. Ensure consistency in structure and content across all languages
6. Validate markdown formatting and links

**Documentation structure:**
```
README.md                 # English
docs/zh-CN/README.md     # Chinese Simplified
docs/zh-TW/README.md     # Chinese Traditional  
docs/ja-JP/README.md     # Japanese
```

### Hook System Enhancement
**Trigger:** When adding new hooks or fixing hook behavior
**Command:** `/add-hook`

1. Update `hooks/hooks.json` configuration with new hook definition
2. Create or modify hook scripts in `scripts/hooks/`
3. Sync corresponding files to `.cursor/hooks/`
4. Add comprehensive tests in `tests/hooks/` and `tests/integration/`
5. Update `hooks/README.md` with usage examples
6. Test hook execution across different scenarios

**Hook configuration example:**
```json
{
  "hooks": {
    "pre-commit": {
      "script": "scripts/hooks/pre-commit.js",
      "description": "Validate code before commit"
    }
  }
}
```

### Skill Addition
**Trigger:** When adding a new skill capability
**Command:** `/add-skill`

1. Create main skill file: `skills/[skill-name]/SKILL.md`
2. Add skill to README.md skills directory listing
3. Sync skill to `.cursor/skills/[skill-name]/SKILL.md`
4. Create agent metadata in `.agents/skills/[skill-name]/SKILL.md`
5. Add OpenAI configuration: `.agents/skills/[skill-name]/agents/openai.yaml`
6. Update `skills/configure-ecc/SKILL.md` to reference new skill

**Skill template structure:**
```markdown
# [Skill Name]

## Overview
Brief description of what this skill teaches

## Usage
How to apply this skill

## Examples
Code examples and use cases
```

### Test Maintenance
**Trigger:** When tests are failing or need updates
**Command:** `/fix-tests`

1. Identify failing tests in `tests/` directory
2. Update hook tests in `tests/hooks/hooks.test.js`
3. Fix integration tests in `tests/integration/hooks.test.js`
4. Update test runner configuration in `tests/run-all.js`
5. Ensure all test suites pass before committing
6. Add new tests for any bug fixes

## Testing Patterns

### Test File Organization
```javascript
// tests/hooks/hooks.test.js
describe('Hook System', () => {
  test('should load hook configuration', () => {
    // Test implementation
  });
});

// tests/integration/hooks.test.js  
describe('Hook Integration', () => {
  test('should execute pre-commit hooks', () => {
    // Integration test
  });
});
```

### Test Naming
- Use descriptive test names: `should load hook configuration when valid config exists`
- Group related tests with `describe` blocks
- Use `test` or `it` for individual test cases

## Commands

| Command | Purpose |
|---------|---------|
| `/release` | Prepare and publish a new version release with comprehensive updates |
| `/sync-platforms` | Synchronize agents, commands, and skills across IDE platforms |
| `/translate-docs` | Update documentation across all supported language versions |
| `/add-hook` | Add or modify hook functionality across the system |
| `/add-skill` | Add new skills across all supported platforms |
| `/fix-tests` | Fix failing tests and update test infrastructure |