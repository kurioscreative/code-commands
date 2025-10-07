---
description: Transform implementation requests into parallelized agentic execution with autonomous agents and automated validation
argument-hint: <goal/description> or @document
allowed-tools:
  - Read
  - Write
  - Edit
  - Bash
  - Glob
  - Grep
  - Task
  - TodoWrite
---

# Agentic Decomposition & Execution

You are now in **agentic mode**. Transform the user's request into a parallelized execution strategy using autonomous agents.

## Input Analysis

User request: $ARGUMENTS

### Phase 1: Analyze & Extract Goals

1. **Parse the input** to identify:
   - Primary deliverables (what to build)
   - Technical constraints (versions, frameworks, patterns)
   - Success indicators (tests, metrics, behaviors)
   - Scope boundaries (included/excluded)

2. **Assess complexity**:
   - Single-file change? → Use sequential, not agentic
   - Multiple independent subsystems? → Good for agentic
   - Clear phases/dependencies? → Good for agentic
   - Exploratory/research-heavy? → Use sequential

3. **Verify readiness**:
   - Sufficient codebase context?
   - Objective success criteria definable?
   - Dependencies mappable?
   - Parallelization opportunities exist?

4. **Present initial assessment**:

```markdown
## Agentic Decomposition Analysis

**Input**: [User's request]
**Complexity**: [Low/Medium/High]
**Agentic Suitability**: [Well-suited / Marginal / Not recommended]

**Identified Goals**:
1. [Goal 1] - [complexity]
2. [Goal 2] - [complexity]
3. [Goal 3] - [complexity]

**Potential Agents**: [N agents across M sequences]
**Estimated Time**: [X hours sequential vs Y hours agentic]
**Speedup Factor**: [X/Y ratio]

**Proceed with agentic decomposition?** [Y/n]
```

### Phase 2: Qualifying Questions (If Needed)

Ask questions ONLY when:
- Success criteria unclear ("fast" - how fast?)
- Multiple implementation paths ("auth" - OAuth? JWT?)
- Scope ambiguous ("dashboard" - what metrics?)
- Dependencies unknown (existing auth? database?)

**Question format**:

```markdown
## Clarifying Questions

Before creating the execution plan, I need to clarify:

**Technical**:
1. [Tech stack question]
2. [Version/framework question]

**Scope**:
3. [Boundaries question]
4. [MVP vs full question]

**Success**:
5. [Verification question]
6. [Metrics question]

Please answer, or reply "use defaults" to proceed with reasonable assumptions.
```

### Phase 3: Generate Agentic Decomposition

Using REPEATABLE_AGENTIC_DECOMPOSITION_PROCESS.md methodology:

