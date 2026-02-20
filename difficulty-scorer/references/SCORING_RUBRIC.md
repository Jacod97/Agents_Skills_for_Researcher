# Difficulty Scoring Rubric

## 1. Score Calculation Guide

A score from 0 to 100 is calculated by comprehensively considering the three factors below.
Each factor is not individually scored and displayed in a table.
They are used only as internal judgment criteria.

### Skill Gap (Greatest Weight)

Compare possession vs. lack of core skills.

**Gap Judgment Criteria:**

| Status | Meaning | Difficulty Impact |
|--------|---------|-------------------|
| Possesses at or above required level | Strength | Lowers |
| 1-level gap | Minor learning needed | Slightly raises |
| 2-level gap | Significant learning needed | Considerably raises |
| 3+ level gap | Must learn from basics | Greatly raises |
| Entirely lacking all core skills | The entire area is completely new | Very greatly raises |

**Core Skills vs. Supporting Skills:**
- Gaps in core skills (research is impossible without them) have a major impact on difficulty
- Gaps in supporting skills (alternatives available) have a minor impact

### Research Complexity (Intrinsic Difficulty of the Research Itself)

| Level | Characteristics |
|-------|-----------------|
| Low | Using existing tools/models as-is, simple analysis |
| Medium | Fine-tuning existing models, medium-scale data, integrating multiple tools |
| High | Custom model design, large-scale experiments, multimodal processing |
| Very High | Novel architectures, distributed training, optimization research |

### Environmental Factors

- **Tool Integration**: Complexity of connecting required tools/services
- **Infrastructure**: Difficulty of setting up GPU, cloud, or specialized environments
- **Project Scale**: Expected duration, code volume, number of experiments

---

## 2. Key Messages by Grade

| Grade | Score | Tone to Convey to the User |
|-------|-------|---------------------------|
| 🟢 Easy | 0~20 | "Go ahead and start right away! Your current capabilities are more than sufficient." |
| 🟢 Slightly Easy | 21~40 | "Do some light studying, then get started." |
| 🟡 Moderate | 41~60 | "Learn the core skills first and take a step-by-step approach." |
| 🟠 Difficult | 61~80 | "It's challenging, but achievable with step-by-step learning and mentor support." |
| 🔴 Very Difficult | 81~100 | "We recommend narrowing the research scope or forming a team." |

---

## 3. Learning Recommendation Priorities

| Priority | Meaning | Criteria |
|----------|---------|----------|
| 🔴 Required Prerequisite | Must learn before starting research | Core skill with a large gap |
| 🟡 Parallel Learning | Can learn alongside the research | Important but not immediately needed, or the gap is small |
| 🟢 Lower Priority | Can learn when needed | Supporting skill, or alternatives exist |

**Principles for Writing Learning Recommendations:**
- Specify the **concrete purpose within this research** for each item
- Provide a **realistic estimated learning duration**
- Where possible, recommend **specific learning resources** (official tutorials, particular courses, etc.)
- 3 to 5 items is ideal (too many becomes overwhelming)
