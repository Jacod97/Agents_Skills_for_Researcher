# Skills for Researcher

A collection of AI coding agent skills for researchers.
Provides integrated support from **information gathering → technical feasibility analysis → difficulty assessment → skill learning recommendations → collaborative architecture design** for research ideas.

> Compatible with AI coding tools that support agent skills, such as Claude Code, Gemini CLI, Cursor, Codex, and more.

---

## At a Glance

```
User: "Is this research topic feasible with current technology?"
          │
          ▼
   ┌─────────────────┐
   │ research-advisor │  ← Orchestrator: controls overall flow
   └────────┬────────┘
            │
            ▼
   ┌─────────────────┐
   │ research-intake  │  ← Information sufficiency check + plan-mode queries
   └────────┬────────┘
            │
            ├─ Sufficient info → finalize structured result
            └─ Insufficient info → iterative queries (up to 3 rounds) → finalize structured result
            │
            ▼
   ┌──────────────────┐
   │ feasibility-check│  ← Sub-agent: verifies if implementable with existing technology
   └────────┬─────────┘
            │
   Feasible │          Not feasible → explain reasons + suggest alternatives → end
            ▼
   ┌────────────────────────────┐
   │      Parallel execution    │
   │                            │
   │  skill-profiler            │  ← Domain core concept-centered skill profiling queries
   │  stack-analyzer            │  ← Sub-agent: required tech stack analysis
   │                            │
   └────────────┬───────────────┘
                │
                ▼
   ┌──────────────────┐
   │ difficulty-scorer │  ← Current skills vs. required skills → difficulty 0~100
   └────────┬─────────┘     + strengths/gaps analysis + learning recommendations
            │
            ▼
   ┌──────────────────────┐
   │ architecture-designer │  ← Collaborative architecture design through conversation
   └──────────────────────┘
```

---

## Skill Overview

### 7 Skills / 2 Sub-agents / 6 Reference Documents

| Skill | Role | Type |
|-------|------|------|
| **research-advisor** | Overall workflow orchestration | Orchestrator |
| **research-intake** | Information sufficiency check + refinement queries | Conversational (main thread) |
| **feasibility-check** | Technical feasibility verification | Sub-agent |
| **skill-profiler** | Domain-centered skill profiling | Conversational (main thread) |
| **stack-analyzer** | Required tech stack identification | Sub-agent |
| **difficulty-scorer** | Difficulty assessment + learning recommendations | Scoring engine |
| **architecture-designer** | C4-lite collaborative architecture design | Conversational (main thread) |

---

## Directory Structure

```
skills_for_researcher/
│
├── research-advisor/                 # Orchestrator
│   └── SKILL.md
│
├── research-intake/                  # Information gathering & refinement
│   ├── SKILL.md
│   └── references/
│       └── INTAKE_TEMPLATES.md       #   Query templates for 7 information axes
│
├── feasibility-check/                # Sub-agent: feasibility verification
│   ├── SKILL.md
│   └── references/
│       └── FEASIBILITY_CRITERIA.md   #   Technology maturity & data availability criteria by domain
│
├── skill-profiler/                   # Conversational: domain-centered skill profiling
│   ├── SKILL.md
│   └── references/
│       └── SKILL_CATEGORIES.md       #   Domain-specific question design guide
│
├── stack-analyzer/                   # Sub-agent: required stack analysis
│   ├── SKILL.md
│   └── references/
│       └── TECH_LANDSCAPE.md         #   Tool reference by research workflow stage
│
├── difficulty-scorer/                # Scoring engine: difficulty assessment
│   ├── SKILL.md
│   └── references/
│       └── SCORING_RUBRIC.md         #   Scoring rubric
│
├── architecture-designer/            # Conversational: collaborative architecture design
│   ├── SKILL.md
│   └── references/
│       └── ARCHITECTURE_PATTERNS.md  #   6 research project architecture patterns
│
└── README.md
```

---

## Installation

Copy the skill folders to the skills/plugin directory of your AI coding tool.
The path varies depending on the tool you use.

