# Research Project Architecture Patterns

## 1. Pattern Classification

### 1.1 Simple Analysis Pattern

Suitable for research with small-scale data and a single analysis technique.

```
Data → Preprocessing → Analysis → Visualization → Report
```

**Suitable cases:**
- Statistical analysis research
- Exploratory data analysis
- Single model experiments

**Configuration:**
- Completed with 1-3 Jupyter Notebooks
- No separate modularization needed
- Data size under 1GB

---

### 1.2 Experiment Pipeline Pattern

Suitable for research that requires systematic management of multiple experiments.

```
Data → Preprocessing → [Experiment Manager] → Model A/B/C → Evaluation → Results Comparison
                              ↕
                     [Experiment Tracking System]
```

**Suitable cases:**
- Model comparison research
- Hyperparameter search
- Reproducible experiments

**Configuration:**
- Modularized code (src/ directory)
- Config file-based experiment management (config.yaml)
- MLflow / W&B integration
- Clear data version control

---

### 1.3 Data Pipeline Pattern

Suitable for research that processes large-scale data in stages.

```
Collection → Cleaning → Transformation → Loading → Analysis → Visualization
    ↓           ↓            ↓              ↓
  [Raw]     [Cleaned]   [Transformed]    [Final]  ← Data saved at each stage
```

**Suitable cases:**
- Large-scale data collection/analysis
- ETL-centric research
- Continuous data updates

**Configuration:**
- Separate scripts per stage
- Intermediate result storage
- Error recovery / restart support
- Scheduler (cron, Airflow)

---

### 1.4 Model Serving Pattern

Suitable for research where the trained model needs to be deployed for external use.

```
[Training Pipeline]
Data → Preprocessing → Training → Evaluation → Model Save
                                                    ↓
[Serving Pipeline]                          [Model Registry]
API Request → Preprocessing → Inference → Postprocessing → Response
```

**Suitable cases:**
- Providing demos/prototypes
- Implementing API-based services
- Sharing models for fellow researchers to use

**Configuration:**
- Separation of training and serving code
- FastAPI / Streamlit / Gradio
- Docker containerization
- Model version control

---

### 1.5 Multimodal Integration Pattern

Research that integrates and processes multiple data types such as text, images, and audio.

```
Text Collection ──→ Text Preprocessing ──┐
                                          ├─→ Unified Model → Evaluation
Image Collection ──→ Image Preprocessing ─┘
```

**Suitable cases:**
- Multimodal learning research
- Text + image analysis
- Cross-modal retrieval

**Configuration:**
- Preprocessing modules per data type
- Common data format definition
- Unified data loader
- GPU memory management

---

### 1.6 LLM-Powered Research Pattern

Research that utilizes LLMs as a core component.

```
Query/Data → Prompt Construction → LLM API → Postprocessing → Results
                  ↑                                ↓
           [Prompt Templates]              [Evaluation Metrics]
                  ↑
           [Vector DB / RAG]  (if applicable)
```

**Suitable cases:**
- LLM performance benchmarking
- RAG system research
- Prompt engineering research
- LLM agent research

**Configuration:**
- Prompt template management
- API key / cost management
- Response caching (cost savings)
- Evaluation framework

---

## 2. Pattern Selection Guide

```
Does the research involve model training?
├── No → Is the data scale large?
│         ├── No → [Simple Analysis Pattern]
│         └── Yes → [Data Pipeline Pattern]
│
└── Yes → Are you comparing multiple models/experiments?
          ├── No → Will the model be made publicly available?
          │        ├── No → [Simple Analysis Pattern] + training code
          │        └── Yes → [Model Serving Pattern]
          │
          └── Yes → [Experiment Pipeline Pattern]
                     └── Is it multimodal?
                          ├── No → [Experiment Pipeline Pattern]
                          └── Yes → [Multimodal Integration Pattern]

Does it utilize LLM APIs?
└── Yes → [LLM-Powered Research Pattern] (can be combined with other patterns)
```

---

## 3. Diagram Creation Tips

### 3.1 Diagram Principles for Researchers

- **Focus on data flow rather than code structure**: For researchers, "how data flows" is what matters most
- **Specify tool names**: Label each component with the specific tools being used
- **Specify outputs per stage**: Clearly define the inputs and outputs of each stage
- **Distinguish optional elements**: Visually separate required vs. optional components

### 3.2 Color Conventions

| Color | Meaning |
|-------|---------|
| `#438DD5` (Blue) | Internal components |
| `#08427B` (Dark Blue) | User/Researcher |
| `#999999` (Gray) | External systems/services |
| `#2D8659` (Green) | Outputs/Results |
| `#D4A843` (Yellow) | Data stores |
