# Detailed Feasibility Assessment Criteria

## 1. Technology Maturity Classification

| Stage | Definition | Assessment Impact |
|-------|-----------|-------------------|
| **Research Stage** | Proposed only in papers, no public implementation | ❌ or ⚠️ (requires custom implementation) |
| **Experimental** | Open-source implementation exists but stability unverified, documentation lacking | ⚠️ |
| **Stable** | Production use cases exist, actively maintained, sufficient documentation | ✅ |
| **Mature** | Industry standard, large community, rich ecosystem | ✅ |

---

## 2. Key Technology Status by Research Domain

### 2.1 Natural Language Processing (NLP)

| Task | Representative Technology/Model | Maturity | Notes |
|------|-------------------------------|----------|-------|
| Text Classification | BERT, RoBERTa, fine-tuning | Mature | Easy to use via Hugging Face |
| Generation | GPT-4, Claude, LLaMA | Mature | API or local execution |
| Information Extraction | spaCy, NER models | Mature | Domain-specific training may be needed |
| Question Answering | RAG, Vector DB + LLM | Stable | LangChain, LlamaIndex |
| Multilingual | mBERT, XLM-R | Stable | Performance varies by language |

### 2.2 Computer Vision (CV)

| Task | Representative Technology/Model | Maturity | Notes |
|------|-------------------------------|----------|-------|
| Image Classification | ResNet, EfficientNet, ViT | Mature | Abundant pretrained models |
| Object Detection | YOLO, DETR | Mature | Real-time capable |
| Segmentation | SAM, Mask R-CNN | Stable | SAM supports zero-shot |
| Generation | Stable Diffusion, DALL-E | Stable | High-end GPU required for training |
| 3D Reconstruction | NeRF, 3D Gaussian Splatting | Experimental | Rapidly advancing |

### 2.3 Data Science / Statistics

| Task | Representative Tools | Maturity | Notes |
|------|---------------------|----------|-------|
| Exploratory Analysis | pandas, matplotlib, seaborn | Mature | Python ecosystem standard |
| Statistical Testing | scipy, statsmodels, R | Mature | |
| Time Series Analysis | Prophet, statsmodels, ARIMA | Stable | |
| Causal Inference | DoWhy, EconML | Experimental~Stable | Tools exist but understanding required |
| Bayesian Analysis | PyMC, Stan | Stable | Steep learning curve |

### 2.4 Reinforcement Learning / Simulation

| Task | Representative Tools | Maturity | Notes |
|------|---------------------|----------|-------|
| Basic RL | Gymnasium, Stable-Baselines3 | Stable | |
| Multi-Agent | PettingZoo, RLlib | Experimental~Stable | |
| Robotics Simulation | MuJoCo, Isaac Sim | Stable | GPU required |
| Custom Environments | Gymnasium API | Stable | Custom implementation required |

### 2.5 Bioinformatics / Medical

| Task | Representative Tools | Maturity | Notes |
|------|---------------------|----------|-------|
| Genomic Analysis | Biopython, GATK | Mature | |
| Protein Structure | AlphaFold, ESMFold | Stable | Pretrained models publicly available |
| Medical Imaging | MONAI, 3D Slicer | Stable | Data accessibility issues |
| Drug Discovery | RDKit, DeepChem | Stable | Domain knowledge essential |

---

## 3. Data Availability Checklist

| Data Type | Verification Items |
|-----------|-------------------|
| **Public Datasets** | Whether it exists on Kaggle, HuggingFace Datasets, UCI ML Repository, or Papers with Code |
| **API Collection** | Whether the service provides an API, rate limits and costs |
| **Web Crawling** | robots.txt permissions, legal issues, data volume |
| **Self-Generated** | Whether it can be generated through experiments/surveys/simulations, time required |
| **Institution-Provided** | Whether accessible data exists from universities/research institutes/hospitals |
| **Synthetic Data** | Whether synthetic data can substitute when real data is unavailable |

---

## 4. Computing Resource Feasibility Criteria

| Level | Specifications | Cost (Monthly) | Target Use |
|-------|---------------|----------------|------------|
| **Personal PC** | CPU + RAM 16-32GB, no GPU or consumer-grade | $0 | Small-scale experiments, preprocessing |
| **Personal PC + GPU** | RTX 3060-4090 | $0 (if owned) | Small to medium-scale training, inference |
| **Cloud GPU** | A100/H100 instances | $1-5/hr | Large-scale training |
| **Google Colab** | T4 free / A100 Pro | $0-$10/month | Prototyping, experimentation |
| **HPC Cluster** | University/institute provided | $0 (if affiliated) | Large-scale experiments |
| **Full Cloud** | Multi-GPU, large-scale storage | $100+/month | Large-scale production |
