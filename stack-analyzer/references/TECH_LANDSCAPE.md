# 연구 분야별 기술 환경 레퍼런스

## 1. 연구 워크플로우별 대표 도구

### 1.1 데이터 수집

| 방법 | 도구/라이브러리 | 난이도 | 적용 사례 |
|------|---------------|--------|-----------|
| 공개 데이터셋 | Hugging Face Datasets, kaggle API, torchvision.datasets | 낮음 | 벤치마크 실험 |
| 웹 크롤링 | requests + BeautifulSoup, Scrapy, Selenium | 중간 | 텍스트/이미지 수집 |
| API 수집 | requests, aiohttp, tweepy(X/Twitter) | 낮음~중간 | SNS, 뉴스 데이터 |
| 센서/IoT | Arduino, Raspberry Pi, MQTT | 높음 | 물리 데이터 수집 |
| 설문/실험 | Google Forms, Qualtrics, PsychoPy | 낮음 | 인간 대상 연구 |
| 합성 데이터 | Faker, SDV(Synthetic Data Vault) | 낮음~중간 | 프라이버시 보호 |

### 1.2 데이터 전처리

| 작업 | 도구/라이브러리 | 난이도 |
|------|---------------|--------|
| 정형 데이터 | pandas, polars | 낮음~중간 |
| 텍스트 정제 | regex, NLTK, spaCy, KoNLPy | 중간 |
| 이미지 처리 | OpenCV, PIL/Pillow, albumentations | 중간 |
| 오디오 처리 | librosa, torchaudio | 중간 |
| 결측치/이상치 | pandas, scikit-learn (imputers) | 낮음 |
| 특성 공학 | scikit-learn, featuretools | 중간 |
| 대용량 처리 | Dask, PySpark, Vaex | 높음 |

### 1.3 분석/모델링

| 영역 | 도구/프레임워크 | 난이도 | 비고 |
|------|---------------|--------|------|
| 통계 분석 | scipy, statsmodels, pingouin | 중간 | 가설검정, 회귀 |
| 전통 ML | scikit-learn, XGBoost, LightGBM | 중간 | 분류, 회귀, 클러스터링 |
| 딥러닝 | PyTorch, TensorFlow | 높음 | 커스텀 모델 |
| NLP | Hugging Face Transformers, spaCy | 중간~높음 | fine-tuning, NER |
| CV | torchvision, ultralytics(YOLO), detectron2 | 중간~높음 | 분류, 탐지, 분할 |
| 강화학습 | Gymnasium, Stable-Baselines3 | 높음 | RL 연구 |
| 그래프 | PyTorch Geometric, NetworkX | 높음 | GNN, 네트워크 분석 |
| 시계열 | Prophet, NeuralProphet, tslearn | 중간 | 예측, 분류 |
| 생존분석 | lifelines, scikit-survival | 중간 | 의료/사회과학 |
| 베이지안 | PyMC, NumPyro, Stan | 높음 | 확률적 추론 |
| LLM 활용 | LangChain, LlamaIndex, Claude/OpenAI API | 중간 | RAG, 에이전트 |

### 1.4 실험 관리

| 도구 | 난이도 | 특징 |
|------|--------|------|
| MLflow | 중간 | 오픈소스, 실험 추적 + 모델 레지스트리 |
| Weights & Biases | 낮음 | SaaS, 시각화 우수, 학생 무료 |
| Neptune.ai | 낮음 | SaaS, 팀 협업 |
| TensorBoard | 낮음 | TF/PyTorch 통합 |
| Sacred + Omniboard | 중간 | 오픈소스, 가벼움 |
| Hydra | 중간 | 설정 관리 |
| DVC | 중간 | 데이터 버전 관리 |

### 1.5 시각화/보고

| 도구 | 난이도 | 용도 |
|------|--------|------|
| matplotlib | 낮음 | 기본 차트, 논문 그래프 |
| seaborn | 낮음 | 통계 시각화 |
| plotly | 낮음~중간 | 인터랙티브 시각화 |
| Streamlit | 낮음 | 데모 웹앱 |
| Gradio | 낮음 | ML 데모 UI |
| LaTeX (+ pgfplots) | 중간 | 논문 품질 그래프 |
| D3.js | 높음 | 커스텀 인터랙티브 |

### 1.6 인프라/환경

| 도구 | 난이도 | 용도 |
|------|--------|------|
| conda / pip + venv | 낮음 | 환경 격리 |
| Docker | 중간 | 재현성 보장 |
| Google Colab | 매우 낮음 | 무료 GPU, 프로토타이핑 |
| AWS SageMaker | 중간~높음 | 클라우드 ML |
| GCP Vertex AI | 중간~높음 | 클라우드 ML |
| SLURM | 중간 | HPC 작업 관리 |
| Ray | 중간~높음 | 분산 컴퓨팅 |

---

## 2. 연구 유형별 권장 스택 조합

### 2.1 논문 재현 / 벤치마크 실험

```
Python + PyTorch + Hugging Face + W&B + conda
```

### 2.2 탐색적 데이터 분석 연구

```
Python + pandas + scipy + matplotlib/seaborn + Jupyter + Git
```

### 2.3 딥러닝 모델 개발 연구

```
Python + PyTorch + Hugging Face + W&B/MLflow + Docker + GPU(Colab/Cloud)
```

### 2.4 LLM 활용 연구 (RAG, 에이전트 등)

```
Python + LangChain/LlamaIndex + Claude/OpenAI API + 벡터DB + Streamlit
```

### 2.5 대규모 데이터 처리 연구

```
Python + PySpark/Dask + SQL + Docker + 클라우드(AWS/GCP)
```

### 2.6 시뮬레이션 / 강화학습 연구

```
Python + PyTorch + Gymnasium + Stable-Baselines3 + W&B + GPU
```
