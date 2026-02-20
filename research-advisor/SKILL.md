---
name: research-advisor
description: >
  When a researcher presents a research idea or topic, this main skill orchestrates the entire flow
  from information sufficiency assessment to technical feasibility analysis, difficulty scoring,
  and architecture design.
  Triggered by requests such as "Is this research feasible?", "Can this idea be realized?",
  "Analyze this research topic", or "Review the feasibility of this project".
user-invocable: true
argument-hint: "[research idea or topic]"
metadata:
  author: skills_for_researcher
  version: "2.0"
  language: en
  role: orchestrator
---

# Research Advisor — Thin Orchestrator

This skill is responsible **only for flow control and data passing**.
The detailed procedures, query methods, and output formats for each step follow the respective skill's own SKILL.md specification.
Do not let the orchestrator redefine sub-skill procedures or reduce their output formats.

---

## Execution Flow

```
Step 1  research-intake         Information gathering & structuring
          |
          v
Step 2  feasibility-check       Feasibility verification (sub-agent)
          |
          +-- Not feasible -> Deliver results to user -> End
          +-- Conditionally feasible -> Explain conditions to user -> Confirm whether to proceed
          |
          v
Step 3  skill-profiler           Assess user's technical capabilities (main thread)
     +  stack-analyzer           Analyze required tech stack (sub-agent, background)
          |
          v
Step 4  difficulty-scorer        Difficulty scoring + learning recommendations
          |
          v
Step 5  architecture-designer    Collaborative architecture design (after user confirmation)
```

---

## Step 1: Information Gathering — research-intake

**Purpose**: Secure sufficient context for subsequent analysis.

**Execution**: Run according to the research-intake skill specification.
- Pass the user's `$ARGUMENTS` as initial input
- Information sufficiency assessment, plan-mode queries when insufficient, and structured result confirmation are all handled by research-intake

**Data Contract**:
- Input: User's original idea (`$ARGUMENTS`)
- Output: `structured_result` — A table with 7 information axes organized (research-intake Phase 3 output format)

**Next Step Condition**: Proceed to Step 2 when the user confirms the structured result ("That's correct").

---

## Step 2: Feasibility Verification — feasibility-check (Sub-Agent)

**Purpose**: Determine whether the idea can be realized with currently existing technology.

**Execution**: Create a sub-agent using the Task tool.

```
Task tool invocation:
  subagent_type: general-purpose
  prompt: |
    You are the feasibility-check skill.
    Please analyze the technical feasibility of the research idea below.
    Follow the analysis procedure (steps 1-3) and output format defined
    in the feasibility-check SKILL.md and return the results as-is.

    === Structured Research Idea ===
    [Insert the entire structured_result from Step 1 here]
```

**Key Rule**: Do not separately specify an output format. Allow the sub-agent to follow the complete structure defined in the "Output Format" section of feasibility-check/SKILL.md on its own (including the technical element analysis table, similar research cases + sources, risk mitigation strategies, and alternatives section).

**Data Contract**:
- Input: `structured_result` (Step 1 output)
- Output: `feasibility_result` — Verdict (✅/⚠️/❌), technical element analysis, similar cases, required skill areas, risks, alternatives

**Branching Logic**:

| Verdict | Orchestrator Action |
|---------|-------------------|
| ❌ Not feasible | Show the `feasibility_result` to the user as-is, highlight the alternatives section, then **end** |
| ⚠️ Conditionally feasible | Show the `feasibility_result` to the user, use AskUserQuestion to confirm whether to proceed. If "proceed", go to Step 3 |
| ✅ Feasible | Show the `feasibility_result` to the user and proceed to Step 3 |

---

## Step 3: Parallel Analysis — skill-profiler + stack-analyzer

**Purpose**: Simultaneously assess the user's existing skills and the project's required skills.

### 3-A: skill-profiler (Main Thread)

**Execution**: Run according to the skill-profiler skill specification.
- Pass `structured_result` to base queries on the core domain concepts of the research topic
- Query about core domain concepts and methodologies of the research, not general-purpose skills (pandas, Git, etc.)

**Data Contract**:
- Input: `structured_result` (Step 1 output — used to design domain-tailored questions)
- Output: `user_skill_profile` — The complete structure defined in skill-profiler's "Output Format" section

### 3-B: stack-analyzer (Sub-Agent, Background)

