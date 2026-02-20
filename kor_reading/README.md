# Skills for Researcher

연구자를 위한 AI 코딩 에이전트 스킬 모음.
연구 아이디어의 **정보 수집 → 기술적 타당성 분석 → 난이도 산정 → 기술 학습 권장 → 아키텍처 공동 설계**까지를 통합 지원합니다.

> Claude Code, Gemini CLI, Cursor, Codex 등 에이전트 스킬을 지원하는 AI 코딩 도구에서 사용할 수 있습니다.

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
   │  skill-profiler            │  ← 연구 도메인 핵심 개념 중심 역량 질의
   │  stack-analyzer            │  ← 서브 에이전트: 필요 기술 스택 분석
   │                            │
   └────────────┬───────────────┘
                │
                ▼
   ┌──────────────────┐
   │ difficulty-scorer │  ← 보유 역량 vs 필요 기술 대조 → 난이도 0~100
   └────────┬─────────┘     + 강점/부족 분석 + 학습 권장
            │
            ▼
   ┌──────────────────────┐
   │ architecture-designer │  ← 사용자와 대화하며 아키텍처 공동 설계
   └──────────────────────┘
```

---

## 스킬 구성

### 7개 스킬 / 2개 서브 에이전트 / 6개 참조 문서

| 스킬 | 역할 | 타입 |
|------|------|------|
| **research-advisor** | 전체 흐름 오케스트레이션 | 오케스트레이터 |
| **research-intake** | 정보 충분성 판별 + 구체화 질의 | 대화형 (메인 스레드) |
| **feasibility-check** | 기술적 타당성 검증 | 서브 에이전트 |
| **skill-profiler** | 연구 도메인 중심 역량 질의 | 대화형 (메인 스레드) |
| **stack-analyzer** | 필요 기술 스택 도출 | 서브 에이전트 |
| **difficulty-scorer** | 난이도 산정 + 학습 권장 | 채점 엔진 |
| **architecture-designer** | C4-lite 아키텍처 공동 설계 | 대화형 (메인 스레드) |

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
├── skill-profiler/                   # 대화형: 도메인 중심 역량 프로파일링
│   ├── SKILL.md
│   └── references/
│       └── SKILL_CATEGORIES.md       #   도메인별 질문 설계 가이드
│
├── stack-analyzer/                   # 서브 에이전트: 필요 스택 분석
│   ├── SKILL.md
│   └── references/
│       └── TECH_LANDSCAPE.md         #   연구 워크플로우별 도구 레퍼런스
│
├── difficulty-scorer/                # 채점 엔진: 난이도 산정
│   ├── SKILL.md
│   └── references/
│       └── SCORING_RUBRIC.md         #   채점 루브릭
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

각 AI 코딩 도구의 스킬/플러그인 디렉토리에 스킬 폴더를 복사합니다.
경로는 사용하는 도구에 따라 다릅니다.

```bash
# 예시: 스킬 디렉토리가 ~/.ai-tool/skills/ 인 경우
SKILL_DIR=~/.ai-tool/skills

