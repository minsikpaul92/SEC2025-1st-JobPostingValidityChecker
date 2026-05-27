# 🥇 SEC 2025 Hackathon - 1st Place Winner
# Job Posting Validity Checker

**Team name:** codeXperts  
**Project title:** Job Posting Validity Checker

---

## 👥 Team Members & Contributions

### Minsik Kim — Backend · Scikit-learn · ML Logic
- Designed and implemented the FastAPI backend server (`backend/main.py`, `backend/models.py`)
- Built the hybrid rule-based + machine learning text classifier (`model_textbase/classify_posting.py`, `backend/textbase_classifier_loader.py`)
- Trained and serialized a Scikit-learn LogisticRegression model (`textbase_classifier.pkl`)
- Developed the RandomForest transparency scoring model (`models_ml/models.py`, `transparency_model.pkl`)
- Engineered TF-IDF + numeric features and designed Ontario 2026 compliance rules
- Implemented field validation utility (`models_ml/models_field_base.py`)

### Tan Dat — Frontend · Docker · Deployment
- Set up the React + Vite frontend project and integrated backend APIs
- Implemented the form-based validation component (`frontend/src/components/form/form.tsx`)
- Implemented the text-area validation component (`frontend/src/components/text-area/text-area.tsx`)
- Configured Docker containers: `backend/Dockerfile`, `frontend/Dockerfile`
- Set up Docker Compose multi-service orchestration (`docker-compose.yml`)
- Configured the development environment and deployment pipeline

### Khai Ngo — Frontend · UI/UX
- Designed the overall UI/UX and user experience flow
- Implemented the result display component (`frontend/src/components/result/result.tsx`)
- Implemented the header component and tabbed interface (`frontend/src/components/header/header.tsx`)
- Built the component system using shadcn/ui + Tailwind CSS
- Created validation result visualizations (confidence, transparency score, missing fields)
- Designed responsive layout and color-coded VALID/INVALID status indicators

---

## 📌 Project Overview

A web application that automatically validates job postings against Ontario's 2026 Job Posting Transparency requirements (Working for Workers Four Act, 2024).

### Key Features
- **Form-based validation**: Validate by filling in 9 structured fields
- **Text-based validation**: Paste raw posting text for rule + ML analysis
- **Transparency score**: RandomForest model evaluates posting transparency from 0–100%
- **Violation details**: Clearly lists missing fields and reasons for non-compliance

---

## 🏗️ System Architecture

```
User Interface (React + Vite + Tailwind)
  ├── Form Tab   → fill 9 fields       → POST /jobs-postings/field-base
  └── Text Tab   → paste raw text      → POST /jobs-postings/text-base
                          ↓
              FastAPI Backend (backend/main.py)
                  ├── /field-base: missing field check + RF transparency score
                  └── /text-base:  rule-based check + LogisticRegression classification
                          ↓
              Result Display (result.tsx)
                  ├── Classification (VALID / INVALID)
                  ├── Confidence (%)
                  ├── Transparency Score (%)
                  └── Missing Fields list
```

---

## 📁 Project Structure

```
SEC2025-1st-JobPostingValidityChecker/
├── backend/                          # FastAPI backend service
│   ├── main.py                       # API endpoints (3 routes)
│   ├── models.py                     # Pydantic data models
│   ├── textbase_classifier_loader.py # Text classifier loader + rule extraction
│   ├── textbase_classifier.pkl       # Trained LogisticRegression model
│   ├── transparency_model.pkl        # Trained RandomForest transparency model
│   ├── requirements.txt              # Backend dependencies
│   └── Dockerfile                    # Docker config for backend
├── frontend/                         # React + Vite + Tailwind UI
│   ├── src/
│   │   ├── App.tsx                   # Root component with tabbed interface
│   │   ├── components/
│   │   │   ├── form/form.tsx         # Form-based validation input
│   │   │   ├── text-area/text-area.tsx # Text-based validation input
│   │   │   ├── result/result.tsx     # Result display component
│   │   │   ├── header/header.tsx     # Header with Canada flag
│   │   │   └── ui/                   # Shared shadcn/ui components
│   │   └── lib/
│   │       ├── validation.ts         # ValidationResult type definition
│   │       └── utils.ts              # Utility functions
│   ├── package.json
│   ├── vite.config.ts
│   ├── tsconfig.json
│   ├── Dockerfile                    # Docker config for frontend
│   └── index.html
├── model_textbase/                   # Rule-first text classifier
│   ├── classify_posting.py           # PostingClassifier class (rule + LR hybrid)
│   ├── textbase_classifier.pkl       # Pre-trained model
│   └── dataset/
│       ├── job_postings_dataset.csv  # Structured dataset
│       ├── raw_postings/             # 10 valid + 10 invalid sample postings
│       └── test_postings/            # 10 test postings for interactive testing
├── models_ml/                        # ML transparency scoring experiments
│   ├── models.py                     # RandomForest transparency model training
│   ├── models_field_base.py          # Field validation utility
│   └── transparency_model.pkl        # Trained RandomForest model
├── dataset/                          # Shared data reference
├── docker-compose.yml                # Multi-container orchestration
└── README.md
```

---

## 🔑 Key Technical Implementations

