# Skills for Researcher

연구자를 위한 Claude Code 에이전트 스킬 모음.
연구 아이디어의 **정보 수집 → 기술적 타당성 분석 → 난이도 정량 산정 → 기술 학습 권장 → 아키텍처 공동 설계**까지를 통합 지원합니다.

---

## 한눈에 보기

```
사용자: "이 연구 주제, 현재 기술로 가능할까?"
          │
          ▼
   ┌─────────────────┐
   │ research-advisor │  ← 오케스트레이터: 전체 흐름 제어
   └────────┬────────┘
            │
            ▼
   ┌─────────────────┐
   │ research-intake  │  ← 정보 충분성 판별 + 플랜 모드 질의
   └────────┬────────┘
            │
            ├─ 정보 충분 → 구조화 결과 확정
            └─ 정보 부족 → 단계적 질의 (최대 3라운드) → 구조화 결과 확정
            │
            ▼
   ┌──────────────────┐
   │ feasibility-check│  ← 서브 에이전트: 현존 기술로 구현 가능한지 검증
   └────────┬─────────┘
            │
       가능 │          불가 → 사유 설명 + 대안 제시 → 종료
            ▼
   ┌────────────────────────────┐
   │        병렬 실행            │
   │                            │
   │  skill-profiler            │  ← 사용자에게 기술 역량 단계적 질의
   │  stack-analyzer            │  ← 서브 에이전트: 필요 기술 스택 분석
   │                            │
   └────────────┬───────────────┘
                │
                ▼
   ┌──────────────────┐
   │ difficulty-scorer │  ← 보유 기술 vs 필요 기술 대조 → 난이도 0~100 채점
   └────────┬─────────┘     + 부족 기술 학습 권장
            │
            ▼
   ┌──────────────────────┐
   │ architecture-designer │  ← 사용자와 대화하며 아키텍처 공동 설계
   └──────────────────────┘
```

---

## 스킬 구성

### 7개 스킬 / 2개 서브 에이전트 / 6개 참조 문서

| 스킬 | 역할 | 타입 | 슬래시 커맨드 |
|------|------|------|-------------|
| **research-advisor** | 전체 흐름 오케스트레이션 | 오케스트레이터 | `/research-advisor` |
| **research-intake** | 정보 충분성 판별 + 구체화 질의 | 대화형 (메인 스레드) | `/research-intake` |
| **feasibility-check** | 기술적 타당성 검증 | 서브 에이전트 (`context: fork`) | `/feasibility-check` |
| **skill-profiler** | 연구자 기술 역량 질의 | 대화형 (메인 스레드) | `/skill-profiler` |
| **stack-analyzer** | 필요 기술 스택 도출 | 서브 에이전트 (`context: fork`) | `/stack-analyzer` |
| **difficulty-scorer** | 난이도 정량 채점 + 학습 권장 | 채점 엔진 | `/difficulty-scorer` |
| **architecture-designer** | C4-lite 아키텍처 공동 설계 | 대화형 (메인 스레드) | `/architecture-designer` |

---

## 디렉토리 구조

```
skills_for_researcher/
│
├── research-advisor/                 # 오케스트레이터
│   └── SKILL.md
│
├── research-intake/                  # 정보 수집 & 구체화
│   ├── SKILL.md
│   └── references/
│       └── INTAKE_TEMPLATES.md       #   7개 정보 축별 질의 템플릿
│
├── feasibility-check/                # 서브 에이전트: 타당성 검증
│   ├── SKILL.md
│   └── references/
│       └── FEASIBILITY_CRITERIA.md   #   분야별 기술 성숙도, 데이터 확보 기준
│
├── skill-profiler/                   # 대화형: 기술 역량 프로파일링
│   ├── SKILL.md
│   └── references/
│       └── SKILL_CATEGORIES.md       #   연구 분야별 기술 카테고리 사전
│
├── stack-analyzer/                   # 서브 에이전트: 필요 스택 분석
│   ├── SKILL.md
│   └── references/
│       └── TECH_LANDSCAPE.md         #   연구 워크플로우별 도구 레퍼런스
│
├── difficulty-scorer/                # 채점 엔진: 난이도 산정
│   ├── SKILL.md
│   └── references/
│       └── SCORING_RUBRIC.md         #   5개 차원 채점 루브릭 상세
│
├── architecture-designer/            # 대화형: 아키텍처 공동 설계
│   ├── SKILL.md
│   └── references/
│       └── ARCHITECTURE_PATTERNS.md  #   연구 프로젝트 아키텍처 패턴 6종
│
└── README.md
```

---

## 설치

### 개인용 (모든 프로젝트에서 사용)