cp -r research-advisor $SKILL_DIR/
cp -r research-intake $SKILL_DIR/
cp -r feasibility-check $SKILL_DIR/
cp -r skill-profiler $SKILL_DIR/
cp -r stack-analyzer $SKILL_DIR/
cp -r difficulty-scorer $SKILL_DIR/
cp -r architecture-designer $SKILL_DIR/
```

설치 후 도구를 재시작하면 자동으로 인식됩니다.

---

## 사용법

### 전체 워크플로우 실행

```
/research-advisor 메시 데이터를 입력받아 ESDF를 활용한 실시간 충돌 회피 에이전트 연구
```

또는 자연어로:

```
"Instant-NGP 기반으로 실내 공간을 실시간 3D 재구성하는 연구를 하고 싶은데, 기술적으로 가능할까?"
```

`research-advisor`가 자동으로 나머지 6개 스킬을 순차/병렬 호출합니다.

### 개별 스킬 사용

일부 스킬은 독립적으로도 사용할 수 있습니다:

```
/research-intake NeRF로 뭔가 재밌는 거 하고 싶어요
```

```
/feasibility-check DeepSDF를 활용한 실시간 3D 형상 생성 및 복원 시스템
```

```
/stack-analyzer 포인트 클라우드 기반 실시간 SLAM 연구
```

```
/architecture-designer Voxel 기반 3D 환경 시뮬레이션 시스템
```

> `skill-profiler`와 `difficulty-scorer`는 이전 단계의 데이터가 필요하므로 주로 `research-advisor`를 통해 자동 호출됩니다.

---

## 각 스킬 상세

### 1. research-advisor

**씬 오케스트레이터** — 흐름 제어와 데이터 전달만 담당합니다.

- 각 스킬의 세부 절차, 질의 방식, 출력 형식을 재정의하지 않음
- 하위 스킬의 SKILL.md 명세를 그대로 따르도록 위임
- 오케스트레이터가 담당하는 것:
  - **실행 순서**: Step 1 → 2 → 3(병렬) → 4 → 5
  - **분기 판단**: 타당성 판정 결과에 따른 진행/종료
  - **데이터 전달**: 이전 Step의 출력 원문을 다음 Step에 전달
  - **최종 요약**: 각 Step 출력을 인용하여 1-page 요약 생성

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

연구자의 역량을 **연구 도메인의 핵심 개념 중심**으로 파악합니다.

- 범용 기술(pandas, Git 등)이 아닌, 연구 주제의 핵심 개념을 질의
- 예: NeRF 연구 → "볼륨 렌더링 원리를 아시나요?", "COLMAP을 사용해보셨나요?"
- 예: ESDF 연구 → "SDF가 뭔지 아시나요?", "메시 데이터를 다뤄보셨나요?"
- 2~3라운드의 도메인 맞춤형 질의로 역량 파악

### 5. stack-analyzer

연구 프로젝트에 **필요한 기술 스택**을 체계적으로 도출합니다.

- 연구 워크플로우를 7단계로 분해 (수집 → 전처리 → 분석 → 실험관리 → 시각화 → 인프라 → 공유)
- 각 단계별 필수/권장 기술과 대안을 제시
- WebSearch로 최신 도구 동향 확인
- 기술 간 의존 관계 명시

### 6. difficulty-scorer

보유 역량과 필요 기술을 대조하여 **0~100 난이도**를 산출합니다.

- 테이블 나열이 아닌, **서술형으로 강점과 부족한 부분을 설명**
- 학습이 필요한 항목을 우선순위(🔴 필수 / 🟡 병행 / 🟢 후순위)로 권장

**난이도 등급:**

| 점수 | 등급 |
|------|------|
| 0~20 | 🟢 쉬움 — 즉시 착수 가능 |
| 21~40 | 🟢 약간 쉬움 — 소폭 학습 후 착수 |
| 41~60 | 🟡 보통 — 핵심 기술 선행 학습 권장 |
| 61~80 | 🟠 어려움 — 멘토링 + 단계적 학습 필요 |
| 81~100 | 🔴 매우 어려움 — 범위 축소 또는 팀 구성 권장 |

### 7. architecture-designer

사용자와 **대화하며** 연구 시스템 아키텍처를 설계합니다.

- Phase A: 맥락 파악 (목표, 데이터, 산출물)
- Phase B: System Context 다이어그램 (L1) — Mermaid
- Phase C: Container/파이프라인 다이어그램 (L2) — Mermaid
- Phase D: 프로젝트 디렉토리 구조 제안
- Phase E: 주요 설계 결정(ADR) 기록

지원하는 아키텍처 패턴 6종: 단순 분석 / 실험 파이프라인 / 데이터 파이프라인 / 모델 서빙 / 멀티모달 통합 / LLM 활용

---

## 설계 원칙: 씬 오케스트레이터

`research-advisor`는 **씬 오케스트레이터** 패턴을 따릅니다.

```
┌─────────────────────────────────────────────────────────┐
│  research-advisor가 하는 것                              │
│                                                         │
│  ✅ 실행 순서 결정  (Step 1 → 2 → 3 → 4 → 5)           │
│  ✅ 분기 판단       (타당성 판정 → 진행/종료)            │
│  ✅ 데이터 전달     (이전 Step 출력 → 다음 Step 입력)    │
│  ✅ 병렬 실행 조율  (skill-profiler ∥ stack-analyzer)    │
│  ✅ 최종 요약       (각 Step 출력을 인용)                │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│  research-advisor가 하지 않는 것                         │
│                                                         │
│  ❌ 하위 스킬의 분석 절차 재정의                          │
│  ❌ 하위 스킬의 출력 형식 축소/변경                       │
│  ❌ 하위 스킬의 질의 방식 재지정                          │
│  ❌ 이전 출력을 재분석 (인용만 함)                        │
└─────────────────────────────────────────────────────────┘
```

이로써 각 스킬의 SKILL.md가 **단일 진실 공급원(Single Source of Truth)**이 되고,
오케스트레이터와 하위 스킬 간의 명세 불일치가 구조적으로 방지됩니다.

### 데이터 흐름 계약

각 Step 간에는 명확한 데이터 계약이 정의되어 있습니다.
오케스트레이터는 이전 Step의 출력 원문을 다음 Step에 그대로 전달합니다.

```
Step 1 research-intake
  출력: 구조화_결과 (7개 정보 축 테이블)
         │
         ▼
