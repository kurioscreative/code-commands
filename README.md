# Code Commands

Experiments with [Claude Code](https://claude.ai/code) slash commands.

## Usage

### Try the commands

1. Copy `agentic.md` to your project's `.claude/commands/` directory:
   ```bash
   mkdir -p .claude/commands
   cp agentic.md .claude/commands/
   ```

2. Use in Claude Code:
   ```
   /agentic Build a user authentication system with email/password
   ```

### Make commands available globally

Copy to `~/.claude/commands/` to use across all projects:
```bash
mkdir -p ~/.claude/commands
cp agentic.md ~/.claude/commands/
```

## Available Commands

- **`/agentic`** - Transform implementation requests into parallelized agentic execution with autonomous agents, automated validation, state recovery, and resource management

## Learn More

[Claude Code Slash Commands Documentation](https://docs.claude.com/en/docs/claude-code/slash-commands)
