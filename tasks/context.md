# Task: Context Management

Manage transient context files for session persistence.

## Context File Location
`/tmp/p2p-context-{ticket-id}.md`

## 1. Context Discovery

### Check for Existing Context
```bash
ls /tmp/p2p-context-*.md
```

### Extract Ticket ID
From user input or branch name:
- "work on READY-123" → `READY-123`
- Branch: `ENG-456-user-auth` → `ENG-456`
- Continue: Load most recent context file

## 2. Context File Structure

```markdown
# P2P Context: {TICKET-ID}

## Ticket Information
**ID**: {ticket-id}
**Title**: {ticket-title}
**Branch**: {branch-name}
**Repository**: {repo-name}
**Status**: {In Progress | Ready for PR | Blocked}

## Acceptance Criteria
### ✅ COMPLETED
1. **AC Description** - Test: {test-name} - PASSING - Files: {modified-files}

### 🔄 IN PROGRESS  
2. **AC Description** - Test: {test-name} - Status: {implementation-notes}

### ⏳ TODO
3. **AC Description** - Test: {not-created-yet}

## Technical Progress
### Modified Files
- {file-path} - {what-changed}
- {file-path} - {what-changed}

### Test Results
- Last test run: {timestamp}
- Passing: {count}
- Failing: {count}
- Build status: {pass/fail}

### Implementation Notes
- {decision-made}: {reasoning}
- {pattern-used}: {why-chosen}
- {blocker}: {how-resolved}

### Next Steps
- [ ] {remaining-task}
- [ ] {remaining-task}

## Commands Used
- Test: {command-from-repo-claude}
- Build: {command-from-repo-claude}  
- Lint: {command-from-repo-claude}

## Session History
### {timestamp} - Session 1
- {what-was-accomplished}

### {timestamp} - Session 2  
- {what-was-accomplished}
```

## 3. Update Frequency

Update context file after:
- ✅ Each test run (pass/fail)
- ✅ Each code change
- ✅ Each AC completion
- ✅ Each decision made
- ✅ Each session start/end

## 4. Context Loading

When resuming:
1. Load existing context file
2. Display current status summary
3. Identify next action from "Next Steps"
4. Continue from where left off

## 5. Context Creation

For new tickets:
1. Extract ticket info from user
2. Create initial context structure
3. Set all ACs to ⏳ TODO
4. Initialize empty progress sections

## 6. Cross-Session Persistence

The context file:
- ✅ Survives conversation resets
- ✅ Maintains full history
- ✅ Enables seamless resumption
- ✅ Provides audit trail

## Success Criteria
- ✅ Context file exists and is current
- ✅ All progress documented
- ✅ Next steps clearly defined
- ✅ Can resume from any point