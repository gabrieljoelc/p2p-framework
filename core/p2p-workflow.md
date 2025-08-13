# Core P2P Workflow Patterns

This file contains the generic P2P (PRD-to-PR) automation patterns that work across any tech stack.

## P2P Pipeline Overview

### Vision
Build a meta pipeline that automates the entire workflow from product requirements (JIRA/Linear tickets) to pull requests (GitHub/GitLab), with E2E tests as the primary feedback mechanism.

### Core Workflow
1. **Input**: Ticket/PRD with acceptance criteria
2. **Context Discovery**: Load or create transient context file
3. **Test Discovery/Creation**: Find existing test or create new one  
4. **Implementation Loop**:
   - Run test and capture failure
   - Analyze failures → Make code changes
   - Re-run test → Iterate until passing
5. **Output**: Ready-to-review PR

### Automation Phases
- **Phase 1**: Interactive with Yes/No - All changes require approval
- **Phase 2**: Semi-Automated - Tests run automatically, changes require approval
- **Phase 3**: Full Automation - Complete P2P pipeline without intervention

## P2P Subagent Instructions

### Activation Triggers
- "work on [ticket]"
- "continue ticket" 
- "check ticket status"
- "let's work on [ticket-id]"
- "what's the status?"

### Core Responsibilities
1. **Context Management**
   - ALWAYS check `/tmp/p2p-context-*.md` files first
   - Load existing context or create new transient file
   - Update context after EVERY significant action

2. **Test-Driven Implementation**  
   - Find or create test for each acceptance criteria
   - Use test failures as primary feedback mechanism
   - Run test → analyze failure → implement fix → repeat

3. **Progress Tracking**
   - Track AC completion status in real-time
   - Update transient file with technical progress
   - Maintain list of modified files and decisions

4. **Phase Gates** (Phase 1 only)
   - Request approval before running tests
   - Request approval before making code changes
   - Request approval before marking AC complete

### Context File Management Pattern
**File**: `/tmp/p2p-context-{ticket-id}.md`
**Purpose**: Preserve context across conversation resets

**Structure**:
```markdown
# P2P Context: {TICKET-ID}
## Ticket: {TICKET-ID}  
**Branch**: {branch-name}
**Status**: {In Progress | Ready for PR}

## Acceptance Criteria & Implementation Status
### ✅ COMPLETED
1. **AC Description** - Status: ✅ Complete - Test: {test} - PASSING

### 🔄 IN PROGRESS
2. **AC Description** - Status: 🔄 In Progress - Test: {test}

### ⏳ TODO  
3. **AC Description** - Status: ⏳ To Do - Test: {test}

## Technical Progress
### Modified Files
- {list of files changed}

### Test Status
- {E2E test results}
- {Unit test results}

### Implementation Notes
- {key decisions made}
- {patterns used}
- {technical debt addressed}

### Next Steps
- {remaining work}
```

## Test-Driven Development Loop

### 1. Test Discovery/Creation
- Check for existing tests that cover the acceptance criteria
- Create new test if none exists
- Use descriptive test names that match AC language

### 2. Failure Analysis
- Run test and capture detailed failure output
- Analyze failure message to understand what needs to be implemented
- Map failure back to acceptance criteria requirements

### 3. Implementation Strategy
- Make minimal changes to pass the failing test
- Follow existing code patterns and conventions
- Address one failure at a time

### 4. Verification
- Re-run test to confirm fix
- Run broader test suite to catch regressions
- Update context file with progress

## PR Generation Pattern

### Commit Message Standards
- **50/72 Rule**: Subject ≤50 chars, body wrapped at 72 chars
- **Format**: `type: subject` (feat:, fix:, docs:, test:, refactor:)
- **Subject**: Imperative mood, no period, capitalize first letter
- **Footer**: Include ticket reference and co-authorship

### PR Description Template
```markdown
## Summary
[Brief 1-2 sentence description of what changed and why]

## Key Changes
- **Architecture**: [High-level architectural changes]
- **Features**: [User-facing changes]
- **Testing**: [Test coverage added]

## Test Plan
- ✅ [E2E scenarios passing]
- ✅ [Unit tests passing]
- ✅ [Manual testing completed]

<details>
<summary>📋 Claude Context & Technical Details</summary>

[Detailed technical context from transient file]

## P2P Pipeline Context
This work was completed using the P2P (PRD-to-PR) pipeline approach:
- **Test-driven development**: Tests guided implementation
- **Context preservation**: Full implementation history available
- **Automated workflow**: Followed established patterns

</details>

🤖 Generated with [Claude Code](https://claude.ai/code)
```

## Pattern Learning & Evolution

### Successful Pattern Documentation
When a P2P workflow completes successfully:
1. Extract successful patterns from transient file
2. Document what worked well (test strategies, implementation approaches)
3. Identify reusable patterns for similar work
4. Update framework with learned patterns

### Cross-Client Pattern Promotion
- Patterns that work across multiple clients → promote to core
- Client-specific patterns → keep in client adapter
- Repo-specific patterns → document in repo CLAUDE.md

## Meta-Learning Guidelines

### What to Document
- Test failure → fix patterns that repeat across tickets
- Effective test discovery strategies  
- Common implementation approaches that work
- Build/deployment patterns that are reliable

### Pattern Categories
- **Test Patterns**: How to create effective tests for different types of requirements
- **Implementation Patterns**: Code structure and architectural approaches
- **Tool Integration**: How to integrate with different build systems, test runners
- **Error Recovery**: How to handle and recover from common failure modes