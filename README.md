# Job Posting Validity Checker
### 🥇 1st Place — SEC 2025 Hackathon · Team codeXperts

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

A full-stack web application that automatically validates job postings against Ontario's **2026 Job Posting Transparency Act**. Submit a raw posting or fill in a structured form and get an instant **VALID / INVALID** verdict — with a transparency score, confidence level, and plain-English explanation of every violation found.

---

## Highlights

- 🏆 **1st Place** out of all competing teams at SEC 2025
- 🤖 **Hybrid ML pipeline** — rule-based hard checks + Logistic Regression classifier + Random Forest transparency scorer
- 📋 **Dual input modes** — structured form or raw text paste
- ⚖️ **Legally grounded** — built directly on Ontario's 2026 Job Posting Transparency Act requirements
- 🐳 **One-command deploy** via Docker Compose

---

## Team

### Minsik Kim — Backend & Machine Learning
Designed and built the FastAPI backend and all ML logic. Developed a **hybrid rule-based + Logistic Regression classifier** that first enforces hard compliance rules (missing fields, salary range limits, AI disclosure, Canadian-experience clauses), then falls back to a trained model when no hard violations are found. Also built a separate **Random Forest transparency scoring model** using TF-IDF and numeric features to rate overall posting quality (~78% accuracy). Both models were trained with scikit-learn on a structured job postings dataset.

### Tan Dat — Frontend & DevOps
Developed the frontend application and integrated it with the backend APIs. Implemented both the form-based and text-based submission flows. Containerized the entire stack using **Docker** and configured **Docker Compose** for seamless multi-service orchestration, enabling one-command deployment.

### Khai Ngo — UI/UX Design
Designed and built the full user interface using React, Tailwind CSS, and shadcn/ui. Created the tabbed layout, input components, and a result panel that surfaces classification verdict, confidence percentage, transparency score, and a color-coded breakdown of any missing or non-compliant fields — all in a clean, accessible design.

---

## How It Works
User submits a job posting (form or raw text)
↓
Rules Engine — checks required fields, salary range, AI disclosure, prohibited clauses
↓
If hard violations found → INVALID immediately
↓
If no hard violations → ML Classifier scores transparency
↓
Result — VALID / INVALID · Confidence % · Transparency Score · Missing Fields

### Rules Engine — Hard Compliance Checks
The rules engine runs first and catches automatic disqualifiers under the Act:
| Rule | What It Checks |
|---|---|
| Required fields | Job title, compensation range, employer info, location |
| Salary range | Min/max must be within legal limits; no misleading ranges |
| AI disclosure | Must disclose if AI tools are used in hiring/screening |
| Canadian experience | Cannot require Canadian work experience unless legally exempt |
| Employment type | Must explicitly state full-time/part-time/contract |
### ML Pipeline — Transparency Scoring
When no hard violations are found, two trained models evaluate the posting quality:
- **Logistic Regression** (text classifier) — trained on labeled job postings using TF-IDF vectorization; determines overall validity from language patterns
- **Random Forest** (transparency scorer) — combines TF-IDF text features with numeric metadata to generate a 0–100 transparency score (~78% accuracy)
Both models were trained with scikit-learn, serialized with `pickle`, and served via FastAPI.
---
**Two input modes:**
- **Form** — fill in structured fields (title, salary, location, employer, employment type, AI usage, etc.)
- **Text** — paste a raw job posting and let the model parse and evaluate it
---
## Tech Stack
| Layer | Technologies |
|---|---|
| Backend | Python, FastAPI, scikit-learn, pandas, numpy |
| ML Models | Logistic Regression (text classifier), Random Forest (transparency scorer), TF-IDF |
| Frontend | React 19, TypeScript, Vite, Tailwind CSS, shadcn/ui |
| DevOps | Docker, Docker Compose |
---
## Quick Start
**Docker — one command (recommended)**
```bash
docker compose up --build
Frontend → http://localhost:5173 · API → http://localhost:8000

Manual setup

# Backend
cd backend
pip install -r requirements.txt
uvicorn main:app --reload

# Frontend
cd frontend
npm install && npm run dev
```

AI Usage Disclosure
OpenAI ChatGPT and GitHub Copilot were used to assist with code refactoring, debugging, regex refinement, and documentation drafting. All AI-generated suggestions were manually reviewed and significantly edited before integration. No fully AI-generated code modules were used.

In accordance with the Working for Workers Four Act, 2024 (S.O. 2024, c.3 – Bill 149), the use of AI tools in this project is fully disclosed. AI did not participate in any automated decision-making within the job-posting evaluation workflow itself.