**Execution**: Create a sub-agent in the background using the Task tool **simultaneously with the start of 3-A**.

```
Task tool invocation:
  subagent_type: general-purpose
  run_in_background: true
  prompt: |
    You are the stack-analyzer skill.
    Please analyze the required tech stack for the research project below.
    Follow the analysis procedure (steps 1-3) and output format defined
    in the stack-analyzer SKILL.md and return the results as-is.

    === Structured Research Idea ===
    [Insert the entire structured_result from Step 1 here]

    === Required Skill Areas from Feasibility Analysis ===
    [Insert the "Required Skill Areas" section from Step 2 feasibility_result here]
```

**Key Rule**: Do not separately specify an output format. Allow the sub-agent to follow the complete structure defined in the "Output Format" section of stack-analyzer/SKILL.md on its own (including step-by-step tables, integrated stack summary, dependency relationships, and computing resource table).

**Joining**: After 3-A (skill-profiler) completes, collect the 3-B results using TaskOutput.

**Data Contract**:
- Input: `structured_result` + required skill areas from `feasibility_result`
- Output: `required_tech_stack` — The complete structure defined in stack-analyzer's "Output Format" section

---

## Step 4: Difficulty Scoring — difficulty-scorer

**Purpose**: Compare existing skills against required skills to produce a quantitative difficulty score and recommend learning paths.

**Execution**: Run according to the difficulty-scorer skill specification.
- The scoring procedure (steps 1-3) and output format are all performed as defined by difficulty-scorer itself

**Data Passing**: Explicitly pass the following two data sets as input to difficulty-scorer.

```
Based on data collected from previous steps, please score the difficulty
and recommend learning paths according to the difficulty-scorer skill specification.

=== User Skill Profile (skill-profiler output) ===
[Insert the entire user_skill_profile from Step 3-A here]

=== Required Tech Stack (stack-analyzer output) ===
[Insert the entire required_tech_stack from Step 3-B here]
```

**Data Contract**:
- Input: `user_skill_profile` (Step 3-A) + `required_tech_stack` (Step 3-B)
- Output: `difficulty_result` — Overall score, strengths/gaps narrative, learning recommendations (narrative format)

**User Delivery**: Show the `difficulty_result` to the user as-is.

---

## Step 5: Architecture Design — architecture-designer

**Purpose**: Design the research system's architecture through dialogue with the user.

**Entry Condition**: Use AskUserQuestion to ask the user whether to proceed with architecture design.
- "Proceed" → Run according to the architecture-designer skill specification
- "Skip" → Move to final summary

**Execution**: Run according to the architecture-designer skill specification.
- The interactive design procedure for Phases A-E is all performed as defined by architecture-designer itself

**Data Passing**: Provide previous step results as context.

```
Please proceed with architecture design according to the architecture-designer
skill specification, referencing the previous analysis results.

=== Structured Research Idea ===
[Summary of structured_result]

=== Confirmed Tech Stack ===
[Integrated stack summary section from required_tech_stack]
```

---

## Final Summary

After all Steps are complete (or if Step 5 was skipped), generate the following summary.
This summary is composed by **quoting** outputs from previous steps (no re-analysis):

```
## Technical Feasibility Analysis — Final Summary

**Research Topic**: [Quote from structured_result]

| Item | Result |
|------|--------|
| Technical Feasibility | [Quote verdict from feasibility_result] |
| Implementation Difficulty | [Quote overall score from difficulty_result] |
| Core Tech Stack | [Quote integrated summary from required_tech_stack] |
| Top Risk | [Quote major risk from feasibility_result] |
| Key Learning Needed | [Quote 🔴 items from difficulty_result] |

**Recommended Next Actions**:
1. [Highest-priority item from difficulty_result's key learning recommendations]
2. [Data acquisition-related action from structured_result]
3. [Next steps from architecture design results, if available]
```

---

## Orchestrator Principles

1. **No redefining sub-procedures**: Do not rewrite each skill's analysis procedures, query methods, or output formats in the orchestrator
2. **No reducing output formats**: Do not request simplified output in sub-agent prompts compared to what the skill specification defines
3. **Data passing only**: When passing output from one Step to the next, pass the original text as-is
4. **Branching logic only**: Handle only flow branching such as feasibility verdicts (✅/⚠️/❌) and user confirmations (proceed/skip)
5. **Quoting only**: In the final summary, quote previous outputs rather than re-analyzing them
