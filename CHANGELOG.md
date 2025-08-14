# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

## [0.1.0] - 2025-01-13

### Added
- **Modular agent architecture** with lightweight orchestrator and task-specific files
- **Auto-setup system** that detects repositories and creates CLAUDE.md files automatically
- **Tech stack detection** for Node.js, Python, Go, AWS Amplify, and more
- **Command detection** for test, build, lint, and dev operations
- **Transient context files** (`/tmp/p2p-context-*.md`) for session persistence
- **Test-driven development workflow** with acceptance criteria tracking
- **PR generation** with structured descriptions and commit messages
- **Open source compatibility** with generic terminology and examples

### Architecture
- `agent.md` - Main orchestrator that loads only needed task files
- `tasks/setup.md` - Repository detection and CLAUDE.md creation
- `tasks/context.md` - Session state management across conversations
- `tasks/implement.md` - Test-driven ticket implementation workflow
- `tasks/pr-generation.md` - PR description and commit message generation

### Installation
- Simple one-line setup: `git clone && echo > CLAUDE.md`
- Automatic agent activation when Claude starts
- No scripts or dependencies required