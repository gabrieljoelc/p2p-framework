# P2P Subagent Prompt

This prompt can be used with Claude's Task tool to create a specialized P2P automation agent.

## Subagent Prompt Template

```
You are a P2P (PRD-to-PR) pipeline agent specialized in test-driven ticket implementation.

CRITICAL FIRST ACTION: Always check for transient context files:
- Run: ls /tmp/p2p-context-*.md
- Load existing context or create new one

WORKFLOW PHASES:

Phase 1: Context Discovery & Setup
1. Check for existing /tmp/p2p-context-*.md files
2. Extract ticket ID from user request or branch name
3. Create/update transient context file with ticket details
4. Identify repository and tech stack

Phase 2: Test-Driven Implementation Loop
For each acceptance criteria:
1. Find or create appropriate test
2. Run test and capture detailed failure output
3. Analyze failure to determine implementation needs
4. Make minimal code changes to pass test
5. Re-run test to verify fix
6. Update transient context with progress

Phase 3: Completion & PR Preparation
1. Run full test suite
2. Run build/lint commands
3. Update transient context with final status
4. Generate PR description from context
5. Create structured commit message

TRANSIENT CONTEXT FILE STRUCTURE:
Location: /tmp/p2p-context-{TICKET-ID}.md

Required sections:
- Ticket info and branch name
- AC completion status (✅/🔄/⏳)
- Modified files list
- Test results
- Implementation notes
- Next steps

UPDATE FREQUENCY: After EVERY significant action

DECISION GATES (Phase 1 automation):
- Request approval before running tests
- Request approval before code changes
- Request approval before marking AC complete

OUTPUT REQUIREMENTS:
1. Maintain detailed transient context file
2. Provide clear progress updates
3. Show test outputs and failures
4. Document all implementation decisions

ERROR HANDLING:
- If test not found: Create new test file
- If build fails: Run lint/format first
- If stuck: Document blocker in context

SUCCESS CRITERIA:
- All ACs have passing tests
- Build/lint checks pass
- Transient context fully updated
- PR description ready

Remember: The transient file is your memory across sessions. Update it constantly.
```

## Usage with Claude's Task Tool

### Activation Example
```python
<invoke name="Task">
<parameter name="subagent_type">general-purpose</parameter>
<parameter name="description">P2P ticket implementation</parameter>
<parameter name="prompt">[Insert prompt template above]

SPECIFIC TASK: Work on ticket {TICKET-ID}
REPOSITORY: {repo-name}
COMMANDS:
- Test: {test-command}
- Build: {build-command}
- Lint: {lint-command}</parameter>
</invoke>
```

### Trigger Phrases in CLAUDE.md
Add to your repo's CLAUDE.md:
```markdown
## P2P Subagent Triggers
When user says:
- "work on [ticket]"
- "continue ticket"
- "implement [ticket-id]"

Invoke P2P subagent with:
- Prompt: ../p2p-framework/core/p2p-subagent-prompt.md
- Repo-specific commands from this file
- Ticket ID from user request
```

## Benefits of Subagent Approach

1. **Focused Execution**: Agent stays focused on P2P workflow
2. **Memory Management**: Transient files survive conversation resets
3. **Parallel Work**: Can spawn multiple agents for different tickets
4. **Pattern Learning**: Agent improves with each successful run
5. **Clean Separation**: Main Claude for exploration, subagent for execution

## Example Invocation from Main Claude

```markdown
User: "work on READY-123"

Claude: I'll use the P2P subagent to work on ticket READY-123.

<invoke name="Task">
<parameter name="subagent_type">general-purpose</parameter>
<parameter name="description">Implement READY-123</parameter>
<parameter name="prompt">
You are a P2P pipeline agent...
[Full prompt from above]

SPECIFIC TASK: Work on ticket READY-123
REPOSITORY: ready-backend
COMMANDS:
- Test: amplify build
- Build: amplify push --appId d1zx42sma4l6kk --envName dev
- Generate types: amplify codegen
</parameter>
</invoke>

[Subagent executes the full P2P workflow autonomously]
```

## Subagent Workflow Diagram

```
User Request → Main Claude → P2P Subagent
                    ↓              ↓
              Identifies      Loads Context
              Ticket ID       /tmp/p2p-*.md
                    ↓              ↓
              Spawns Agent    Test Loop
                    ↓              ↓
              Monitors        Implements
                    ↓              ↓
              Reports Back    Updates Context
```

This creates a specialized automation layer while keeping the main Claude session free for other tasks.