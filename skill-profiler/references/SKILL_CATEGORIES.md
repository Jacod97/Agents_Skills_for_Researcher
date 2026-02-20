# 연구 분야별 기술 카테고리

## 1. 공통 기술

모든 연구 분야에 공통적으로 해당하는 기술입니다.

| 카테고리 | 기술 | 설명 |
|----------|------|------|
| 언어 | Python | 연구 생태계의 사실상 표준 |
| 언어 | R | 통계 분석, 생물통계 |
| 언어 | Julia | 고성능 과학 컴퓨팅 |
| 데이터 처리 | pandas | 정형 데이터 처리 |
| 데이터 처리 | numpy | 수치 연산 |
| 시각화 | matplotlib | 기본 시각화 |
| 시각화 | seaborn | 통계 시각화 |
| 시각화 | plotly | 인터랙티브 시각화 |
| 환경 | Jupyter Notebook/Lab | 실험 환경 |
| 환경 | Git/GitHub | 버전 관리 |
| 환경 | conda/pip | 패키지 관리 |
| 문서 | LaTeX | 논문 작성 |
| 문서 | Markdown | 문서 작성 |

---

## 2. 데이터 사이언스 / 통계 분석

| 카테고리 | 기술 | 숙련도 질의 기준 |
|----------|------|-----------------|
| 통계 | scipy.stats | 가설 검정, 분포 적합 경험 |
| 통계 | statsmodels | 회귀 분석, 시계열 경험 |
| 통계 | R (tidyverse) | R 기반 데이터 분석 파이프라인 |
| DB | SQL (PostgreSQL, MySQL) | 쿼리 작성 및 데이터 추출 |
| DB | NoSQL (MongoDB) | 비정형 데이터 저장/조회 |
| 시각화 | ggplot2 (R) | R 기반 시각화 |
| 시각화 | Tableau / Power BI | 대시보드 제작 |
| ETL | Apache Airflow | 데이터 파이프라인 |
| ETL | dbt | 데이터 변환 |
| 빅데이터 | PySpark | 대규모 분산 처리 |

---

## 3. 머신러닝 / 딥러닝

| 카테고리 | 기술 | 숙련도 질의 기준 |
|----------|------|-----------------|
| 전통 ML | scikit-learn | 분류/회귀/클러스터링 경험 |
| 전통 ML | XGBoost / LightGBM | 부스팅 모델 경험 |
| 딥러닝 | PyTorch | 모델 구축/학습 경험 |
| 딥러닝 | TensorFlow / Keras | 모델 구축/학습 경험 |
| 딥러닝 | JAX | 고성능 연산 경험 |
| 실험관리 | MLflow | 실험 추적 경험 |
| 실험관리 | Weights & Biases | 실험 추적/시각화 |
| 하이퍼파라미터 | Optuna | 자동 튜닝 경험 |
| 배포 | ONNX / TorchServe | 모델 서빙 경험 |
| 데이터 | Hugging Face Datasets | 데이터셋 로딩/처리 |
| GPU | CUDA 프로그래밍 | GPU 직접 활용 |

---

## 4. 자연어 처리 (NLP)

| 카테고리 | 기술 | 숙련도 질의 기준 |
|----------|------|-----------------|
| 전처리 | 토큰화 (tokenization) | 직접 구현 또는 라이브러리 사용 |
| 전처리 | spaCy / KoNLPy | 형태소 분석, NER |
| 모델 | Hugging Face Transformers | 사전학습 모델 fine-tuning |
| 모델 | sentence-transformers | 임베딩 생성 |
| LLM | OpenAI API / Claude API | LLM API 호출 경험 |
| LLM | LangChain / LlamaIndex | LLM 앱 프레임워크 |
| 검색 | 벡터 DB (Chroma, Pinecone, Weaviate) | RAG 구축 경험 |
| 평가 | BLEU, ROUGE, BERTScore | 생성 모델 평가 |

---

## 5. 컴퓨터 비전 (CV)

| 카테고리 | 기술 | 숙련도 질의 기준 |
|----------|------|-----------------|
| 기본 | OpenCV | 이미지 처리 기본 |
| 기본 | PIL / Pillow | 이미지 입출력 |
| 모델 | torchvision | 사전학습 모델 활용 |
| 모델 | YOLO (ultralytics) | 객체 탐지 |
| 모델 | Segment Anything (SAM) | 세그멘테이션 |
| 증강 | albumentations | 데이터 증강 |
| 3D | Open3D / PCL | 포인트 클라우드 처리 |
| 의료 | MONAI | 의료 영상 분석 |

---

## 6. 인프라 / 컴퓨팅

| 카테고리 | 기술 | 숙련도 질의 기준 |
|----------|------|-----------------|
| 컨테이너 | Docker | 이미지 빌드/실행 경험 |
| 오케스트레이션 | Kubernetes | 클러스터 운영 경험 |
| 클라우드 | AWS (EC2, S3, SageMaker) | 서비스별 사용 경험 |
| 클라우드 | GCP (Vertex AI, GCE) | 서비스별 사용 경험 |
| 클라우드 | Azure (ML Studio) | 서비스별 사용 경험 |
| HPC | SLURM | 작업 스케줄러 사용 |
| GPU | Google Colab | 무료 GPU 활용 |
| GPU | Lambda Cloud / RunPod | GPU 클라우드 |
| CI/CD | GitHub Actions | 자동화 파이프라인 |

---

## 7. 숙련도 판정 기준

### 자동 숙련도 추정

사용자의 답변으로부터 숙련도를 아래 기준으로 추정합니다:

| 신호 | 추정 숙련도 |
|------|------------|
| "들어봤다", "이름만 안다" | 입문 이하 (없음) |
| "튜토리얼을 따라해봤다", "수업에서 써봤다" | 입문 |
| "과제/프로젝트에서 사용했다" | 초급 |
| "연구에서 직접 활용하고 있다", "문제 해결에 사용한다" | 중급 |
| "내부 동작을 이해한다", "커스텀 구현 가능", "남에게 가르칠 수 있다" | 고급 |
