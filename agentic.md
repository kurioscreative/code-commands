---
description: Transform implementation requests into parallelized agentic execution with autonomous agents, automated validation, state recovery, and resource management.
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

You are now in **agentic mode**. Transform the user's request into a production-ready, parallelized execution strategy with comprehensive safeguards.

## Input Analysis

User request: $ARGUMENTS

### Phase 1: Analyze & Extract Goals

1. **Parse the input** to identify:
   - Primary deliverables (what to build)
   - Technical constraints (versions, frameworks, patterns)
   - Success indicators (tests, metrics, behaviors, performance)
   - Scope boundaries (included/excluded)
   - Quality requirements (security, performance, accessibility)

2. **Assess complexity**:
   - Single-file change? → Use sequential, not agentic
   - Multiple independent subsystems? → Good for agentic
   - Clear phases/dependencies? → Good for agentic
   - Exploratory/research-heavy? → Use sequential

3. **Assess risk factors**:
   - **Conflict Risks**:
     - Parallel agents likely to touch same files? → Flag
     - File/resource conflicts possible? → Flag
     - State dependencies unclear? → Flag
   - **Resource Risks**:
     - API/cost intensive operations? → Flag, estimate costs
     - High concurrency (>5 parallel agents)? → Flag, add limits
     - Large context requirements? → Flag, plan chunking
   - **Quality Risks**:
     - Security-sensitive code? → Flag for security scanning
     - Performance-critical paths? → Flag for benchmarking
     - Public-facing features? → Flag for accessibility checks

4. **Estimate resource costs**:
   - Agent count × average tokens per agent
   - Estimated LLM API cost range
   - Flag if cost exceeds threshold ($1+ estimated)

5. **Verify readiness**:
   - Sufficient codebase context?
   - Objective success criteria definable?
   - Dependencies mappable into acyclic graph?
   - Parallelization opportunities exist?
   - Conflict risks manageable?
   - Resource costs acceptable?

6. **Present initial assessment**:

```markdown
## Agentic Decomposition Analysis

**Input**: [User's request]
**Complexity**: [Low/Medium/High]
**Agentic Suitability**: [Well-suited / Marginal / Not recommended]

**Identified Goals**:

1. [Goal 1] - [complexity] - [performance requirement if any]
2. [Goal 2] - [complexity] - [security consideration if any]
3. [Goal 3] - [complexity]

**Decomposition Metrics**:

- **Potential Agents**: [N agents across M sequences]
- **Max Parallel**: [P concurrent agents]
- **Estimated Time**: [X hours sequential vs Y hours agentic]
- **Speedup Factor**: [X/Y ratio]
- **Estimated Cost**: $[low]-$[high] (based on ~[tokens]k tokens)

**Risk Assessment**:

🔴 **Critical Risks**:

- [Risk if any, e.g., "High parallel file conflicts - needs sequencing"]

🟡 **Important Risks**:

- [Risk if any, e.g., "Heavy API usage - implementing rate limiting"]
- [Risk if any, e.g., "Estimated cost >$1 - requires approval"]

🟢 **Mitigated Risks**:

- [Risk and mitigation, e.g., "Security scanning via Brakeman after Sequence 2"]

**Quality Gates**: [Rubocop / Brakeman / RSpec / Performance benchmarks]

**Proceed with agentic decomposition?** [Y/n]
```

### Phase 2: Qualifying Questions (If Needed)

Ask questions ONLY when:

- Success criteria unclear ("fast" - how fast? ms? sub-second?)
- Multiple implementation paths ("auth" - OAuth? JWT?)
- Scope ambiguous ("dashboard" - what metrics?)
- Dependencies unknown (existing auth? database?)
- **Conflict risks identified** (which agents might overlap?)
- **Resource concerns** (API limits? cost budget? performance requirements?)
- **Quality requirements** (security level? accessibility? performance SLAs?)

**Question format**:

