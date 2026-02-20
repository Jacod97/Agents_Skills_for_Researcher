# Query Templates by Information Axis

## How to Use

When each information axis is in ❌ Missing or 🟡 Partial status, refer to the templates below to construct an AskUserQuestion.
Adjust options to fit the situation, but maintain the basic structure.

---

## 1. Problem Definition

### ❌ Missing — When nothing has been identified

```
Question: "What specific problem are you trying to solve or explore in this research?"
Options:
  - "I want to improve the performance/accuracy of existing methods"
  - "I want to propose a new methodology or model"
  - "I want to apply existing techniques to a specific domain"
  - "I want to discover new insights through data analysis"
```

### 🟡 Partial — When there is a direction but it is vague

```
Question: "Within [the direction the user mentioned], what specific aspect are you focusing on?"
Options:
  - "[Specific option A — based on user context]"
  - "[Specific option B — based on user context]"
  - "[Specific option C — based on user context]"
```

---

## 2. Research Goal

### ❌ Missing

```
Question: "What is the primary purpose of this research?"
Options:
  - "Degree thesis (Master's/PhD)"
  - "Academic paper (conference/journal submission)"
  - "Personal learning and portfolio"
  - "Practical/workplace application"
```

### 🟡 Partial

```
Question: "How do you plan to ultimately use the research results?"
Options:
  - "Publish as a paper (I have a specific conference/journal in mind)"
  - "Build a prototype and validate it"
  - "A proof-of-concept (PoC) level is sufficient"
  - "I haven't decided specifically yet"
```

---

## 3. Data

### ❌ Missing

```
Question: "How do you plan to obtain the data for your research?"
Options:
  - "Use public datasets (Kaggle, HuggingFace, UCI, etc.)"
  - "Collect it myself (web crawling, APIs, surveys, etc.)"
  - "Provided by my institution/lab"
  - "I haven't decided yet / I'm not sure"
```

### 🟡 Partial — Source is known but scale/format is unclear

```
Question: "What is the approximate scale and format of the data you plan to use?"
Options:
  - "Small scale (hundreds to thousands of records, a few MB)"
  - "Medium scale (tens of thousands of records, hundreds of MB to a few GB)"
  - "Large scale (hundreds of thousands of records or more, tens of GB+)"
  - "I haven't determined this yet"
```

---

## 4. Core Methods

### ❌ Missing

```
Question: "What core technology or methodology will you use in your research?"
Options:
  - "Statistical analysis / data mining"
  - "Machine learning (classification, regression, clustering, etc.)"
  - "Deep learning (CNN, RNN, Transformer, etc.)"
  - "LLM utilization (prompting, RAG, fine-tuning, etc.)"
```

### 🟡 Partial — Method was mentioned but lacks specificity

```
Question: "Could you elaborate on [the method the user mentioned]? What level of implementation are you considering?"
Options:
  - "Use existing models/libraries as-is"
  - "Fine-tune existing models on my data"
  - "Modify/extend existing architectures"
  - "Design a new model/algorithm from scratch"
```

---

## 5. Deliverables

### ❌ Missing

```
Question: "What form of final output would you like to produce?"
Options:
  - "Analysis report / paper (results + visualizations)"
  - "Trained model (usable by others)"
  - "Web demo / dashboard (interactive)"
  - "Dataset construction (public or internal use)"
```

---

## 6. Scope

### ❌ Missing

```
Question: "What is the expected duration and team size for this research?"
Options:
  - "1-2 months, working alone"
  - "3-6 months, working alone"
  - "3-6 months, team of 2-3"
  - "6+ months, lab/team project"
```

---

## 7. Constraints

### ❌ Missing

```
Question: "Are there any equipment or budget constraints for your research? (Multiple selections allowed)"
multiSelect: true
Options:
  - "No GPU server (CPU only or free-tier Colab)"
  - "Cannot use paid APIs/services (free only)"
  - "Can only use a specific programming language"
  - "No particular constraints"
```

---

## Compound Question Design Guide

### Combining two axes into a single AskUserQuestion

When two axes are simultaneously ❌ Missing, related axes can be bundled together into a single query.

**Combinations that can be bundled:**
- Problem Definition + Core Methods (what + how)
- Research Goal + Deliverables (why + output)
- Scope + Constraints (how much + limitations)

**Combinations that should not be bundled:**
- Problem Definition + Constraints (too dissimilar)
- Data + Deliverables (low relevance)

### Example: Problem Definition + Core Methods compound question

```
questions:
  - question: "What is the core problem you are trying to solve in this research?"
    Options: [...]
  - question: "What technology/methodology do you plan to primarily use?"
    Options: [...]
```

---

## Handling "I'm not sure" Responses

When the user selects "I'm not sure" / "I haven't decided yet":

1. **Fill in the axis with an estimate** (based on the research topic and context)
2. **Clearly mark it as an estimate** (indicate *(estimated)* in Phase 3 output)
3. **Do not ask additional questions** (repeatedly asking about unknowns causes stress)
4. **Handle that part flexibly in subsequent analysis** (present multiple scenarios)
