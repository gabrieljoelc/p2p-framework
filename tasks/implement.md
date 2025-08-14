# Task: Ticket Implementation

Test-driven development workflow for implementing tickets.

## Prerequisites
Load `tasks/context.md` first to establish ticket state.

## Phase 1: Setup & Discovery

### 1. Extract Ticket Information
From user request or existing context:
- Ticket ID (e.g., TICKET-123, ENG-456)
- Acceptance criteria
- Repository to work in

### 2. Branch Management
```bash
# Create feature branch if not exists
git checkout -b {ticket-id}-{short-description}

# Or switch to existing branch
git checkout {existing-branch}
```

### 3. Repository Commands
Read commands from current repo's CLAUDE.md:
- Test command
- Build command  
- Lint command

## Phase 2: Test-Driven Loop

For **each acceptance criteria**:

### 1. Test Discovery/Creation
- Check existing test files for coverage
- Create new test if needed
- Name test to match AC: `test_{ac_description}`

### 2. Test Execution
```bash
{test-command}  # From repo CLAUDE.md
```
- Capture full output
- Identify specific failures
- Document failure reason

### 3. Implementation
- Make **minimal** changes to pass failing test
- Follow existing code patterns
- Don't implement more than needed

### 4. Verification
```bash
{test-command}    # Re-run specific test
{build-command}   # Ensure build works
{lint-command}    # Check code quality
```

### 5. Context Update
Update `/tmp/p2p-context-{ticket-id}.md`:
- Mark AC as ✅ Complete or 🔄 In Progress
- Add modified files
- Document implementation decisions

## Phase 3: Quality Checks

### Full Test Suite
```bash
{test-command}  # Run all tests
```

### Build Verification
```bash
{build-command}  # Full build
```

### Code Quality
```bash
{lint-command}  # Lint checks
```

## Decision Gates (Phase 1 Automation)
Before each action, request approval:
- "Run test for AC #{number}? (y/n)"
- "Make code changes to implement? (y/n)"
- "Mark AC as complete? (y/n)"

## Error Handling

### Test Creation Failed
- Check test directory structure
- Look for existing test patterns
- Create minimal test file

### Build Failed
- Run lint/format first
- Check import paths
- Document build error in context

### Implementation Stuck
- Document blocker in context
- Request user guidance
- Provide current state summary

## Success Criteria
- ✅ All ACs have passing tests
- ✅ Full test suite passes
- ✅ Build succeeds
- ✅ Lint checks pass
- ✅ Context file updated