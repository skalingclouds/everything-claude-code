# everything-claude-code Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches the development patterns and workflows for the everything-claude-code repository, a multi-platform AI coding assistant system that synchronizes skills and capabilities across Claude Code, Cursor, Codex, and OpenCode platforms. The codebase focuses on skill management, cross-platform compatibility, and automated workflow orchestration.

## Coding Conventions

### File Naming
- Use camelCase for JavaScript files: `skillManager.js`, `releaseHelper.js`
- Use kebab-case for directories: `skill-name`, `multi-platform-sync`
- SKILL.md files are always uppercase
- Test files follow pattern: `*.test.js`

### Import/Export Style
```javascript
// Mixed import styles supported
const { skillManager } = require('./skillManager');
import { syncPlatforms } from './platformSync.js';

// Mixed export styles
module.exports = { addSkill, updateSkill };
export default { syncToAll };
```

### Commit Patterns
- Use conventional commit prefixes: `feat:`, `fix:`, `test:`, `chore:`, `docs:`
- Keep commit messages around 73 characters
- Examples:
  ```
  feat: add new skill synchronization across platforms
  fix: resolve skill metadata parsing in SKILL.md files
  docs: update README with new skill count and directory
  ```

## Workflows

### Skill Addition
**Trigger:** When someone wants to add a new capability or domain knowledge
**Command:** `/add-skill`

1. Create `skills/{skill-name}/SKILL.md` with proper frontmatter:
   ```markdown
   ---
   title: "Skill Name"
   description: "Brief description"
   version: "1.0.0"
   ---
   ```
2. Add origin metadata and skill content to SKILL.md
3. Update README.md skill count in the stats section
4. Update README.md directory listing with new skill
5. Optionally create supporting scripts in `skills/{skill-name}/scripts/`
6. Commit with message: `feat: add {skill-name} skill`

### Multi-Platform Sync
**Trigger:** When adding skills that need to work across Claude Code, Cursor, Codex, and OpenCode
**Command:** `/sync-platforms`

1. Create or update main skill file: `skills/{name}/SKILL.md`
2. Sync to Cursor platform: `.cursor/skills/{name}/SKILL.md`
3. Add Agent configuration: `.agents/skills/{name}/SKILL.md` with `openai.yaml`
4. Update Codex agents list: `.codex/AGENTS.md`
5. Update OpenCode documentation: `.opencode/README.md`
6. Verify all platforms have consistent skill definitions
7. Commit with message: `feat: sync {name} skill across all platforms`

### Release Preparation
**Trigger:** When ready to publish a new version
**Command:** `/prepare-release`

1. Update version in `.claude-plugin/marketplace.json`:
   ```json
   {
     "version": "1.2.3",
     "name": "everything-claude-code"
   }
   ```
2. Update version in `.claude-plugin/plugin.json`
3. Update version in `.opencode/package.json`
4. Update README.md with new stats and features
5. Update root `package.json` version
6. Run release script: `scripts/release.sh`
7. Create release commit: `chore: prepare release v1.2.3`

### Pull Request Review
**Trigger:** When reviewing and merging community pull requests
**Command:** `/review-pr`

1. Review PR for security implications and code quality
2. Check if changes follow established conventions
3. Add LGTM comment with safety assessment:
   ```
   LGTM! Security check: ✅ No sensitive operations
   Code quality: ✅ Follows project conventions
   ```
4. Merge pull request using appropriate merge strategy
5. Follow up with fixes or improvements if needed
6. Update documentation if PR adds new patterns

### Hook System Update
**Trigger:** When improving the development workflow automation
**Command:** `/update-hooks`

1. Update `hooks/hooks.json` with new hook configuration:
   ```json
   {
     "pre-commit": {
       "script": "scripts/hooks/preCommit.js",
       "description": "Validate skills and sync platforms"
     }
   }
   ```
2. Create or update hook script in `scripts/hooks/{hook-name}.js`
3. Update `hooks/README.md` with documentation
4. Optionally sync to `.cursor/hooks/` for Cursor compatibility
5. Test hook functionality before committing

### Documentation Sync
**Trigger:** When documentation needs to be synchronized across locales
**Command:** `/sync-docs`

1. Update primary `README.md` with new content
2. Translate and update `README.zh-CN.md` (Simplified Chinese)
3. Update `docs/zh-TW/README.md` (Traditional Chinese)
4. Update `docs/ja-JP/README.md` (Japanese)
5. Sync any skill documentation to corresponding language directories
6. Verify all translations maintain consistent information
7. Commit: `docs: sync documentation across all languages`

### Rules System Expansion
**Trigger:** When establishing coding standards for a language or updating existing ones
**Command:** `/add-rules`

1. Create or update rule files: `rules/{language}/{category}.md`
   ```markdown
   # JavaScript Best Practices
   
   ## Naming Conventions
   - Use camelCase for variables and functions
   - Use PascalCase for classes
   ```
2. Update `rules/README.md` with new rule documentation
3. Sync to Cursor format: `.cursor/rules/{language}-{category}.md`
4. Update language-specific patterns in `skills/{language}-patterns/`
5. Test rules with existing codebase for compatibility

## Testing Patterns

Tests follow the `*.test.js` pattern and are located alongside source files:

```javascript
// skillManager.test.js
const { addSkill, validateSkill } = require('./skillManager');

describe('Skill Management', () => {
  test('should validate skill metadata', () => {
    const skill = { name: 'test-skill', version: '1.0.0' };
    expect(validateSkill(skill)).toBe(true);
  });
});
```

## Commands

| Command | Purpose |
|---------|---------|
| `/add-skill` | Add a new skill with proper structure and metadata |
| `/sync-platforms` | Synchronize skills across all supported AI platforms |
| `/prepare-release` | Update version numbers and prepare for release |
| `/review-pr` | Review and merge community pull requests safely |
| `/update-hooks` | Add or modify development workflow hooks |
| `/sync-docs` | Update documentation across all supported languages |
| `/add-rules` | Create or update coding standards for languages |