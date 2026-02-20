# Domain-Specific Question Design Guide

## How to Use

Given a research topic, design questions targeting **core concepts of the relevant domain** by referring to the patterns below.
Do not use the examples in this document verbatim; adapt them to fit the research topic.

---

## 1. Question Design Patterns

### Pattern A: Concept Understanding

```
"How familiar are you with [core concept]?"
Options:
  - "I've never heard of it"
  - "I understand the concept but have never worked with it directly"
  - "I've read related papers or run code related to it"
  - "I have experience implementing it myself or using it in research"
```

### Pattern B: Methodology Experience

```
"Do you have experience with [methodology/algorithm]?"
Options:
  - "I have no related experience at all"
  - "[Example of beginner-level experience]"
  - "[Example of intermediate-level experience]"
  - "[Example of advanced-level experience]"
```

### Pattern C: Data Type Experience

```
"Do you have experience working with [data type] data?"
Options:
  - "I have never worked with this type of data"
  - "I've done simple exploration/visualization with it"
  - "I have hands-on experience with preprocessing and analysis"
  - "I have experience building large-scale processing pipelines"
```

---

## 2. Core Concepts by Domain (Examples)

The following are reference examples. Identify the core concepts appropriate to the actual research topic.

### Natural Language Processing (NLP)

| Research Type | Core Concepts to Ask About |
|---------------|---------------------------|
| Semantic Search | Embeddings, vector similarity, pretrained models, language-specific preprocessing |
| Text Classification | Classification models (BERT, etc.), fine-tuning, evaluation metrics (F1, etc.) |
| Information Extraction | NER, relation extraction, knowledge graphs |
| Text Generation | LLM, prompt engineering, decoding strategies, evaluation (BLEU, etc.) |

### Computer Vision (CV)

| Research Type | Core Concepts to Ask About |
|---------------|---------------------------|
| Image Classification | CNN architectures, transfer learning, data augmentation |
| Object Detection | Anchor boxes, NMS, mAP, YOLO/RCNN family |
| 3D Vision | Point clouds, meshes, SDF, NeRF |
| Medical Imaging | DICOM, segmentation, data imbalance |

### Reinforcement Learning (RL)

| Research Type | Core Concepts to Ask About |
|---------------|---------------------------|
| Robot Control | State/action spaces, reward design, sim-to-real |
| Game AI | Environment design, policy learning (DQN, PPO), self-play |
| Optimization | MDP modeling, exploration-exploitation tradeoff |

### Data Science

| Research Type | Core Concepts to Ask About |
|---------------|---------------------------|
| Predictive Modeling | Feature engineering, cross-validation, ensemble methods |
| Time Series Analysis | Stationarity, ARIMA/Prophet, sequence models |
| Recommendation Systems | Collaborative filtering, content-based, embeddings |

### Robotics / Simulation

| Research Type | Core Concepts to Ask About |
|---------------|---------------------------|
| Path Planning | SDF/ESDF, sampling-based algorithms (RRT, PRM), optimal control |
| SLAM | Point cloud processing, map representation, loop closure |
| Manipulation | Inverse kinematics, grasp planning, force control |

---

## 3. Proficiency Signal Interpretation

Criteria for estimating capability level from user responses:

| Response Signal | Estimated Level |
|-----------------|-----------------|
| "I've never heard of it", "I don't really know" | No experience |
| "I understand the concept but...", "I know it theoretically but..." | Conceptual understanding |
| "I did it in a class/tutorial", "I followed along with a simple example" | Beginner |
| "I used it directly in an assignment/project" | Elementary |
| "I'm using it in my research", "I use it to solve problems" | Intermediate |
| "I can implement it from scratch", "I can teach it to others" | Advanced |

---

## 4. What NOT to Ask

- **General-purpose programming tools**: pandas, numpy, matplotlib, Git, Docker, Jupyter, etc.
  → These are identified as required skills by stack-analyzer, and gaps are assessed by difficulty-scorer
- **Skills unrelated to the research**: Skills not directly relevant to the research topic
- **Already known information**: Do not re-ask about things already identified during research-intake