Step 2 feasibility-check
  입력: 구조화_결과
  출력: 타당성_결과 (판정 + 기술요소 분석 + 유사사례 + 리스크 + 대안)
         │
    ┌────┴────┐
    ▼         ▼
Step 3-A   Step 3-B
skill-     stack-analyzer
profiler   입력: 구조화_결과 + 타당성_결과.필요기술영역
입력:       출력: 필요_기술_스택 (단계별 테이블 + 통합요약 + 의존관계 + 자원표)
구조화_결과
  출력:
  사용자_기술_프로필
    │         │
    └────┬────┘
         ▼
Step 4 difficulty-scorer
  입력: 사용자_기술_프로필 + 필요_기술_스택
  출력: 난이도_결과 (점수 + 강점/부족 서술 + 학습 권장)
         │
         ▼
Step 5 architecture-designer
  입력: 구조화_결과 + 필요_기술_스택.통합스택요약
  출력: 아키텍처_설계 (L1/L2 다이어그램 + 디렉토리 구조 + ADR)
```

`skill-profiler`가 사용자와 대화하는 **동안** `stack-analyzer`가 백그라운드에서 필요 기술을 분석하므로, 사용자 대기 시간이 최소화됩니다.

---

## 커스터마이징

### 정보 수집 질의 템플릿 수정

`research-intake/references/INTAKE_TEMPLATES.md`에서 각 정보 축의 질의 문항과 선택지를 수정할 수 있습니다.

### 채점 기준 변경

`difficulty-scorer/references/SCORING_RUBRIC.md`에서 채점 기준과 등급별 메시지를 수정할 수 있습니다.

### 도메인별 질문 가이드 추가

새로운 연구 분야를 지원하려면:

1. `skill-profiler/references/SKILL_CATEGORIES.md`에 도메인별 핵심 개념과 질문 예시 추가
2. `stack-analyzer/references/TECH_LANDSCAPE.md`에 도구 레퍼런스 추가
3. `feasibility-check/references/FEASIBILITY_CRITERIA.md`에 성숙도 기준 추가

### 아키텍처 패턴 추가

`architecture-designer/references/ARCHITECTURE_PATTERNS.md`에 새 패턴 섹션을 추가합니다.

---

## 요구사항

- 에이전트 스킬을 지원하는 AI 코딩 도구 (Claude Code, Gemini CLI, Cursor, Codex 등)
- `feasibility-check`과 `stack-analyzer`는 WebSearch를 활용하므로 인터넷 연결이 필요합니다

---

## 라이선스

MIT