### 1. Hybrid Rule + ML Model (`model_textbase/classify_posting.py`)
- **Hard rules first**: Missing required fields, salary range width over $50k, undisclosed AI use, explicit Canadian-experience requirements all force an `INVALID` result immediately
- **ML fallback**: If no hard rules are violated, a balanced `LogisticRegression` trained on rule-derived features makes the final classification
- Returns specific violation reasons for each failed check

### 2. Backend Endpoints (`backend/main.py`)
| Endpoint | Method | Description |
|---|---|---|
| `/jobs-postings/` | GET | Returns sample posting texts grouped by filename |
| `/jobs-postings/text-base` | POST | Classifies raw text (rules + LogisticRegression) |
| `/jobs-postings/field-base` | POST | Validates fields + computes RF transparency score |

### 3. ML Transparency Model (`models_ml/models.py`)
- TF-IDF (100 features) + numeric features (field completeness, employment type, AI disclosure, salary presence)
- RandomForest classifier predicts transparency label (1 = all fields present, 0 = fields missing)
- 70/30 train/evaluation split; saved as `transparency_model.pkl`

### 4. Frontend (`frontend/src/`)
- React 19 + TypeScript + Tailwind CSS 4 + shadcn/ui
- **Form tab**: 9-field input (title, salary, location, employer, description, requirements, benefits, employment_type, ai_used)
- **Text tab**: Paste raw posting text for instant analysis
- **Results**: VALID/INVALID badge, confidence %, transparency score %, color-coded missing field list

---

## 🚀 How to Run

### Option 1: Docker Compose (Recommended)

```bash
docker compose up --build
```

- Frontend: http://localhost:5173
- Backend: http://localhost:8000

---

### Option 2: Manual Setup

#### Prerequisites
- Python 3.11+
- Node.js 18+

#### Backend (FastAPI)
```bash
cd backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload
# → http://localhost:8000
```

#### Frontend (React + Vite)
```bash
cd frontend
npm install
npm run dev
# → http://localhost:5173
```

#### Text Classifier (standalone)
```bash
cd model_textbase
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python classify_posting.py
# → Enter a test index (1–10) or path to any .txt file
```

#### Train ML Transparency Model
```bash
cd models_ml
python3 -m venv venv
source venv/bin/activate
pip install scikit-learn pandas numpy scipy
python models.py             # trains RandomForest, saves transparency_model.pkl
python models_field_base.py  # validates required fields across the CSV dataset
```

---

## 🛠️ Tech Stack

| Area | Technologies |
|---|---|
| Backend | Python 3.11, FastAPI, uvicorn |
| ML / Data | scikit-learn, pandas, numpy |
| Frontend | React 19, TypeScript, Vite |
| UI | Tailwind CSS 4, shadcn/ui, Radix UI, Lucide React |
| Containers | Docker, Docker Compose |

---

## 🤖 AI Usage & Citation Statement

### AI Tools Used
This project used **OpenAI ChatGPT** and **GitHub Copilot** to support development tasks such as code refactoring, feature brainstorming, logic troubleshooting, debugging assistance, and documentation drafting. All AI-generated suggestions were manually reviewed, validated, and integrated by the development team.

### Purpose of AI Assistance
AI tools were used to:
- Improve development efficiency and explore alternative solution approaches
- Brainstorm rule-based features aligned with Ontario's 2026 Job Posting Transparency requirements
- Refine the logic and flow of the hybrid rule–plus–logistic-regression model
- Identify issues in early iterations of `classify_posting.py`
- Enhance regex patterns for extracting salary ranges and required fields
- Produce and revise explanatory documentation (README sections, comments)
- Clarify edge cases and suggest additional test cases for `dataset/test_postings/`

### Human Oversight
All code, logic, and model behavior were written, validated, and tested by the codeXperts team.
AI assistance was treated strictly as optional input, and all outputs were significantly edited before integration.
No fully-generated code modules were used.

### Specific AI Usage Notes
- **ChatGPT** assisted with conceptual explanations, reasoning tasks, and iterative improvement of transparency-validation logic.
- **GitHub Copilot** assisted minimally, specifically with a helper method in `backend/main.py` to list posting files (documented in-code).

### Compliance Disclosure
In accordance with the **Working for Workers Four Act, 2024 (S.O. 2024, c.3 – Bill 149)**, this project fully discloses the use of AI in its development.
AI tools were used only during development and documentation. They do not participate in automated decision-making within the job-posting evaluation workflow.

---

## 📚 References

- Working for Workers Four Act, 2024 (S.O. 2024, c.3 – Bill 149)
- SEC 2025 – Problem Brief: Defines transparency requirements, required posting fields, and compliance expectations
- SEC 2025 – Opening Briefing: System tasks, expectations, and challenge context
- SEC 2025 – FAQ & Rules: Judging criteria, allowed tools, and AI-usage disclosure requirements
- SEC 2025 Job Postings Dataset (`dataset/job_postings_dataset.csv`, `dataset/raw_postings/`, `dataset/test_postings/`)
- Python libraries: scikit-learn, numpy, pandas, FastAPI, uvicorn
- Frontend libraries: React, Vite, Tailwind CSS, shadcn/ui