```markdown
## Clarifying Questions

Before creating the execution plan, I need to clarify:

**Technical**:

1. [Tech stack question]
2. [Version/framework question]

**Scope**: 3. [Boundaries question] 4. [MVP vs full question]

**Success Criteria**: 5. [Verification question] 6. [Performance requirements - e.g., "API response time <200ms?"]

**Risk Mitigation**: 7. [Conflict resolution if flagged - e.g., "Agents 3-5 may touch same controller - sequential or separate files?"] 8. [Resource limits if flagged - e.g., "Estimated cost $2.50 - proceed or reduce scope?"]

**Quality Requirements**: 9. [Security scanning needed? E.g., "Payment handling - require Brakeman scan?"] 10. [Performance benchmarks needed? E.g., "Critical path - target response time?"]

Please answer, or reply "use defaults" to proceed with reasonable assumptions.
```

### Phase 3: Generate Agentic Decomposition

Using REPEATABLE_AGENTIC_DECOMPOSITION_PROCESS.md methodology:

1. **Extract agent tasks** following agent-readiness criteria
2. **Build dependency graph**:
   - Verify acyclic (no circular dependencies)
   - Calculate critical path
   - Identify parallelization opportunities
3. **Identify file/resource conflicts** - flag parallel agents that may touch same files
4. **Plan rollback strategy** - define undo steps for each sequence
5. **Create detailed agent prompts** with:
   - Context (what exists, what's needed)
   - Task (specific objective)
   - Requirements (technical specs, performance targets)
   - Deliverable (files, code, tests)
   - Success Criteria (3-5 objective, **programmatically verifiable** criteria)
   - Test Strategy (RSpec, system tests, performance benchmarks)
   - Rollback Instructions (how to undo if downstream fails)
   - Shared State (data to pass to dependent agents)

6. **Define quality gates** per sequence:
   - Test coverage requirements
   - Linting rules (Rubocop)
   - Security scanning (Brakeman for Rails)
   - Performance benchmarks (where applicable)

7. **Calculate resource estimates**:
   - Tokens per agent (context + generation)
   - Total estimated cost
   - Concurrency limits
   - Rate limiting strategy

8. **Organize into sequences** with checkpoints and rollback plans
9. **Define state tracking file**: `agentic-{feature-slug}-{timestamp}-plan.md`

**Present execution plan**:

```markdown
# Agentic Execution Plan: [Feature Name]

**Plan File**: `agentic-{feature-slug}-{timestamp}-plan.md`
**Branch**: `agentic/{feature-slug}-{timestamp}`

## Summary

- **Goal**: [High-level objective]
- **Total Agents**: [N]
- **Sequences**: [M]
- **Parallel Opportunities**: [P agents concurrent]
- **Max Concurrency**: [C agents at once]
- **Estimated Time**: [X hours]
- **Estimated Cost**: $[low]-$[high]
- **Checkpoints**: [C git commits for state recovery]
- **Rollback Points**: [R sequences with undo capability]

## Resource Management

**Token Budget**:

- Estimated total: ~[X]k tokens
- Per agent average: ~[Y]k tokens
- Cost estimate: $[low]-$[high] at current rates

**Concurrency Limits**:

- Max parallel agents: [C] (to prevent rate limiting)
- Sequence 2: [P] parallel agents
- Sequence 3: [Q] parallel agents

**Rate Limiting**:

- Inter-agent delay: [N] seconds (if needed)
- Batch size: [B] agents per batch (if high concurrency)

## Dependency Graph (Acyclic Verified ✅)
```

Agent 1 (Foundation) [Critical Path]
↓
Agent 2 (Models) [Critical Path]
↓
┌────────┴────────┐
Agent 3 Agent 4 (PARALLEL - no conflicts ✅)
└────────┬────────┘
Agent 5 [Critical Path - Performance sensitive]
└─ Benchmark: <200ms response time

````

**Critical Path**: Agents 1 → 2 → 5 (estimated [X] min)
**Parallel Savings**: [Y] min from concurrent Agents 3-4

## Agent Breakdown

### SEQUENCE 1: [Phase Name] (Sequential) - Foundation

**Checkpoint**: After completion, commit "Agentic: Sequence 1 - [Phase Name]"
**Rollback**: `git revert HEAD` + `rails db:rollback STEP=2`
**Quality Gates**: RSpec models, Rubocop
**Estimated Cost**: $[X]-$[Y]

#### Agent 1: [Task Name - e.g., Database Schema]

- **Creates**:
  - `db/migrate/TIMESTAMP_create_households.rb`
  - `db/migrate/TIMESTAMP_create_tasks.rb`
- **Modifies**: `db/schema.rb`
- **Tests**:
  - Write: `spec/migrations/create_households_spec.rb`
  - Verify: `bundle exec rspec spec/migrations`
- **Depends on**: None
- **Provides to downstream**: Schema structure for Agent 2
- **Success Criteria** (Programmatic):
  - `bundle exec rails db:migrate` exits 0
  - `bundle exec rails db:rollback && rails db:migrate` succeeds (reversible)
  - `bundle exec rspec spec/migrations` passes (5 examples expected)
  - Schema includes tables: households, tasks
- **Performance Criteria**: N/A (not performance-critical)
- **Security Considerations**: None for this agent
- **Rollback Instructions**:
  ```bash
  bundle exec rails db:rollback STEP=2
  git rm db/migrate/TIMESTAMP_create_*.rb
````

- **Time**: 8 minutes
- **Estimated Tokens**: ~3k
- **Conflict Risk**: None

#### Agent 2: [Task Name - e.g., ActiveRecord Models]

- **Creates**:
  - `app/models/household.rb`
  - `app/models/task.rb`
- **Tests**:
  - Write: `spec/models/household_spec.rb` (>80% coverage)
  - Write: `spec/models/task_spec.rb` (>80% coverage)
- **Depends on**: Agent 1 (requires schema)
- **Provides to downstream**: Model interfaces for Agents 3-4
- **Success Criteria** (Programmatic):
  - `bundle exec rspec spec/models/household_spec.rb` passes (12+ examples)
  - `bundle exec rspec spec/models/task_spec.rb` passes (10+ examples)
  - `bundle exec rubocop app/models/household.rb app/models/task.rb` 0 offenses
  - Models validate required fields (test coverage confirms)
  - Associations working (household.tasks returns ActiveRecord::Relation)
- **Performance Criteria**: N/A
- **Security Considerations**: Ensure no mass assignment vulnerabilities
- **Rollback Instructions**:
  ```bash
  git rm app/models/household.rb app/models/task.rb
  git rm spec/models/household_spec.rb spec/models/task_spec.rb
  ```
- **Time**: 12 minutes
- **Estimated Tokens**: ~4k
- **Conflict Risk**: None

---

### SEQUENCE 2: [Phase Name] (Parallel) - Services Layer

**Checkpoint**: After completion, commit "Agentic: Sequence 2 - [Phase Name]"
**Rollback**: `git revert HEAD` + remove service files
**Quality Gates**: RSpec services (>90% coverage), Rubocop, Brakeman (if security-sensitive)
**Estimated Cost**: $[X]-$[Y]

#### Agent 3: [Task Name] (PARALLEL)

- **Creates**: `app/services/weekly_schedule_generator.rb`
- **Tests**: `spec/services/weekly_schedule_generator_spec.rb`
- **Depends on**: Agent 2 (uses Household, Task models)
- **Provides to downstream**: ScheduleGenerator interface for Agent 5
- **Success Criteria** (Programmatic):
  - `bundle exec rspec spec/services/weekly_schedule_generator_spec.rb` passes (15+ examples)
  - `bundle exec rubocop app/services/weekly_schedule_generator.rb` 0 offenses
  - Coverage: >90% (check via SimpleCov)
  - Generates valid schedule structure (hash with required keys)
- **Performance Criteria**:
  - Generates schedule for 100 tasks in <100ms
  - `Benchmark.measure { WeeklyScheduleGenerator.new(...).generate }` < 0.1s
- **Rollback Instructions**:
  ```bash
  git rm app/services/weekly_schedule_generator.rb
  git rm spec/services/weekly_schedule_generator_spec.rb
  ```
- **Time**: 15 minutes
- **Estimated Tokens**: ~5k
- **Conflict Risk**: ✅ No overlap with Agent 4 (different files)

#### Agent 4: [Task Name] (PARALLEL)

- **Creates**: `app/services/notification_service.rb`
- **Tests**: `spec/services/notification_service_spec.rb`
- **Depends on**: Agent 2 (uses models)
- **Provides to downstream**: Notification capability for Agent 6
- **Success Criteria** (Programmatic):
  - `bundle exec rspec spec/services/notification_service_spec.rb` passes (10+ examples)
  - `bundle exec rubocop app/services/notification_service.rb` 0 offenses
  - Integration test: Sends email via ActionMailer (test mode)
- **Performance Criteria**: N/A (async via background job)
- **Rollback Instructions**:
  ```bash
  git rm app/services/notification_service.rb
  git rm spec/services/notification_service_spec.rb
  ```
- **Time**: 15 minutes (parallel with Agent 3)
- **Estimated Tokens**: ~4k
- **Conflict Risk**: ✅ No overlap with Agent 3 (different files)

**Sequence 2 Parallelization**: Agents 3-4 run concurrently (15 min total vs 30 min sequential)

---

### SEQUENCE 3: [Phase Name] (Sequential) - Integration & Security

**Checkpoint**: After completion, commit "Agentic: Sequence 3 - [Phase Name]"
**Rollback**: `git revert HEAD` + remove controllers/routes
**Quality Gates**: RSpec system tests, Rubocop, **Brakeman security scan**
**Estimated Cost**: $[X]-$[Y]

#### Agent 5: [Task Name - e.g., API Controller] (CRITICAL PATH)

- **Creates**:
  - `app/controllers/api/households_controller.rb`
  - `config/routes.rb` (modify)
- **Tests**:
  - `spec/requests/api/households_spec.rb` (API contract tests)
  - `spec/system/household_workflow_spec.rb` (end-to-end)
- **Depends on**: Agents 3-4 (uses services)
- **Provides to downstream**: Public API endpoints
- **Success Criteria** (Programmatic):
  - `bundle exec rspec spec/requests/api/households_spec.rb` passes (20+ examples)
  - `bundle exec rspec spec/system/household_workflow_spec.rb` passes
  - `curl -X GET http://localhost:3000/api/households` returns 200
  - JSON response validates against schema
  - All CRUD operations functional
- **Performance Criteria** (CRITICAL):
  - GET /api/households response time <200ms (50 records)
  - `Benchmark.measure { get '/api/households' }` < 0.2s
  - N+1 query check: <5 queries per request
- **Security Considerations** (CRITICAL):
  - **Brakeman scan required**: 0 high/medium severity issues
  - Authentication required on all endpoints
  - Authorization checks present (household ownership)
  - No SQL injection vectors (use parameterized queries)
- **Rollback Instructions**:
  ```bash
  git checkout HEAD~1 -- config/routes.rb
  git rm app/controllers/api/households_controller.rb
  git rm spec/requests/api/households_spec.rb
  ```
- **Time**: 20 minutes
- **Estimated Tokens**: ~6k
- **Conflict Risk**: None

---

## Quality Gates by Sequence

### Sequence 1 Gates:

```bash
# Must pass before proceeding to Sequence 2
bundle exec rspec spec/models spec/migrations
bundle exec rubocop app/models
# Exit code 0 required
```

### Sequence 2 Gates:

```bash
# Must pass before proceeding to Sequence 3
bundle exec rspec spec/services --format documentation
bundle exec rubocop app/services
# Coverage check
bundle exec rspec spec/services --require spec_helper --format html --out coverage/index.html
# Verify >90% coverage in coverage/index.html
```

### Sequence 3 Gates (SECURITY):

```bash
# Must pass before completion
bundle exec rspec spec/requests spec/system
bundle exec rubocop app/controllers

# SECURITY SCAN (blocking)
bundle exec brakeman -z -q
# Must return 0 high or medium severity issues

# PERFORMANCE VALIDATION
bundle exec rspec spec/performance --tag performance
# Benchmarks must meet targets (<200ms)
```

## Rollback Strategy

Each sequence has defined rollback steps in case downstream sequences fail:

**Scenario**: Sequence 3 Agent 5 fails security scan

1. Automated rollback: `git revert HEAD` (undo Sequence 3 commit)
2. Preserve: Sequences 1-2 remain (validated work)
3. Options presented:
   - [R]efine Agent 5 prompt with security requirements
   - [S]plit Agent 5 into security review + implementation
   - [M]anual intervention to fix issues
4. Replay from Sequence 3 after fixes

**Scenario**: Sequence 2 performance test fails

1. Keep code, mark sequence as failed
2. Options:
   - [O]ptimize: Create new Agent 4b to optimize Agent 4
   - [R]eplan: Split optimization into separate sequence
   - [A]ccept: Proceed with warning if non-critical

## Agent Communication Protocol

Agents can share intermediate learnings via state tracking file:

**Agent 2 discovers**:

- "Household model requires timezone for scheduling"
- Logged to state file under "Shared Discoveries"
- Agent 3 prompt updated to include timezone handling

**Format in state file**:

```markdown
## Shared Agent Discoveries

**Agent 2** (2025-10-03 14:48):

- Finding: Household requires timezone attribute for schedule generation
- Impact: Agents 3, 5
- Action: Added `timezone:string` to migration
- Verification: `rails console` → `Household.new.respond_to?(:timezone)` → true
```

## Validation Strategy

### Automated Validations (99% of criteria):

- RSpec test suites with >80% coverage requirement
- Rubocop linting (0 offenses)
- Brakeman security scanning (0 high/medium issues)
- Performance benchmarks (specific targets)
- Integration tests (curl, rails runner)

### Manual Validations (1% of criteria, critical only):

- Security architecture review (if handling PII/payments)
- UX review for critical user flows
- Accessibility audit (if public-facing)

**Manual validation format**:

```markdown
⏸️ MANUAL CHECKPOINT: Security Review Required

**Sequence**: 3
**Trigger**: Payment processing code detected
**Reviewer**: Human approval needed
**Criteria**:

- [ ] PCI compliance patterns followed
- [ ] No plaintext card data in logs
- [ ] Stripe integration uses idempotency keys

Please review code and confirm: [approved/needs-changes]
```

## Cost Tracking & Display

Display cost tracking in progress updates:

```markdown
═══════════════════════════════════════════════════════
🤖 AGENTIC EXECUTION: [Feature Name]
═══════════════════════════════════════════════════════

📊 Progress: Sequence 2 of 4 (50% complete)
📝 State: agentic-{slug}-{timestamp}-plan.md
🌿 Branch: agentic/{slug}-{timestamp}
💾 Last Checkpoint: abc1234 (Sequence 1 complete)
💰 Cost: $0.42 actual / $0.85 estimated (49% of budget)

✅ SEQUENCE 1: Foundation (Complete - 15 min, $0.18)
✅ Agent 1: Database schema
└─ Tokens: 3.2k, Cost: $0.08
✅ Agent 2: ActiveRecord models
└─ Tokens: 4.1k, Cost: $0.10
└─ Checkpoint: git commit abc1234

🔄 SEQUENCE 2: Services (Running - 8/20 min, $0.24 actual)
✅ Agent 3: Schedule generator (PARALLEL)
└─ Tokens: 5.3k, Cost: $0.13, Time: 15min
🔄 Agent 4: Notification service (PARALLEL - in progress...)
└─ Estimated: 4k tokens, $0.11, 7min remaining

⏳ SEQUENCE 3: Integration (Pending, est. $0.20)
⏳ SEQUENCE 4: Polish (Pending, est. $0.15)

⏱️ Elapsed: 23 min | Remaining: ~37 min
💰 Budget: $0.42 / $1.50 (28% used)
🚀 Speedup: 2.8× vs sequential
═══════════════════════════════════════════════════════
```

## Error Recovery Strategies

Advanced recovery beyond simple retry:

### Strategy 1: Refined Retry

- First failure: Refine prompt with error details
- Add missing context, clarify requirements
- One automatic retry

### Strategy 2: Agent Decomposition

- Complex agent fails: Split into smaller agents
- Example: Agent 5 → Agent 5a (setup) + Agent 5b (implementation)
- User approves decomposition

### Strategy 3: Partial Rollback

- Downstream failure: Revert specific sequence
- Preserve validated prior work
- Replay from rollback point

### Strategy 4: Alternative Approach

- Technical approach fails: Suggest alternative
- Example: "Direct PDF generation failed, propose HTML→PDF conversion"
- Present trade-offs, user chooses

### Strategy 5: Human-in-the-Loop

- Automated recovery not viable
- Pause execution, present diagnostic
- User provides guidance or manual fix
- Resume from fixed state

**Error handling example**:

```markdown
❌ Agent 5: API Controller - Performance Test FAILED

Programmatic verification results:
✅ 1. RSpec tests pass (20/20)
✅ 2. Security scan clean (0 issues)
❌ 3. Performance benchmark failed

Performance Results:
Expected: GET /api/households <200ms
Actual: 847ms (4.2× slower than target)

Root Cause Analysis:

- N+1 query detected: 50 households → 150 queries
- Missing eager loading: `households.includes(:tasks)`

Recovery Options:

1. [R]efine agent - Add optimization prompt with N+1 fix
   Estimated: 5 min, auto-retry

2. [D]ecompose - Split into:
   - Agent 5: Basic controller (keep)
   - Agent 5b: Performance optimization (new)
     Estimated: 10 min, better separation

3. [A]lternative - Implement caching layer
   Trade-off: Adds complexity, better for high traffic
   Estimated: 15 min

4. [P]artial rollback - Revert Agent 5, redesign approach
   Fresh start with performance-first design

5. [M]anual - Human intervention needed

Choose: [R/D/A/P/M]
```

## State Tracking File Format (Enhanced)

```markdown
# Agentic Execution: [Feature Name]

**Started**: 2025-10-03 14:23:00
**Branch**: agentic/feature-name-20251003
**Status**: In Progress / Complete / Interrupted / Rolled Back
**Plan File**: This file

## Resource Tracking

**Cost Budget**: $1.50
**Actual Cost**: $0.42 (28% used)
**Token Usage**: 18.2k / 65k estimated
**Time Budget**: 60 min
**Actual Time**: 23 min (38% used)

## Execution Summary

- **Total Agents**: 11 planned
- **Completed**: 7
- **In Progress**: Agent 8
- **Pending**: Agents 9-11
- **Replanning Events**: 1
- **Rollback Events**: 0

## Progress Detail

### SEQUENCE 1: Foundation - ✅ Complete (18 min, $0.18)

**Commit**: abc1234 - "Agentic: Sequence 1 - Foundation"
**Quality Gates**: ✅ All passed

- [x] Agent 1: Database schema - ✅ Complete (8 min, $0.08, 3.2k tokens)
  - Tests: `bundle exec rspec spec/migrations` - 5/5 passed
  - Rollback test: ✅ Reversible migration confirmed
  - Verified: 2025-10-03 14:35:00

- [x] Agent 2: ActiveRecord models - ✅ Complete (10 min, $0.10, 4.1k tokens)
  - Tests: `bundle exec rspec spec/models` - 22/22 passed
  - Rubocop: ✅ 0 offenses
  - Coverage: 92%
  - Verified: 2025-10-03 14:48:00
  - **Discovery**: Added timezone attribute (see Shared Discoveries)

### SEQUENCE 2: Services - 🔄 In Progress (8/20 min, $0.24/$0.43)

**Target Commit**: "Agentic: Sequence 2 - Services"
**Quality Gates**: Pending

- [x] Agent 3: Schedule generator (PARALLEL) - ✅ Complete (15 min, $0.13, 5.3k tokens)
  - Tests: `bundle exec rspec spec/services/weekly_*` - 15/15 passed
  - Performance: ✅ <100ms for 100 tasks (actual: 67ms)
  - Verified: 2025-10-03 15:12:00

- [ ] Agent 4: Notification service (PARALLEL) - 🔄 In Progress
  - Started: 2025-10-03 15:12:00
  - Estimated: 4k tokens, $0.11

[... continue for all sequences ...]

## Quality Gate Results

### Sequence 1 Gates: ✅ PASSED
```

$ bundle exec rspec spec/models spec/migrations
22 examples, 0 failures

$ bundle exec rubocop app/models
0 offenses detected

```

### Sequence 2 Gates: ⏳ Pending
Expected:
- RSpec services >90% coverage
- Rubocop clean
- Performance benchmarks met

[... continue ...]

## Shared Agent Discoveries

**Agent 2** (2025-10-03 14:48):
- **Finding**: Household requires timezone attribute for schedule generation
- **Impact**: Agents 3, 5 need timezone-aware logic
- **Action**: Added `timezone:string` to migration, default 'UTC'
- **Verification**: `Household.column_names.include?('timezone')` → true
- **Downstream Updates**: Agent 3 prompt updated with timezone handling

## Adaptive Replanning Log

**Event 1** - 2025-10-03 15:12:00
- **Trigger**: Agent 5 discovered font dependency
- **Type**: Agent decomposition
- **Change**: Split Agent 5 into:
  - Agent 5a: Font configuration setup
  - Agent 5b: PDF generation (depends on 5a)
- **Approved**: Yes (user confirmed)
- **Impact**: +1 agent, +5 min estimate, +$0.08 cost
- **Updated Dependency Graph**:
```

Agent 4
↓
Agent 5a (fonts)
↓
Agent 5b (PDF)

```

## Rollback Events

[None yet - would log any sequence rollbacks here]

## Performance Benchmarks

**Agent 3: ScheduleGenerator**
- Target: <100ms for 100 tasks
- Actual: 67ms ✅
- Headroom: 33% under target

**Agent 5: API Controller** (pending)
- Target: <200ms GET /api/households (50 records)
- Actual: [will measure]

## Security Scan Results

**Brakeman** (Sequence 3 gate):
- Status: Pending
- Expected: 0 high/medium severity issues

## Next Steps

**Current State**: Sequence 2 in progress, Agent 4 running

**If Interrupted**:
1. `git checkout agentic/feature-name-20251003`
2. Review this file - last checkpoint at Sequence 1 (commit abc1234)
3. Agent 3 complete, Agent 4 in progress
4. Resume: Re-run Agent 4 (idempotent, safe to retry)
5. Continue with Sequence 2 quality gates

**On Completion**:
1. Run final quality gates
2. Merge checklist review
3. Create PR or merge to main
```

## Reference Documents

- See REPEATABLE_AGENTIC_DECOMPOSITION_PROCESS.md for decomposition algorithm
- See AGENTIC_IMPLEMENTATION_PROMPT.md for agent prompt templates
- See project CLAUDE.md for tech stack, patterns, and quality standards

## Important Rules

1. **Agent Prompts Must**:
   - Include full context (files, structure, patterns)
   - State specific task clearly
   - List all requirements including performance/security
   - Define expected deliverable
   - **Require test coverage** (RSpec, >80% minimum)
   - Provide 3-5 objective, **programmatically verifiable** success criteria
   - Include performance benchmarks if performance-critical
   - Define rollback instructions
   - Specify shared state for downstream agents
   - Estimate token usage

2. **Success Criteria Must**:
   - Be objective and **programmatically** verifiable (99% automated)
   - Use specific test commands (RSpec, rails runner, curl, benchmark)
   - Never use subjective terms ("looks good", "works well")
   - Test actual functionality with assertions
   - Include performance benchmarks where relevant
   - Manual verification <1% (critical security/UX only)

3. **Dependency Management**:
   - Build acyclic dependency graph (no cycles)
   - Verify graph is enforceable
   - Calculate critical path
   - Identify parallelization opportunities
   - Check for file/resource conflicts
   - Plan agent communication for shared discoveries

4. **Parallelization**:
   - Only parallelize truly independent agents
   - Check for file/resource conflicts during planning
   - Flag conflicts for user clarification
   - Enforce concurrency limits (prevent rate limiting)
   - Use single message with multiple Task calls for parallel launch
   - Monitor for race conditions

5. **Resource Management**:
   - Estimate token usage per agent
   - Calculate total cost range
   - Flag if cost exceeds threshold
   - Set concurrency limits to prevent rate limiting
   - Track actual vs estimated costs
   - Display cost in progress updates

6. **Quality Gates**:
   - Define per-sequence quality gates
   - Automate: RSpec, Rubocop, Brakeman, benchmarks
   - Block progression on gate failures
   - Manual gates <1% (critical only)
   - Document required coverage levels

7. **State Management**:
   - Create state tracking markdown file at start
   - Update after each agent completion
   - Git commit after each sequence (checkpoint)
   - Log all discoveries, replanning, rollbacks
   - State file enables resumption if interrupted
   - Include cost/time/token tracking

8. **Rollback Strategy**:
   - Define rollback steps per sequence
   - Test rollback viability during planning
   - Preserve validated prior work
   - Offer rollback on downstream failures
   - Document rollback events in state file

9. **Error Recovery**:
   - Refined retry (first attempt)
   - Agent decomposition (complexity)
   - Partial rollback (downstream failure)
   - Alternative approach (technical blocker)
   - Human-in-the-loop (unrecoverable)
   - Never silently skip failures
   - Always verify success criteria programmatically

10. **Agent Communication**:
    - Log discoveries in state tracking file
    - Update downstream agent prompts with learnings
    - Share intermediate state explicitly
    - Document shared discoveries with timestamps
    - Verify downstream agents received updates

11. **Performance Validation**:
    - Include benchmarks for performance-critical paths
    - Set specific targets (ms, throughput)
    - Verify with Benchmark.measure or equivalent
    - Check for N+1 queries, memory leaks
    - Document performance criteria in success criteria

12. **Security Validation**:
    - Run Brakeman for Rails security scanning
    - Check for SQL injection, XSS, CSRF
    - Validate authentication/authorization
    - Flag PII/payment handling for review
    - Block on high/medium severity issues

## Phase 4-7: Execution & Completion

[Same as v2, enhanced with]:

- Cost tracking in progress displays
- Performance benchmark verification
- Security scan results
- Rollback event logging
- Agent communication tracking
- Advanced error recovery strategies
- Resource usage monitoring

## Key Improvements in v3 (Production Grade)

1. ✅ **Resource Management**: Token/cost estimation, tracking, budgets, concurrency limits
2. ✅ **Rollback Mechanisms**: Per-sequence rollback plans, partial rollback on downstream failures
3. ✅ **Quality Gates**: Automated linting (Rubocop), security (Brakeman), performance benchmarks
4. ✅ **Cost Tracking**: Estimate, track actual vs budget, display in progress, flag overruns
5. ✅ **Agent Communication**: Shared discoveries logged, downstream prompts updated
6. ✅ **Performance Validation**: Benchmarks for critical paths, N+1 detection, specific targets
7. ✅ **Formal Dependencies**: Acyclic graph verification, critical path calculation
8. ✅ **Advanced Recovery**: 5 strategies (retry, decompose, rollback, alternative, human)
9. ✅ **Security Integration**: Brakeman scans, PCI patterns, auth/authz validation
10. ✅ **Enhanced State Tracking**: Cost, performance, discoveries, rollbacks in state file

---

**Now begin Phase 1: Analyze the user's request and provide initial assessment.**
