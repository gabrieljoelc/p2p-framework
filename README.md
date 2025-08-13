# P2P Framework

Generic PRD-to-PR automation patterns for Claude Code.

## Quick Start

1. Clone this repo next to your client repos:
```bash
cd ~/dev/my-client
git clone git@github.com:gabrieljoelc/p2p-framework.git
```

2. Create `CLAUDE.md` in each repo that needs P2P:
```markdown
# My Repo

## P2P Pipeline
Framework: ../p2p-framework/core/p2p-workflow.md

## Commands
- Test: npm test
- Build: npm build
```

3. Start Claude Code and say: "work on [ticket-id]"

## What This Does

- Provides test-driven development patterns
- Uses `/tmp/p2p-context-{ticket-id}.md` for session persistence  
- Guides implementation from ticket → code → PR

## Files

- `core/p2p-workflow.md` - The complete P2P automation patterns

That's it. No installation, no scripts, just markdown.