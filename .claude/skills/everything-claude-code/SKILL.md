```markdown
# everything-claude-code Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill teaches the core development patterns, coding conventions, and collaborative workflows used in the `everything-claude-code` repository. The project is primarily JavaScript (no framework), and emphasizes modular skills, agents, commands, and install targets, with a strong focus on documentation and automation. You’ll learn how to contribute new features, update documentation, manage agents and commands, and maintain CI and scripts according to established patterns.

## Coding Conventions

### File Naming
- **JavaScript files:** Use `camelCase` (e.g., `installTargets.js`, `addSkill.js`)
- **Test files:** Suffix with `.test.js` (e.g., `installTargets.test.js`)
- **Markdown docs:** Use lowercase or kebab-case (e.g., `README.md`, `AGENTS.md`)

### Import Style
- Use **relative imports** for modules:
  ```js
  const installTargets = require('./installTargets');
  ```

### Export Style
- **Mixed:** Both CommonJS (`module.exports`) and ES6 (`export`) styles may be present.
  ```js
  // CommonJS
  module.exports = function() { ... };

  // ES6
  export function addSkill() { ... }
  ```

### Commit Messages
- **Conventional commits** with prefixes: `fix`, `feat`, `docs`, `chore`
- Example:  
  ```
  feat: add support for new install target 'docker'
  ```

## Workflows

### Add or Update Skill
**Trigger:** When introducing or enhancing a skill  
**Command:** `/add-skill`

1. Create or update `skills/<skill-name>/SKILL.md` (and/or `.agents/skills/<skill-name>/SKILL.md`)
2. Optionally add/update supporting files in `rules/`, `references/`, or `assets/`
3. Update `manifests/install-modules.json` and/or `manifests/install-components.json`
4. Update `AGENTS.md`, `README.md`, and localized docs (e.g., `README.zh-CN.md`, `docs/zh-CN/AGENTS.md`)
5. Optionally update `WORKING-CONTEXT.md`

**Example:**
```bash
# Add a new skill 'summarize'
/add-skill summarize
# Then edit skills/summarize/SKILL.md and update manifests
```

---

### Add or Update Command
**Trigger:** When adding or improving a workflow command  
**Command:** `/add-command`

1. Create or update `commands/<command-name>.md`
2. Optionally update related agent or skill files
3. Update `AGENTS.md` or `README.md` if the command is significant

---

### Add or Update Agent
**Trigger:** When introducing or modifying an agent  
**Command:** `/add-agent`

1. Create or update `agents/<agent-name>.md`
2. Optionally update related skill (`skills/<skill-name>/SKILL.md`) or command files
3. Update `AGENTS.md` and/or `README.md`

---

### Add or Update Install Target
**Trigger:** When supporting a new external tool or environment  
**Command:** `/add-install-target`

1. Create or update `scripts/lib/install-targets/<target>.js`
2. Add or update `<target>` directory with `install.sh`, `uninstall.sh`, and `.codebuddy/README.md`
3. Update `manifests/install-modules.json` and/or `schemas/ecc-install-config.schema.json`
4. Update `scripts/lib/install-manifests.js`
5. Add or update tests in `tests/lib/install-targets.test.js`

**Example:**
```js
// scripts/lib/install-targets/docker.js
module.exports = function installDocker() { ... };
```

---

### Update CI or GitHub Actions
**Trigger:** When upgrading CI dependencies, workflows, or patching security  
**Command:** `/update-ci`

1. Update `.github/workflows/*.yml` files
2. Update `package.json`, `yarn.lock`, or `package-lock.json`
3. Optionally update `.github/dependabot.yml`

---

### Refactor or Harden Hooks and Scripts
**Trigger:** When optimizing, securing, or fixing hooks/scripts  
**Command:** `/refactor-hooks`

1. Update `hooks/hooks.json`
2. Modify or add `scripts/hooks/*.js` or `scripts/hooks/*.sh`
3. Update or add tests in `tests/hooks/*.test.js` or `tests/scripts/*.test.js`

---

### Documentation Update or Sync
**Trigger:** When improving, translating, or syncing documentation  
**Command:** `/update-docs`

1. Edit `README.md`, `AGENTS.md`, `WORKING-CONTEXT.md`, or localized docs
2. Edit or add `docs/*.md` or `docs/zh-CN/*.md`
3. Optionally update related skill or agent documentation

---

## Testing Patterns

- **Test files:** Use the pattern `*.test.js` (e.g., `installTargets.test.js`)
- **Framework:** Not explicitly specified; likely uses Node.js assert or a lightweight test runner.
- **Example test file:**
  ```js
  // tests/lib/install-targets.test.js
  const installTargets = require('../../scripts/lib/install-targets/docker');
  describe('installTargets', () => {
    it('should install docker', () => {
      // test implementation
    });
  });
  ```

## Commands

| Command             | Purpose                                                        |
|---------------------|----------------------------------------------------------------|
| /add-skill          | Add or update a skill, including docs and manifests            |
| /add-command        | Add or update a workflow command                               |
| /add-agent          | Add or update an agent definition                              |
| /add-install-target | Add or update an install target and related scripts/tests      |
| /update-ci          | Update CI workflows, dependencies, or GitHub Actions           |
| /refactor-hooks     | Refactor, fix, or enhance hooks and supporting scripts         |
| /update-docs        | Update or synchronize documentation and context files          |
```