1. **Extract agent tasks** following agent-readiness criteria
2. **Create detailed agent prompts** with:
   - Context (what exists, what's needed)
   - Task (specific objective)
   - Requirements (technical specs)
   - Deliverable (files, code, tests)
   - Success Criteria (3-5 objective, verifiable criteria - NO "looks good")

3. **Map dependencies** and identify parallel opportunities
4. **Organize into sequences** (sequential or parallel)

**Present execution plan**:

```markdown
# Agentic Execution Plan: [Feature Name]

## Summary
- **Goal**: [High-level objective]
- **Total Agents**: [N]
- **Sequences**: [M]
- **Parallel Opportunities**: [P agents concurrent]
- **Estimated Time**: [X hours]

## Agent Breakdown

### SEQUENCE 1: [Phase Name] (Sequential/Parallel)

#### Agent 1: [Task Name]
- **Creates**: [file paths]
- **Tests**: [test approach]
- **Depends on**: [none/Agent X]
- **Success Criteria**:
  - [Objective criterion 1]
  - [Objective criterion 2]
  - [Objective criterion 3]
- **Time**: [N minutes]

#### Agent 2: [Task Name]
- **Creates**: [file paths]
- **Tests**: [test approach]
- **Depends on**: [Agent 1]
- **Success Criteria**:
  - [Objective criterion 1]
  - [Objective criterion 2]
  - [Objective criterion 3]
- **Time**: [N minutes]

---

### SEQUENCE 2: [Phase Name] (Parallel)

#### Agent 3: [Task Name] (PARALLEL)
[... same structure ...]

#### Agent 4: [Task Name] (PARALLEL)
[... same structure ...]

---

## Dependency Graph

```
Agent 1 (Foundation)
    ↓
Agent 2 (Models)
    ↓
    ┌────┴────┐
Agent 3    Agent 4  (PARALLEL)
    └────┬────┘
    Agent 5
```

## Validation Gates

- **After Sequence 1**: Verify [specific artifact]
- **After Sequence 2**: Test [specific integration]
- **Final**: Confirm [overall success criteria]

## Risks & Mitigations

- **Risk**: [Potential issue]
  **Mitigation**: [How to handle]

---

**Approve this plan to begin execution?** [Y/n/modify]
```

### Phase 4: Handle User Response

- **Y/yes/approve** → Proceed to execution
- **modify [change]** → Regenerate plan with changes, re-present
- **n/no/cancel** → Exit agentic mode, offer sequential alternative
- **[question]** → Answer, re-present plan

### Phase 5: Execute Agents

Use TodoWrite to track progress. For each sequence:

1. **Pre-sequence check**:
   ```
   - Verify prerequisites (files exist, data ready)
   - Report: Starting sequence N of M
   - List agents (parallel/sequential)
   ```

2. **Agent execution**:
   - Use Task tool with general-purpose agent
   - Display: "Agent N: [Task Name] - Starting"
   - Execute with detailed prompt including:
     - Full context
     - Specific task
     - Requirements
     - Deliverable expectations
     - Success criteria
   - Capture output
   - Verify success criteria with actual commands
   - Display: "Agent N: [Status] ✅/❌"

3. **Validation gate**:
   - Run verification commands
   - Check success criteria
   - Report results
   - If critical: pause for human review

4. **Progress display**:

```markdown
═══════════════════════════════════════════════════════
🤖 AGENTIC EXECUTION: [Feature Name]
═══════════════════════════════════════════════════════

📊 Progress: Sequence 2 of 4 (50% complete)

✅ SEQUENCE 1: Foundation (Complete - 15 min)
   ✅ Agent 1: Database schema
   ✅ Agent 2: ActiveRecord models
   ✅ Agent 3: Seed data

🔄 SEQUENCE 2: Services (Running - 8/20 min)
   ✅ Agent 4: Schedule generator
   🔄 Agent 5: PDF generator (in progress...)
   ⏳ Agent 6: Print controller (waiting on Agent 5)

⏳ SEQUENCE 3: UI Layer (Pending)
⏳ SEQUENCE 4: Integration (Pending)

⏱️  Elapsed: 23 min | Remaining: ~37 min
═══════════════════════════════════════════════════════
```

**Success criteria verification format**:

```markdown
Agent 5: PDF Generator - Verification

Running success criteria checks:

✅ 1. PDF renders without errors
   $ WeeklyPrintGenerator.new(...).generate_pdf
   → Prawn::Document generated successfully

✅ 2. File exists at tmp/sample_week.pdf
   $ ls -la tmp/sample_week.pdf
   → -rw-r--r-- 1 user staff 6084 Oct 3 12:34 tmp/sample_week.pdf

✅ 3. Valid PDF format
   $ file tmp/sample_week.pdf
   → PDF document, version 1.3, 1 pages

RESULT: All criteria passed ✅
```

**Error handling**:

```markdown
❌ Agent 5: PDF Generator - FAILED

Success criteria failures:
✅ 1. PDF renders without errors
❌ 2. Valid PDF format
   Expected: PDF document
   Actual: empty file

Error: Prawn::Errors::UnknownFont: 'Helvetica-Bold' not found

Suggested fix: Add font registration to WeeklyPrintGenerator

Options:
1. [R]etry with refined prompt
2. [S]kip this agent
3. [A]bort execution
4. [M]anual intervention

Choose: [R/S/A/M]
```

### Phase 6: Completion Summary

```markdown
═══════════════════════════════════════════════════════
✅ AGENTIC EXECUTION COMPLETE: [Feature Name]
═══════════════════════════════════════════════════════

## Summary Statistics

**Total Time**: 1h 23min (vs 4h 30min sequential)
**Speedup**: 3.2× faster
**Agents**: 11 executed (11 succeeded, 0 failed)
**Tests**: 87 examples, 0 failures
**Files Created**: 23
**Files Modified**: 5

## Sequences Completed

✅ SEQUENCE 1: Foundation (3 agents, 18 min)
✅ SEQUENCE 2: Services (3 agents, 32 min)
✅ SEQUENCE 3: UI Layer (2 agents, 19 min)
✅ SEQUENCE 4: Integration (3 agents, 14 min)

## Files Created

**Models** (5):
- app/models/household.rb
- app/models/task.rb
[... list all files ...]

**Services** (3):
- app/services/weekly_schedule_generator.rb
[... list all files ...]

## Validation Results

✅ All routes registered (6 routes)
✅ All migrations up (5 migrations)
✅ All tests passing (87/87)
✅ Database seeded

## Quick Start

```bash
# Commands to run the feature
rails s
# Visit URLs or test commands
```

## Next Steps

[Suggest logical next phase or related work]

═══════════════════════════════════════════════════════
```

## Important Rules

1. **Agent Prompts Must**:
   - Include full context (files, structure, patterns)
   - State specific task clearly
   - List all requirements
   - Define expected deliverable
   - Provide 3-5 objective success criteria (verifiable by command/test)
   - Specify time estimate

2. **Success Criteria Must**:
   - Be objective and verifiable
   - Use specific commands to verify
   - Never use subjective terms ("looks good", "works well")
   - Test actual functionality

3. **Parallelization**:
   - Only parallelize truly independent agents
   - Agents in same sequence can run parallel if no shared dependencies
   - Use Task tool to launch agents
   - If launching parallel agents, use single message with multiple Task calls

4. **Progress Tracking**:
   - Use TodoWrite for all sequences and agents
   - Mark in_progress before starting
   - Mark completed immediately after success
   - Keep user informed with progress displays

5. **Error Recovery**:
   - Automatic retry with refined prompt (first failure)
   - Offer options on repeated failure
   - Never silently skip failures
   - Always verify success criteria

6. **Validation**:
   - Run actual verification commands
   - Show command output
   - Confirm each success criterion
   - Pause at validation gates if critical

## Git Integration

Before execution:
- Create branch: `agentic/[feature-name]-[date]`
- Baseline commit: "Pre-agentic execution baseline"

After each sequence:
- Commit: "Agentic: Sequence N - [Phase Name] (Agents X-Y)"

On completion:
- Final commit: "Agentic: Complete - [Feature Name]"

## Reference Documents
- See project CLAUDE.md for tech stack and patterns

---

**Now begin Phase 1: Analyze the user's request and provide initial assessment.**
