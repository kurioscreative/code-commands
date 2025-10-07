# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Code Commands is a collection of my experiements with Claude Code slash comands.

## Development Workflow

1. Create feature branch from `master`
2. Run tests before committing
3. Ensure migrations are reversible

## Core Code Philosophy

- Build the simplest solution that solves the immediate problem
- Follow "Make it work, make it right, make it fast" - in that order
- Every line of code is a liability. The best code is no code.

## Development Rules

### Start Minimal

- Implement the absolute minimum that satisfies current requirements
- Use constants instead of configuration options
- Direct implementation over abstract interfaces
- No "just in case" features

### Decision Framework

Before adding any code, score it:

- User explicitly requested it: +3 points
- Current code fails without it: +3 points
- We've worked around this 3+ times: +2 points
- It removes existing code: +1 point
- "Might need it later": -3 points
- "Best practice": -2 points
- "More flexible": -2 points
- Adds new abstractions: -1 point

**Only add features scoring > 0**

### Progressive Enhancement

```ruby
# Version 1: Just works
def execute(workflow)
  workflow.steps.each(&:run)
end

# Version 2: Add concurrency (only after proving bottleneck)
def execute(workflow)
  Async { workflow.steps.each(&:run) }.wait
end

# Version 3: Add timeout (only after experiencing hangs)
def execute(workflow, timeout: 300)
  Async do
    workflow.steps.each { |s| s.run_with_timeout(timeout) }
  end.wait
end
```

## Red Flags

Stop if your code has:

- Event systems with no subscribers
- Configuration for single-option features
- "revalger", "Handler", or "Registry" classes
- Mode switches that aren't used
- Checkpointing without restart crashes
- Approval systems without compliance requirements

## Testing Approach

- Test behavior, not implementation
- No mocks for things that don't exist yet
- Integration tests over unit tests for simple code

## Final Checklist

Before committing:

- [ ] Can I delete 50% and still solve the problem?
- [ ] Would a new developer understand this in 5 minutes?
- [ ] Am I solving real problems or imaginary ones?
- [ ] Have I added code for problems I've never seen?

Remember: Start simple. Add complexity only when reality forces you to.