```bash
# Example: if the skills directory is ~/.ai-tool/skills/
SKILL_DIR=~/.ai-tool/skills

cp -r research-advisor $SKILL_DIR/
cp -r research-intake $SKILL_DIR/
cp -r feasibility-check $SKILL_DIR/
cp -r skill-profiler $SKILL_DIR/
cp -r stack-analyzer $SKILL_DIR/
cp -r difficulty-scorer $SKILL_DIR/
cp -r architecture-designer $SKILL_DIR/
```

After installation, restart the tool and the skills will be automatically recognized.

---

## Usage

### Running the Full Workflow

```
/research-advisor Research on real-time collision avoidance agents using ESDF from mesh data input
```

Or in natural language:

```
"I want to research real-time 3D reconstruction of indoor spaces using Instant-NGP — is it technically feasible?"
```

`research-advisor` will automatically invoke the remaining 6 skills in sequential/parallel order.

### Using Individual Skills

Some skills can also be used independently:

```
/research-intake I want to do something fun with NeRF
```

```
/feasibility-check Real-time 3D shape generation and reconstruction system using DeepSDF
```

```
/stack-analyzer Real-time SLAM research based on point clouds
```

```
/architecture-designer Voxel-based 3D environment simulation system
```

> `skill-profiler` and `difficulty-scorer` require data from previous steps, so they are primarily invoked automatically through `research-advisor`.

---

## Skill Details

### 1. research-advisor

**Thin orchestrator** — handles only flow control and data passing.

- Does not redefine the detailed procedures, query methods, or output formats of each skill
- Delegates to sub-skills to follow their own SKILL.md specifications as-is
- What the orchestrator handles:
  - **Execution order**: Step 1 → 2 → 3 (parallel) → 4 → 5
  - **Branching decisions**: proceed or terminate based on feasibility results
  - **Data passing**: forwards raw output from previous Steps to the next Step
  - **Final summary**: generates a 1-page summary citing each Step's output

### 2. research-intake

The **first gate** that determines the quality of the entire analysis.

Evaluates the user's idea across 7 information axes:

| # | Information Axis | Description |
|---|------------------|-------------|
| 1 | Problem Definition | What problem are you trying to solve or explore? |
| 2 | Research Purpose | Why are you conducting this research? |
| 3 | Data | What data is needed and can it be obtained? |
| 4 | Core Functions/Methods | What specifically will you implement or analyze? |
| 5 | Deliverables | What is the final output? |
| 6 | Scale/Scope | Project duration and team size |
| 7 | Constraints | Budget, equipment, timeline, and other constraints |

**How it works:**
- Evaluates each axis as ✅ Sufficient / 🟡 Partial / ❌ Insufficient
- If sufficient, passes through without additional queries
- If insufficient, enters **plan mode**: iterative option-based queries on lacking items only (up to 3 rounds)
- "I'm not sure" is a valid response → supplemented with reasonable estimates (marked as estimated)
- Final structured result is confirmed with the user before proceeding

### 3. feasibility-check

Determines whether the research idea is **realizable with existing technology**.

- Investigates latest technology trends and similar research cases via WebSearch
- 3-level verdict: **Feasible** / **Conditionally Feasible** / **Not Feasible**
- All verdicts include supporting evidence
- Suggests alternative directions when deemed not feasible

### 4. skill-profiler

Assesses the researcher's capabilities **centered on core concepts of the research domain**.

- Queries domain-specific core concepts, not general-purpose skills (pandas, Git, etc.)
- Example: NeRF research → "Do you understand volume rendering?", "Have you used COLMAP?"
- Example: ESDF research → "Do you know what SDF is?", "Have you worked with mesh data?"
- 2–3 rounds of domain-tailored queries to assess capabilities

### 5. stack-analyzer

Systematically identifies the **required tech stack** for the research project.

- Breaks down the research workflow into 7 stages (collection → preprocessing → analysis → experiment management → visualization → infrastructure → sharing)
- Suggests essential/recommended tools and alternatives for each stage
- Verifies latest tool trends via WebSearch
- Specifies inter-technology dependencies

### 6. difficulty-scorer

Compares current skills against required skills to produce a **difficulty score from 0 to 100**.

- Provides **narrative descriptions of strengths and gaps**, not just table listings
- Recommends learning items by priority (🔴 Essential / 🟡 Concurrent / 🟢 Deferred)

**Difficulty levels:**

