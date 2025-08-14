# P2P Framework

Generic PRD-to-PR automation patterns for Claude Code.

## Installation

Clone this framework **INTO your partner organization's root directory**:
```bash
# Navigate to your partner/client root (where all their repos live)
cd ~/dev/partner-org  # Could be any client: imgix, ready-platform, etc.

# Clone the framework and create root CLAUDE.md
git clone git@github.com:gabrieljoelc/p2p-framework.git && touch CLAUDE.md

# Your structure should look like:
# partner-org/
# ├── p2p-framework/      # This framework
# ├── CLAUDE.md           # Root CLAUDE.md (triggers P2P)
# ├── backend-repo/       # Partner's backend repository
# ├── frontend-repo/      # Partner's frontend repository  
# └── mobile-repo/        # Partner's mobile repository
```

## Quick Start

1. Start Claude Code from the partner root:
```bash
cd ~/dev/partner-org
claude
```

2. Claude will automatically:
   - Detect the P2P framework
   - Create `CLAUDE.md` files in repos that need them
   - Auto-detect tech stack and commands

3. Start working: "work on [ticket-id]"

## Agent Architecture

The P2P agent uses modular task files for efficiency:

### Main Orchestrator
- `agent.md` - Lightweight router that loads only needed task files

### Task Files
- `tasks/setup.md` - Repository detection and CLAUDE.md creation
- `tasks/context.md` - Transient context file management  
- `tasks/implement.md` - Test-driven ticket implementation
- `tasks/pr-generation.md` - PR description and commit generation


## What This Does

- Provides test-driven development patterns
- Uses `/tmp/p2p-context-{ticket-id}.md` for session persistence  
- Auto-creates `CLAUDE.md` files in each repository
- Guides implementation from ticket → code → PR

## Usage Examples

```
Claude startup → loads tasks/setup.md → creates CLAUDE.md files
"work on READY-123" → loads tasks/context.md + tasks/implement.md
"generate pr" → loads tasks/pr-generation.md
```

That's it. No installation scripts, just markdown and Claude.