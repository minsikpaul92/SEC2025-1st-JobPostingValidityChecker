# 🥇 SEC 2025 Hackathon - 1st Place Winner
# Job Posting Validity Checker

**Team name:** codeXperts  
**Project title:** Job Posting Validity Checker

---

## 👥 Team Members & Contributions

### Minsik Kim — Backend · Scikit-learn · ML Logic
- FastAPI 백엔드 서버 설계 및 구현 (`backend/main.py`, `backend/models.py`)
- 하이브리드 규칙 기반 + 머신러닝 텍스트 분류기 개발 (`model_textbase/classify_posting.py`, `backend/textbase_classifier_loader.py`)
- Scikit-learn 기반 LogisticRegression 모델 학습 및 저장 (`textbase_classifier.pkl`)
- RandomForest 투명성 점수 모델 개발 (`models_ml/models.py`, `transparency_model.pkl`)
- TF-IDF + 수치 피처 엔지니어링, 온타리오 2026 규정 기반 규칙 설계
- 필드 유효성 검증 유틸리티 개발 (`models_ml/models_field_base.py`)

### Tan Dat — Frontend · Docker · Deployment
- React + Vite 프론트엔드 프로젝트 구성 및 백엔드 API 연동
- 폼(Form) 기반 검증 컴포넌트 구현 (`frontend/src/components/form/form.tsx`)
- 텍스트 입력 기반 검증 컴포넌트 구현 (`frontend/src/components/text-area/text-area.tsx`)
- Docker 컨테이너 설정: `backend/Dockerfile`, `frontend/Dockerfile`
- Docker Compose 멀티 서비스 오케스트레이션 (`docker-compose.yml`)
- 개발 환경 및 배포 파이프라인 구성

### Khai Ngo — Frontend · UI/UX
- 전체 UI/UX 디자인 및 사용자 경험 설계
- 결과 표시 컴포넌트 구현 (`frontend/src/components/result/result.tsx`)
- 헤더 컴포넌트 및 탭 인터페이스 구현 (`frontend/src/components/header/header.tsx`)
- shadcn/ui + Tailwind CSS 기반 컴포넌트 시스템 구성
- 검증 결과 시각화 (신뢰도, 투명성 점수, 누락 필드 표시)
- 반응형 레이아웃 및 색상 코딩 (VALID/INVALID 상태 구분)

---

## 📌 프로젝트 개요

온타리오주 2026년 구인공고 투명성 요건(Working for Workers Four Act, 2024)에 따라 구인공고의 적법성을 자동으로 검증하는 웹 애플리케이션입니다.

### 주요 기능
- **Form 기반 검증**: 9개 필드를 직접 입력하여 검증
- **텍스트 기반 검증**: 구인공고 원문을 붙여넣어 규칙 + ML 모델로 분석
- **투명성 점수**: RandomForest 모델이 공고의 투명성 수준을 0~100%로 평가
- **위반 항목 안내**: 누락 필드 및 규정 위반 이유를 명시

---

## 🏗️ 시스템 아키텍처

```
User Interface (React + Vite + Tailwind)
  ├── Form Tab → 9개 필드 입력 → POST /jobs-postings/field-base
  └── Text Box Tab → 원문 텍스트 → POST /jobs-postings/text-base
              ↓
      FastAPI Backend (backend/main.py)
          ├── /field-base: 누락 필드 체크 + RF 투명성 점수
          └── /text-base: 규칙 기반 검사 + LogisticRegression 분류
              ↓
      Result Display (result.tsx)
          ├── 분류 결과 (VALID / INVALID)
          ├── 신뢰도 (%)
          ├── 투명성 점수 (%)
          └── 누락 필드 목록
```

---

## 📁 프로젝트 구조

```
SEC2025-1st-JobPostingValidityChecker/
├── backend/                          # FastAPI 백엔드 서비스
│   ├── main.py                       # API 엔드포인트 (3개)
│   ├── models.py                     # Pydantic 데이터 모델
│   ├── textbase_classifier_loader.py # 텍스트 분류기 로더 + 규칙 추출
│   ├── textbase_classifier.pkl       # 학습된 LogisticRegression 모델
│   ├── transparency_model.pkl        # 학습된 RandomForest 투명성 모델
│   ├── requirements.txt              # 백엔드 의존성
│   └── Dockerfile                    # 백엔드 Docker 설정
├── frontend/                         # React + Vite + Tailwind UI
│   ├── src/
│   │   ├── App.tsx                   # 루트 컴포넌트 (탭 인터페이스)
│   │   ├── components/
│   │   │   ├── form/form.tsx         # 폼 기반 검증 입력
│   │   │   ├── text-area/text-area.tsx # 텍스트 기반 검증 입력
│   │   │   ├── result/result.tsx     # 결과 표시 컴포넌트
│   │   │   ├── header/header.tsx     # 헤더 (캐나다 국기 포함)
│   │   │   └── ui/                   # shadcn/ui 공용 컴포넌트
│   │   └── lib/
│   │       ├── validation.ts         # ValidationResult 타입 정의
│   │       └── utils.ts              # 유틸리티 함수
│   ├── package.json
│   ├── vite.config.ts
│   ├── tsconfig.json
│   ├── Dockerfile                    # 프론트엔드 Docker 설정
│   └── index.html
├── model_textbase/                   # 규칙 우선 텍스트 분류기
│   ├── classify_posting.py           # PostingClassifier 클래스
│   ├── textbase_classifier.pkl       # 사전 학습 모델
│   └── dataset/
│       ├── job_postings_dataset.csv  # 구조화된 데이터셋
│       ├── raw_postings/             # 유효/무효 샘플 공고 (각 10개)
│       └── test_postings/            # 테스트용 공고 (10개)
├── models_ml/                        # ML 투명성 점수 실험
│   ├── models.py                     # RandomForest 투명성 모델 학습
│   ├── models_field_base.py          # 필드 유효성 검증 유틸리티
│   └── transparency_model.pkl        # 학습된 RF 모델
├── dataset/                          # 공유 데이터 참조
├── docker-compose.yml                # 멀티 컨테이너 오케스트레이션
└── README.md
```