| Score | Level |
|-------|-------|
| 0–20 | 🟢 Easy — ready to start immediately |
| 21–40 | 🟢 Slightly Easy — start after minor study |
| 41–60 | 🟡 Moderate — prior study of core skills recommended |
| 61–80 | 🟠 Difficult — mentoring + incremental learning needed |
| 81–100 | 🔴 Very Difficult — consider reducing scope or forming a team |

### 7. architecture-designer

Designs the research system architecture **collaboratively through conversation** with the user.

- Phase A: Context gathering (goals, data, deliverables)
- Phase B: System Context diagram (L1) — Mermaid
- Phase C: Container/pipeline diagram (L2) — Mermaid
- Phase D: Project directory structure proposal
- Phase E: Key design decisions (ADR) documentation

Supports 6 architecture patterns: Simple Analysis / Experiment Pipeline / Data Pipeline / Model Serving / Multimodal Integration / LLM-powered

---

## Design Principle: Thin Orchestrator

`research-advisor` follows the **thin orchestrator** pattern.

```
┌─────────────────────────────────────────────────────────┐
│  What research-advisor DOES                             │
│                                                         │
│  ✅ Determine execution order  (Step 1 → 2 → 3 → 4 → 5)│
│  ✅ Make branching decisions   (feasibility → proceed/stop)│
│  ✅ Pass data between steps   (prev Step output → next Step input)│
│  ✅ Coordinate parallel execution (skill-profiler ∥ stack-analyzer)│
│  ✅ Generate final summary    (citing each Step's output)│
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│  What research-advisor DOES NOT do                      │
│                                                         │
│  ❌ Redefine sub-skill analysis procedures              │
│  ❌ Reduce or alter sub-skill output formats            │
│  ❌ Override sub-skill query methods                    │
│  ❌ Re-analyze previous outputs (only cites them)       │
└─────────────────────────────────────────────────────────┘
```

This ensures that each skill's SKILL.md serves as the **Single Source of Truth**,
structurally preventing specification mismatches between the orchestrator and sub-skills.

### Data Flow Contract

Clear data contracts are defined between each Step.
The orchestrator forwards the raw output of the previous Step to the next Step as-is.

```
Step 1 research-intake
  Output: structured_result (7 information axes table)
         │
         ▼
Step 2 feasibility-check
  Input:  structured_result
  Output: feasibility_result (verdict + tech element analysis + similar cases + risks + alternatives)
         │
    ┌────┴────┐
    ▼         ▼
Step 3-A   Step 3-B
skill-     stack-analyzer
profiler   Input:  structured_result + feasibility_result.required_tech_areas
Input:     Output: required_tech_stack (stage-by-stage table + integrated summary + dependencies + resource table)
structured_result
  Output:
  user_skill_profile
    │         │
    └────┬────┘
         ▼
Step 4 difficulty-scorer
  Input:  user_skill_profile + required_tech_stack
  Output: difficulty_result (score + strengths/gaps narrative + learning recommendations)
         │
         ▼
Step 5 architecture-designer
  Input:  structured_result + required_tech_stack.integrated_stack_summary
  Output: architecture_design (L1/L2 diagrams + directory structure + ADR)
```

While `skill-profiler` converses with the user, `stack-analyzer` analyzes the required tech stack in the background, minimizing user wait time.

---

## Customization

### Modifying Information Gathering Query Templates

You can modify the query items and options for each information axis in `research-intake/references/INTAKE_TEMPLATES.md`.

### Changing Scoring Criteria

You can modify the scoring criteria and level-specific messages in `difficulty-scorer/references/SCORING_RUBRIC.md`.

### Adding Domain-Specific Question Guides

To support new research domains:

1. Add domain-specific core concepts and example questions in `skill-profiler/references/SKILL_CATEGORIES.md`
2. Add tool references in `stack-analyzer/references/TECH_LANDSCAPE.md`
3. Add maturity criteria in `feasibility-check/references/FEASIBILITY_CRITERIA.md`

### Adding Architecture Patterns

Add a new pattern section in `architecture-designer/references/ARCHITECTURE_PATTERNS.md`.

---

## Requirements

- An AI coding tool that supports agent skills (Claude Code, Gemini CLI, Cursor, Codex, etc.)
- `feasibility-check` and `stack-analyzer` use WebSearch, so an internet connection is required

---

## License

MIT
