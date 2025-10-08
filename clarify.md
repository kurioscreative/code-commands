---
description: Analyze and improve the clarity of your intent in documents, requirements, or ideas through structured evaluation and targeted clarification.
argument-hint: <question/goal> with @documents or text
allowed-tools:
  - Read
  - Edit
  - Glob
  - Grep
  - TodoWrite
---

# Clarify Intent & Requirements

You are now in **clarify mode**. Your goal is to help the user achieve maximum clarity in their communication, documentation, or planning by identifying ambiguities, gaps, and alignment issues.

## Core Philosophy

Clarity emerges through:
1. **Precision**: Specific, concrete statements over vague generalities
2. **Alignment**: Components support the stated goal consistently
3. **Completeness**: No critical questions left unanswered
4. **Actionability**: Clear next steps for implementation

## Input Analysis

User request: $ARGUMENTS

## Phase 1: Understand the Clarification Goal

First, identify what type of clarity analysis is needed:

### Type A: Alignment Check
**Pattern**: "Does X align with Y?" or "Evaluate if X fits with Y"
**Goal**: Verify consistency between components, documents, or ideas
**Output**: Alignment assessment with specific gaps/conflicts identified

### Type B: Readiness Assessment
**Pattern**: "Is X ready for Y?" or "Think harder to consider if X is ready"
**Goal**: Evaluate if requirements/documentation are sufficient for next phase
**Output**: Readiness score with missing elements and blocking issues

### Type C: Document Refinement
**Pattern**: "Update X to add clarity" or "Improve clarity of X"
**Goal**: Enhance existing documentation to resolve ambiguities
**Output**: Specific refinements with clarifying questions for user

### Type D: Concept Validation
**Pattern**: "Does this make sense?" or "Is this approach clear?"
**Goal**: Validate logical coherence and identify unclear areas
**Output**: Validation with specific unclear points highlighted

## Phase 2: Deep Analysis

Apply rigorous analytical thinking:

### 2.1 First Principles Decomposition

Break down the request into fundamental components:
- What is the **core intent**?
- What are the **stated goals**?
- What are the **implied constraints**?
- What are the **success criteria** (explicit or implicit)?

### 2.2 Clarity Evaluation Framework

For each component, evaluate on 5 dimensions:

**1. Specificity** (1-5 scale)
- 1: Vague, subjective, unmeasurable
- 3: Some specifics but gaps remain
- 5: Concrete, measurable, actionable

**2. Completeness** (1-5 scale)
- 1: Major elements missing
- 3: Core present, details sparse
- 5: All necessary information provided

**3. Consistency** (1-5 scale)
- 1: Contradictory statements
- 3: Mostly aligned, some tensions
- 5: Fully coherent throughout

**4. Actionability** (1-5 scale)
- 1: No clear next steps
- 3: General direction unclear
- 5: Precise implementation path

**5. Unambiguousness** (1-5 scale)
- 1: Multiple valid interpretations
- 3: Some interpretation needed
- 5: Single clear meaning

### 2.3 Question Generation

For any dimension scoring <4, generate clarifying questions using this hierarchy:

**Critical Questions** (blockers - must answer to proceed):
- Ambiguous requirements with multiple valid interpretations
- Missing essential information for implementation
- Contradictions that prevent coherent action

**Important Questions** (significant gaps - should answer for quality):
- Underspecified details that affect design decisions
- Unclear success criteria or acceptance tests
- Implicit assumptions that should be explicit

**Refinement Questions** (nice-to-have - improves clarity):
- Edge cases not addressed
- Performance/quality expectations unstated
- User experience details unspecified

## Phase 3: Structured Output

Present findings in this format:

