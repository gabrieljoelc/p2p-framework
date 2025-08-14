# Task: Repository Setup

Auto-create or update CLAUDE.md files in repositories.

## Instructions

### 1. Repository Detection
```bash
# Find all repositories (directories with .git)
find . -maxdepth 2 -type d -name ".git" | sed 's/\/.git$//' | grep -v p2p-framework
```

### 2. Tech Stack Detection

Check for these files in order:
- `package.json` → Node.js project
  - Has `next` dependency → Next.js
  - Has `react-native` → React Native
  - Has `@angular/core` → Angular
  - Default: Node.js/JavaScript

- `requirements.txt` or `pyproject.toml` → Python
  - Has `django` → Django
  - Has `fastapi` → FastAPI
  - Has `flask` → Flask
  - Default: Python

- `go.mod` → Go project
- `Gemfile` → Ruby/Rails
- `pom.xml` → Java/Maven
- `build.gradle` → Java/Gradle
- `amplify/` directory → AWS Amplify

### 3. Command Detection

Based on tech stack, set default commands:

**Node.js:**
- Test: `npm test` or `yarn test` (check which is used)
- Build: `npm run build` or `yarn build`
- Lint: `npm run lint` or `yarn lint`
- Dev: `npm run dev` or `yarn dev`

**Python:**
- Test: `pytest` or `python -m pytest`
- Build: `python -m build`
- Lint: `ruff check` or `flake8`
- Run: `python main.py` or `python manage.py runserver`

**AWS Amplify:**
- Test: `amplify mock`
- Build: `amplify build`
- Deploy: `amplify push`
- Codegen: `amplify codegen`

### 4. CLAUDE.md Creation

For each repository, create or update CLAUDE.md:

```markdown
# {repo-name}

## P2P Pipeline
**Framework**: ../p2p-framework/agent.md
**Context**: Check `/tmp/p2p-context-*.md` for active tickets

## Commands
- Test: {detected-test-command}
- Build: {detected-build-command}
- Lint: {detected-lint-command}
- Dev: {detected-dev-command}

## Tech Stack
- Language: {detected-language}
- Framework: {detected-framework}
- Package Manager: {npm/yarn/pip/etc}

## Quick Start
1. Install dependencies: {install-command}
2. Run tests: {test-command}
3. Start development: {dev-command}

## P2P Workflow
When working on tickets:
- "work on [ticket-id]" - Start new ticket
- "continue ticket" - Resume from context
- Check transient files: `ls /tmp/p2p-context-*.md`
```

### 5. Preserve Existing Content

If CLAUDE.md exists:
1. Check for "## P2P Pipeline" section
2. If missing, add at top after main heading
3. Preserve all existing content below

### Success Criteria
- ✅ All repos have CLAUDE.md files
- ✅ P2P section present in each
- ✅ Commands match actual tech stack
- ✅ Existing content preserved