```bash
# 각 스킬 폴더를 ~/.claude/skills/ 에 복사
cp -r research-advisor ~/.claude/skills/
cp -r research-intake ~/.claude/skills/
cp -r feasibility-check ~/.claude/skills/
cp -r skill-profiler ~/.claude/skills/
cp -r stack-analyzer ~/.claude/skills/
cp -r difficulty-scorer ~/.claude/skills/
cp -r architecture-designer ~/.claude/skills/
```

### 프로젝트용 (특정 프로젝트에서만 사용)

```bash
# 각 스킬 폴더를 프로젝트의 .claude/skills/ 에 복사
mkdir -p .claude/skills
cp -r research-advisor .claude/skills/
cp -r research-intake .claude/skills/
cp -r feasibility-check .claude/skills/
cp -r skill-profiler .claude/skills/
cp -r stack-analyzer .claude/skills/
cp -r difficulty-scorer .claude/skills/
cp -r architecture-designer .claude/skills/
```

설치 후 Claude Code를 재시작하면 자동으로 인식됩니다.

---

## 사용법

### 전체 워크플로우 실행

```
/research-advisor 한국어 학술 논문에서 핵심 주장을 자동 추출하는 NLP 시스템
```

또는 자연어로:

```
"LLM을 활용한 코드 취약점 자동 탐지 연구를 하고 싶은데, 기술적으로 가능할까?"
```

`research-advisor`가 자동으로 나머지 6개 스킬을 순차/병렬 호출합니다.

### 개별 스킬 사용

각 스킬은 독립적으로도 사용할 수 있습니다:

```
/research-intake LLM으로 뭔가 재밌는 거 하고 싶어요
```

```
/feasibility-check 소규모 LLM을 fine-tuning해서 의료 QA 시스템 구축
```

```
/skill-profiler
```

```
/stack-analyzer 강화학습 기반 로봇 경로 계획 연구
```

```
/difficulty-scorer
```

```
/architecture-designer RAG 기반 논문 검색 시스템
```

---

## 각 스킬 상세

### 1. research-advisor

전체 분석 흐름을 제어하는 **오케스트레이터**입니다.

- `research-intake`로 정보 충분성을 먼저 확보
- `feasibility-check` 서브 에이전트를 호출하여 타당성 판정
- 구현 가능 판정 시 `skill-profiler`와 `stack-analyzer`를 **병렬** 실행
- 두 결과를 `difficulty-scorer`에 전달하여 난이도 채점
- 마지막으로 `architecture-designer`로 아키텍처 공동 설계

### 2. research-intake

분석의 품질을 좌우하는 **첫 번째 관문**입니다.

사용자의 아이디어를 7개 정보 축으로 평가합니다:

| # | 정보 축 | 설명 |
|---|---------|------|
| 1 | 문제 정의 | 어떤 문제를 해결/탐구하려 하는가? |
| 2 | 연구 목적 | 왜 이 연구를 하는가? |
| 3 | 데이터 | 어떤 데이터가 필요하고 확보 가능한가? |
| 4 | 핵심 기능/방법 | 구체적으로 무엇을 구현/분석하는가? |
| 5 | 산출물 | 최종 결과물은 무엇인가? |
| 6 | 규모/범위 | 프로젝트 기간과 인원 |
| 7 | 제약 조건 | 예산, 장비, 기간 등 제약 |

**작동 방식:**
- 각 축을 ✅ 충분 / 🟡 부분적 / ❌ 부족으로 평가
- 충분하면 추가 질의 없이 바로 통과
- 부족하면 **플랜 모드** 진입: 부족한 항목만 선택지 기반으로 단계적 질의 (최대 3라운드)
- "잘 모르겠다"도 유효 → 합리적 추정으로 보완 (추정 표기)
- 최종 구조화 결과를 사용자에게 확인받고 확정

### 3. feasibility-check

연구 아이디어가 **현존하는 기술로 실현 가능한지** 판단합니다.

- WebSearch로 최신 기술 동향, 유사 연구 사례를 조사
- 3단계 판정: **구현 가능** / **조건부 가능** / **구현 불가**
- 모든 판정에 근거를 명시
- 구현 불가 시 대안 방향을 제시

### 4. skill-profiler

연구자의 기술 역량을 **단계적으로** 파악합니다.

- Round 1: 주 프로그래밍 언어 + 연구 분야
- Round 2: 분야 맞춤형 세부 기술 (ML, NLP, CV 등)
- Round 3: 인프라 & 개발 환경 경험
- Round 4: 프로젝트 경험 규모
- 결과: 카테고리별 기술/숙련도 테이블

### 5. stack-analyzer

연구 프로젝트에 **필요한 기술 스택**을 체계적으로 도출합니다.

- 연구 워크플로우를 7단계로 분해 (수집 → 전처리 → 분석 → 실험관리 → 시각화 → 인프라 → 공유)
- 각 단계별 필수/권장 기술과 대안을 제시
- WebSearch로 최신 도구 동향 확인
- 기술 간 의존 관계 명시