```markdown
# Clarification Analysis: [Topic/Document Name]

## Executive Summary

**Clarity Score**: [X]/25 (sum of 5 dimensions)
**Readiness**: [Ready / Nearly Ready / Needs Work / Not Ready]
**Blocking Issues**: [N critical questions]

**One-line assessment**: [Direct verdict on alignment/readiness/clarity]

---

## Detailed Evaluation

### Specificity: [X]/5
[Brief assessment with specific examples of vague vs. concrete statements]

**Needs improvement**:
- [Quote vague statement] → Suggest: [More specific alternative]
- [Quote unmeasurable goal] → Suggest: [Measurable version]

**Well-specified**:
- [Quote good example for reinforcement]

### Completeness: [X]/5
[Assessment of what's present vs. missing]

**Missing elements**:
- [Element 1]: [Why it's needed]
- [Element 2]: [Why it's needed]

**Well-covered**:
- [Element that's thorough]

### Consistency: [X]/5
[Assessment of internal coherence]

**Tensions/contradictions**:
- [Statement A] conflicts with [Statement B]
  - Resolution needed: [Clarify which takes precedence]

**Aligned sections**:
- [Example of good consistency]

### Actionability: [X]/5
[Assessment of implementability]

**Unclear paths**:
- [Area lacking implementation guidance]
  - Needs: [What would make it actionable]

**Clear paths**:
- [Example of actionable requirement]

### Unambiguousness: [X]/5
[Assessment of interpretability]

**Ambiguous statements**:
- "[Quote]" could mean:
  - Interpretation A: [...]
  - Interpretation B: [...]
  - **Clarification needed**: [Specific question]

**Clear statements**:
- [Example of unambiguous requirement]

---

## Critical Clarifying Questions

These **must** be answered before proceeding:

1. **[Topic]**: [Specific question]
   - Why critical: [Impact of not answering]
   - Example scenario: [Where ambiguity would cause problems]

2. **[Topic]**: [Specific question]
   - Why critical: [Impact]
   - Example scenario: [Problem case]

[Continue for all critical questions...]

---

## Important Clarifying Questions

These **should** be answered for quality:

1. **[Topic]**: [Question]
   - Impact: [Design/quality implications]
   - Suggested default if skipped: [Reasonable assumption]

[Continue for important questions...]

---

## Refinement Suggestions

Optional improvements for enhanced clarity:

1. **[Area]**: [Suggestion]
   - Benefit: [Why this helps]

[Continue for refinement suggestions...]

---

## Alignment Analysis
[Only for Type A: Alignment Check]

**Component A**: [Name/description]
**Component B**: [Name/description]

### Areas of Strong Alignment ✅
- [Specific alignment point with evidence]
- [Another alignment with quotes/references]

### Areas of Misalignment ⚠️
- [Specific conflict or gap]
  - Component A expects: [X]
  - Component B provides: [Y]
  - **Resolution**: [Suggestion or question]

### Missing Bridges 🔗
- [Element needed to connect A and B]
  - Why needed: [Explanation]
  - Suggestion: [How to bridge]

---

## Readiness Assessment
[Only for Type B: Readiness Assessment]

**Goal**: [What this needs to be ready for]
**Verdict**: [Ready / Nearly Ready / Needs Work / Not Ready]

### Readiness Checklist

- [x] **[Element 1]**: Present and sufficient
- [x] **[Element 2]**: Present and sufficient
- [ ] **[Element 3]**: Missing or insufficient
  - Gap: [What's lacking]
  - Needed: [What would satisfy this]
- [~] **[Element 4]**: Partially addressed
  - Present: [What exists]
  - Missing: [What's needed]

### Blocking Issues (Must resolve)
1. [Issue 1 preventing readiness]
2. [Issue 2 preventing readiness]

### Recommended Before Proceeding
1. [Non-blocking but valuable improvement]
2. [Another recommendation]

---

## Proposed Refinements
[Only for Type C: Document Refinement]

### Section: [Section Name]

**Current**:
```
[Current text/structure]
```

**Refined**:
```
[Improved version with specific changes]
```

**Changes made**:
- [Change 1 and rationale]
- [Change 2 and rationale]

**Open questions**:
- [Question 1 that requires user input]
- [Question 2 requiring decision]

[Repeat for each section needing refinement...]

---

## Recommended Next Steps

Based on this analysis, here's the optimal path forward:

**If Clarity Score ≥20**:
1. [Address N critical questions]
2. [Consider M important questions]
3. Ready to proceed with implementation

**If Clarity Score 15-19**:
1. [Resolve blocking issues first]
2. [Answer critical questions]
3. [One more clarification pass recommended]

**If Clarity Score <15**:
1. [Major gaps to address]
2. [Recommend restructuring approach]
3. [Schedule another clarification session after changes]

---

## Response Template for User

To streamline your response, you can:

**Answer all questions**:
[Provide numbered answers corresponding to questions above]

**OR use shortcuts**:
- "Use reasonable defaults" - I'll apply standard assumptions
- "Implementation decides" - Mark as implementation detail
- "Skip refinements" - Focus only on critical/important questions

**OR selective response**:
Just answer the questions that matter most to you. I'll note the rest as "implementation detail" or "assumed standard practice."
```

## Phase 4: Interactive Refinement

After presenting analysis:

1. **Wait for user response** to clarifying questions
2. **If user provides answers**: Update analysis, show new clarity score
3. **If user asks to refine document**: Apply refinements with their input
4. **If user says "use defaults"**: Document assumptions, proceed with reasonable defaults
5. **Iterate** until clarity score ≥20 or user satisfied

## Key Principles

### Think Harder
When user says "think harder":
- Re-examine assumptions you made
- Question what seemed obvious
- Look for subtle inconsistencies
- Generate deeper, more probing questions
- Consider edge cases and failure modes
- Apply first principles thinking

### Be Specific
Avoid vague assessments:
- ❌ "This section could be clearer"
- ✅ "Line 47 uses 'fast' without defining target latency. Suggest: 'API response <200ms p95'"

### Find Real Ambiguities
Don't create problems where none exist:
- If implementation detail can be decided later, note it but don't block
- Focus on ambiguities that would lead to **different implementations**
- Distinguish between "underspecified" and "genuinely ambiguous"

### Respect User Intent
- If user wants validation, validate honestly (including "not ready" if true)
- If user wants questions, focus on questions, not solutions
- If user wants refinement, propose changes, don't just critique
- Match your response to the type of clarity they're seeking

### Progressive Disclosure
1. Start with executive summary (quick verdict)
2. Provide detailed analysis (for those who want depth)
3. Surface critical questions prominently
4. Make refinements optional to consider

## Examples of Good vs. Bad Clarifying Questions

### Bad (too vague):
❌ "What do you mean by 'smooth path'?"
❌ "Can you clarify the requirements?"
❌ "Is performance important?"

### Good (specific, actionable):
✅ "By 'smooth path', do you mean: (a) CLI commands exist for each algorithm step, (b) documentation guides implementation, or (c) automated scaffolding generates boilerplate?"
✅ "The roadmap mentions 'fast processing' - what's the target throughput? (e.g., 1000 ops/sec, 10k ops/sec, or is this not performance-critical?)"
✅ "Algorithm step 3 requires 'user data' but the CLI design doesn't show data input. Should this be: (a) CLI flag, (b) config file, (c) interactive prompt?"

---

**Now begin Phase 1: Analyze the user's input and identify the clarification goal type (A/B/C/D).**
