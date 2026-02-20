# Technology Landscape Reference by Research Domain

## 1. Representative Tools by Research Workflow

### 1.1 Data Collection

| Method | Tools/Libraries | Difficulty | Use Cases |
|--------|----------------|------------|-----------|
| Public Datasets | Hugging Face Datasets, kaggle API, torchvision.datasets | Low | Benchmark experiments |
| Web Crawling | requests + BeautifulSoup, Scrapy, Selenium | Medium | Text/image collection |
| API Collection | requests, aiohttp, tweepy (X/Twitter) | Low~Medium | Social media, news data |
| Sensors/IoT | Arduino, Raspberry Pi, MQTT | High | Physical data collection |
| Surveys/Experiments | Google Forms, Qualtrics, PsychoPy | Low | Human subjects research |
| Synthetic Data | Faker, SDV (Synthetic Data Vault) | Low~Medium | Privacy protection |

### 1.2 Data Preprocessing

| Task | Tools/Libraries | Difficulty |
|------|----------------|------------|
| Structured Data | pandas, polars | Low~Medium |
| Text Cleaning | regex, NLTK, spaCy, KoNLPy (for Korean NLP) | Medium |
| Image Processing | OpenCV, PIL/Pillow, albumentations | Medium |
| Audio Processing | librosa, torchaudio | Medium |
| Missing Values/Outliers | pandas, scikit-learn (imputers) | Low |
| Feature Engineering | scikit-learn, featuretools | Medium |
| Large-Scale Processing | Dask, PySpark, Vaex | High |

### 1.3 Analysis/Modeling

| Domain | Tools/Frameworks | Difficulty | Notes |
|--------|-----------------|------------|-------|
| Statistical Analysis | scipy, statsmodels, pingouin | Medium | Hypothesis testing, regression |
| Traditional ML | scikit-learn, XGBoost, LightGBM | Medium | Classification, regression, clustering |
| Deep Learning | PyTorch, TensorFlow | High | Custom models |
| NLP | Hugging Face Transformers, spaCy | Medium~High | Fine-tuning, NER |
| CV | torchvision, ultralytics (YOLO), detectron2 | Medium~High | Classification, detection, segmentation |
| Reinforcement Learning | Gymnasium, Stable-Baselines3 | High | RL research |
| Graph | PyTorch Geometric, NetworkX | High | GNN, network analysis |
| Time Series | Prophet, NeuralProphet, tslearn | Medium | Forecasting, classification |
| Survival Analysis | lifelines, scikit-survival | Medium | Medical/social science |
| Bayesian | PyMC, NumPyro, Stan | High | Probabilistic inference |
| LLM Utilization | LangChain, LlamaIndex, Claude/OpenAI API | Medium | RAG, agents |

### 1.4 Experiment Management

| Tool | Difficulty | Features |
|------|------------|----------|
| MLflow | Medium | Open-source, experiment tracking + model registry |
| Weights & Biases | Low | SaaS, excellent visualization, free for students |
| Neptune.ai | Low | SaaS, team collaboration |
| TensorBoard | Low | TF/PyTorch integration |
| Sacred + Omniboard | Medium | Open-source, lightweight |
| Hydra | Medium | Configuration management |
| DVC | Medium | Data version control |

### 1.5 Visualization/Reporting

| Tool | Difficulty | Purpose |
|------|------------|---------|
| matplotlib | Low | Basic charts, publication-quality graphs |
| seaborn | Low | Statistical visualization |
| plotly | Low~Medium | Interactive visualization |
| Streamlit | Low | Demo web apps |
| Gradio | Low | ML demo UI |
| LaTeX (+ pgfplots) | Medium | Publication-quality graphs |
| D3.js | High | Custom interactive visualizations |

### 1.6 Infrastructure/Environment

| Tool | Difficulty | Purpose |
|------|------------|---------|
| conda / pip + venv | Low | Environment isolation |
| Docker | Medium | Reproducibility |
| Google Colab | Very Low | Free GPU, prototyping |
| AWS SageMaker | Medium~High | Cloud ML |
| GCP Vertex AI | Medium~High | Cloud ML |
| SLURM | Medium | HPC job management |
| Ray | Medium~High | Distributed computing |

---

## 2. Recommended Stack Combinations by Research Type

### 2.1 Paper Reproduction / Benchmark Experiments

```
Python + PyTorch + Hugging Face + W&B + conda
```

### 2.2 Exploratory Data Analysis Research

```
Python + pandas + scipy + matplotlib/seaborn + Jupyter + Git
```

### 2.3 Deep Learning Model Development Research

```
Python + PyTorch + Hugging Face + W&B/MLflow + Docker + GPU (Colab/Cloud)
```

### 2.4 LLM Utilization Research (RAG, Agents, etc.)

```
Python + LangChain/LlamaIndex + Claude/OpenAI API + Vector DB + Streamlit
```

### 2.5 Large-Scale Data Processing Research

```
Python + PySpark/Dask + SQL + Docker + Cloud (AWS/GCP)
```

### 2.6 Simulation / Reinforcement Learning Research

```
Python + PyTorch + Gymnasium + Stable-Baselines3 + W&B + GPU
```