### 6. difficulty-scorer

보유 기술과 필요 기술을 대조하여 **0~100 난이도**를 산출합니다.

**채점 차원 (가중치):**

| 차원 | 가중치 |
|------|--------|
| 기술 격차 | 35% |
| 연구 복잡도 | 25% |
| 도구 통합도 | 15% |
| 인프라 요구도 | 15% |
| 프로젝트 규모 | 10% |

**난이도 등급:**

| 점수 | 등급 |
|------|------|
| 0~20 | 🟢 쉬움 — 즉시 착수 가능 |
| 21~40 | 🟢 약간 쉬움 — 소폭 학습 후 착수 |
| 41~60 | 🟡 보통 — 핵심 기술 선행 학습 권장 |
| 61~80 | 🟠 어려움 — 멘토링 + 단계적 학습 필요 |
| 81~100 | 🔴 매우 어려움 — 범위 축소 또는 팀 구성 권장 |

채점 후 부족한 기술에 대해 **학습 우선순위**(🔴 필수 선행 / 🟡 병행 / 🟢 후순위)와 구체적인 학습 경로를 권장합니다.

### 7. architecture-designer

사용자와 **대화하며** 연구 시스템 아키텍처를 설계합니다.

- Phase A: 맥락 파악 (목표, 데이터, 산출물)
- Phase B: System Context 다이어그램 (L1) — Mermaid
- Phase C: Container/파이프라인 다이어그램 (L2) — Mermaid
- Phase D: 프로젝트 디렉토리 구조 제안
- Phase E: 주요 설계 결정(ADR) 기록

지원하는 아키텍처 패턴 6종: 단순 분석 / 실험 파이프라인 / 데이터 파이프라인 / 모델 서빙 / 멀티모달 통합 / LLM 활용

---

## 실행 구조 상세

### 정보 수집 단계 (research-intake)

```
사용자 입력: "LLM으로 뭔가 하고 싶어요"
                │
                ▼
        ┌───────────────────┐
        │ 7개 정보 축 평가   │
        │ ✅✅❌❌❌🟡❌    │
        └───────┬───────────┘
                │
                ▼
        ┌───────────────────┐
        │ 현재 상태 공유     │  "파악된 내용은 이렇고, 부족한 부분을 여쭤볼게요"
        └───────┬───────────┘
                │
         ┌──────┴──────┐
         ▼             ▼
     Round 1        Round 2        Round 3 (필요 시)
    핵심 질의      보충 질의        최종 확인
    (❌ 항목)     (🟡 항목)
         │             │              │
         └──────┬──────┘──────────────┘
                ▼
        ┌───────────────────┐
        │ 구조화 결과 출력   │
        │ + 사용자 확인      │
        └───────────────────┘
```

### 병렬 분석 단계 (skill-profiler + stack-analyzer)

```
                     research-advisor (메인 스레드)
                            │
                 ┌──────────┴──────────┐
                 │                     │
          메인 스레드               백그라운드
       skill-profiler            stack-analyzer
    (사용자와 대화 중)          (서브 에이전트가 독립 분석)
                 │                     │
                 └──────────┬──────────┘
                            │
                     difficulty-scorer
                     (두 결과를 합산)
```

`skill-profiler`가 사용자와 대화하는 **동안** `stack-analyzer`가 백그라운드에서 필요 기술을 분석하므로, 사용자 대기 시간이 최소화됩니다.

---

## 커스터마이징

### 정보 수집 질의 템플릿 수정

`research-intake/references/INTAKE_TEMPLATES.md`에서 각 정보 축의 질의 문항과 선택지를 수정할 수 있습니다.

### 채점 가중치 변경

`difficulty-scorer/SKILL.md`의 차원별 가중치를 수정하면 채점 기준을 조정할 수 있습니다.

### 기술 카테고리 추가

새로운 연구 분야를 지원하려면:

1. `skill-profiler/references/SKILL_CATEGORIES.md`에 분야별 기술 추가
2. `stack-analyzer/references/TECH_LANDSCAPE.md`에 도구 레퍼런스 추가
3. `feasibility-check/references/FEASIBILITY_CRITERIA.md`에 성숙도 기준 추가

### 아키텍처 패턴 추가

`architecture-designer/references/ARCHITECTURE_PATTERNS.md`에 새 패턴 섹션을 추가합니다.

---

## 요구사항

- **Claude Code** (Claude Code CLI)
- 스킬은 Claude Code의 [Agent Skills](https://code.claude.com/docs/en/skills) 표준을 따릅니다
- `feasibility-check`과 `stack-analyzer`는 WebSearch를 활용하므로 인터넷 연결이 필요합니다

---

## 라이선스

MIT