---

## 🔑 핵심 기술 구현

### 1. 하이브리드 규칙 + ML 모델 (`model_textbase/classify_posting.py`)
- **하드 규칙 우선**: 필수 필드 누락, 급여 범위 초과($50k 이상 폭), AI 미공개, 캐나다 경력 요구 등은 즉시 `INVALID` 판정
- **ML 폴백**: 규칙 위반 없을 경우 규칙 파생 피처로 `LogisticRegression` 분류
- 위반 이유를 구체적으로 반환

### 2. 백엔드 엔드포인트 (`backend/main.py`)
| 엔드포인트 | 메서드 | 설명 |
|---|---|---|
| `/jobs-postings/` | GET | 샘플 공고 텍스트 목록 반환 |
| `/jobs-postings/text-base` | POST | 원문 텍스트 분류 (규칙 + LogisticRegression) |
| `/jobs-postings/field-base` | POST | 필드 검증 + RF 투명성 점수 |

### 3. ML 투명성 모델 (`models_ml/models.py`)
- TF-IDF (100 피처) + 수치 피처(필드 완성도, 고용 형태, AI 공개 여부, 급여 존재)
- RandomForest 분류기로 투명성 라벨 예측 (1 = 모든 필드 존재, 0 = 누락 있음)
- 70/30 학습/평가 분할

### 4. 프론트엔드 (`frontend/src/`)
- React 19 + TypeScript + Tailwind CSS + shadcn/ui
- Form 탭: 9개 필드 폼 입력 (title, salary, location, employer, description, requirements, benefits, employment_type, ai_used)
- Text Box 탭: 원문 붙여넣기
- 결과: 분류(VALID/INVALID), 신뢰도, 투명성 점수, 누락 필드 색상 코딩 표시

---

## 🚀 실행 방법

### 방법 1: Docker Compose (권장)

```bash
docker compose up --build
```

- 프론트엔드: http://localhost:5173
- 백엔드: http://localhost:8000

---

### 방법 2: 수동 실행

#### 사전 조건
- Python 3.11+
- Node.js 18+

#### 백엔드 (FastAPI)
```bash
cd backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload
# → http://localhost:8000
```

#### 프론트엔드 (React + Vite)
```bash
cd frontend
npm install
npm run dev
# → http://localhost:5173
```

#### 텍스트 분류기 (단독 실행)
```bash
cd model_textbase
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python classify_posting.py
# → 테스트 인덱스(1-10) 또는 .txt 파일 경로 입력
```

#### ML 투명성 모델 학습
```bash
cd models_ml
python3 -m venv venv
source venv/bin/activate
pip install scikit-learn pandas numpy scipy
python models.py             # RF 학습 + transparency_model.pkl 저장
python models_field_base.py  # CSV 데이터셋 필드 유효성 검증
```

---

## 🛠️ 기술 스택

| 영역 | 기술 |
|---|---|
| 백엔드 | Python 3.11, FastAPI, uvicorn |
| ML / 데이터 | scikit-learn, pandas, numpy |
| 프론트엔드 | React 19, TypeScript, Vite |
| UI | Tailwind CSS 4, shadcn/ui, Radix UI, Lucide React |
| 컨테이너 | Docker, Docker Compose |

---

## 🤖 AI 사용 및 출처 공개

### 사용한 AI 도구
- **OpenAI ChatGPT**: 코드 리팩토링, 로직 트러블슈팅, 문서 초안 작성, 정규식 패턴 개선
- **GitHub Copilot**: `backend/main.py`의 파일 목록 헬퍼 메서드 일부 보조

### AI 활용 목적
- 개발 효율 향상 및 대안적 접근법 탐색
- 온타리오 2026 요건 기반 규칙 피처 브레인스토밍
- 하이브리드 규칙+회귀 모델 로직 및 흐름 개선
- `classify_posting.py` 초기 버전 이슈 식별
- 급여 범위 및 필수 필드 추출 정규식 패턴 개선
- 테스트 케이스 엣지 케이스 제안

### 인간 감독 (Human Oversight)
모든 코드, 로직, 모델 동작은 codeXperts 팀이 직접 작성·검증·테스트했습니다.  
AI 지원은 선택적 입력으로만 활용되었으며, 모든 출력은 통합 전 대폭 수정되었습니다.  
완전히 AI가 생성한 코드 모듈은 사용되지 않았습니다.

### 규정 준수 공개
Working for Workers Four Act, 2024 (S.O. 2024, c.3 – Bill 149)에 따라 AI 사용을 전면 공개합니다.  
AI 도구는 개발 및 문서화 단계에서만 사용되었으며, 구인공고 평가 워크플로우 내 자동화된 의사결정에는 참여하지 않습니다.

---

## 📚 참고 문헌

- Working for Workers Four Act, 2024 (S.O. 2024, c.3 – Bill 149)
- SEC 2025 – Problem Brief: 투명성 요건, 필수 필드, 준수 기대치 정의
- SEC 2025 – Opening Briefing: 시스템 과제, 기대치, 챌린지 컨텍스트
- SEC 2025 – FAQ & Rules: 심사 기준, 허용 도구, AI 사용 공개 요건
- SEC 2025 Job Postings Dataset (`dataset/`)
- Python 라이브러리: scikit-learn, numpy, pandas, FastAPI, uvicorn
- Frontend 라이브러리: React, Vite, Tailwind CSS, shadcn/ui
