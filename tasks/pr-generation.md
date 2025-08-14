# Task: PR Generation

Generate pull request descriptions and commit messages from context.

## Prerequisites
- All ACs completed (✅ status in context)
- All tests passing
- Build successful
- Context file fully updated

## 1. Commit Message Generation

### Format
```
type: brief summary (max 50 chars)

Detailed explanation of what and why, not how.
Wrap at 72 characters.

Closes #{ticket-id}

🤖 Generated with [Claude Code](https://claude.ai/code)

Co-Authored-By: Claude <noreply@anthropic.com>
```

### Types
- `feat:` - New feature
- `fix:` - Bug fix  
- `docs:` - Documentation
- `test:` - Tests
- `refactor:` - Code refactoring
- `style:` - Code style changes
- `chore:` - Maintenance

### Example
```
feat: add user profile completion tracking

Implement percentage-based progress tracking for user profiles.
Displays completion status in mobile app and sends notification
at 50% completion to encourage profile completion.

- Add profile completion calculation service
- Create progress display component
- Integrate push notification system
- Add comprehensive test coverage

Closes #READY-123

🤖 Generated with [Claude Code](https://claude.ai/code)

Co-Authored-By: Claude <noreply@anthropic.com>
```

## 2. PR Description Generation

### Template
```markdown
## Summary
{1-2 sentence description of what changed and why}

## Acceptance Criteria
{List each AC with ✅ status}

## Key Changes
- **Architecture**: {high-level changes}
- **Features**: {user-facing changes}
- **Testing**: {test coverage added}

## Technical Implementation
- {major-technical-decision}: {reasoning}
- {pattern-used}: {why-chosen}
- {files-modified}: {what-changed}

## Test Plan
- ✅ {test-scenario-1} - PASSING
- ✅ {test-scenario-2} - PASSING
- ✅ Build verification - PASSING
- ✅ Lint checks - PASSING

<details>
<summary>📋 Implementation Context</summary>

## Detailed Technical Changes
{Extract from context file implementation notes}

## Modified Files
{List from context with descriptions}

## Test Results
{Final test run output}

## Session History
{Copy session history from context}

## P2P Pipeline Context
This work was completed using the P2P (PRD-to-PR) pipeline:
- **Test-driven development**: Tests guided implementation
- **Context preservation**: Full audit trail maintained
- **Automated workflow**: Consistent patterns applied

</details>

🤖 Generated with [Claude Code](https://claude.ai/code)
```

## 3. GitHub PR Creation URL

Generate ready-to-use GitHub URL:
```
https://github.com/{org}/{repo}/pull/new/{branch}?title={url-encoded-title}&body={url-encoded-description}
```

## 4. File Operations

### Save PR Description
```bash
cat > /tmp/{ticket-id}-pr-description.md << 'EOF'
{generated-pr-description}
EOF
```

### Copy to Clipboard (macOS)
```bash
cat /tmp/{ticket-id}-pr-description.md | pbcopy
```

## 5. Final Checklist

Before generating PR:
- [ ] All ACs marked ✅ in context
- [ ] All tests passing
- [ ] Build successful  
- [ ] Lint checks pass
- [ ] Context file complete
- [ ] Branch pushed to remote

## 6. Output Format

Provide user with:
1. **Commit message** - Ready to copy/paste
2. **PR description file** - Location of saved description
3. **GitHub URL** - Ready-to-click PR creation link
4. **Clipboard status** - "PR description copied to clipboard"

## Success Criteria
- ✅ Commit message follows conventional format
- ✅ PR description includes all context
- ✅ Technical details in collapsible section
- ✅ Files ready for user to create PR