# P2P Framework

Generic PRD-to-PR automation patterns for Claude Code.

## Installation

Clone this framework **INTO your organization's root directory**:
```bash
# Navigate to your organization root (where all repos live)
cd ~/dev/org  # Could be any organization

# Clone the framework and create root CLAUDE.md with P2P agent activation
git clone git@github.com:gabrieljoelc/p2p-framework.git && echo "# Organization Root

## P2P Agent
**Source**: ./p2p-framework/agent.md

When user mentions tickets, automatically use the P2P agent:
- \"work on [ticket-id]\" → Load tasks/context.md + tasks/implement.md  
- \"set up p2p\" → Load tasks/setup.md
- \"generate pr\" → Load tasks/pr-generation.md" > CLAUDE.md

# Your structure should look like:
# org/
# ├── p2p-framework/      # This framework
# ├── CLAUDE.md           # Root CLAUDE.md (triggers P2P)
# ├── backend-repo/       # Organization's backend repository
# ├── frontend-repo/      # Organization's frontend repository  
# └── mobile-repo/        # Organization's mobile repository
```

## Quick Start

1. Start Claude Code from the org root:
```bash
cd ~/dev/org
claude
```

2. The P2P agent will:
   - Detect repositories and create `CLAUDE.md` files
   - Auto-detect tech stack and commands
   - Activate when you mention tickets

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
"work on TICKET-123" → loads tasks/context.md + tasks/implement.md
"generate pr" → loads tasks/pr-generation.md
```

## Documentation

- **README.md** - Installation and quick start (this file)
- **CHANGELOG.md** - Release history and version changes
- **ROADMAP.md** - Future plans and development phases
- **agent.md** - Main P2P agent orchestrator
- **tasks/** - Modular task files for specific operations

That's it. No installation scripts, just markdown and Claude.