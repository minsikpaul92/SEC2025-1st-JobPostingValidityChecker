# Job Posting Validity Checker
### 🥇 1st Place — SEC 2025 Hackathon · Team codeXperts

A full-stack web application that automatically validates job postings against Ontario's **2026 Job Posting Transparency Act**. Submit a raw posting or fill in a structured form and get an instant **VALID / INVALID** verdict — with a transparency score, confidence level, and plain-English explanation of every violation found.

---

## Team

### Minsik Kim — Backend & Machine Learning
Designed and built the FastAPI backend and all ML logic. Developed a **hybrid rule-based + Logistic Regression classifier** that first enforces hard compliance rules (missing fields, salary range limits, AI disclosure, Canadian-experience clauses), then falls back to a trained model when no hard violations are found. Also built a separate **Random Forest transparency scoring model** using TF-IDF and numeric features to rate overall posting quality. Both models were trained with scikit-learn on a structured job postings dataset.

### Tan Dat — Frontend & DevOps
Developed the frontend application and integrated it with the backend APIs. Implemented both the form-based and text-based submission flows. Containerized the entire stack using **Docker** and configured **Docker Compose** for seamless multi-service orchestration, enabling one-command deployment.

### Khai Ngo — UI/UX Design
Designed and built the full user interface using React, Tailwind CSS, and shadcn/ui. Created the tabbed layout, input components, and a result panel that surfaces classification verdict, confidence percentage, transparency score, and a color-coded breakdown of any missing or non-compliant fields — all in a clean, accessible design.

---

## How It Works

```
User submits a job posting (form or raw text)
         ↓
Rules Engine — checks required fields, salary range, AI disclosure, prohibited clauses
         ↓
ML Model — scores transparency if no hard violations found
         ↓
Result — VALID / INVALID · Confidence % · Transparency Score · Missing Fields
```

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
```
Frontend → http://localhost:5173 · API → http://localhost:8000

**Manual setup**
```bash
# Backend
cd backend
pip install -r requirements.txt
uvicorn main:app --reload

# Frontend
cd frontend
npm install && npm run dev
```

---

## AI Usage Disclosure

OpenAI ChatGPT and GitHub Copilot were used to assist with code refactoring, debugging, regex refinement, and documentation drafting. All AI-generated suggestions were manually reviewed and significantly edited before integration. No fully AI-generated code modules were used.

In accordance with the **Working for Workers Four Act, 2024 (S.O. 2024, c.3 – Bill 149)**, the use of AI tools in this project is fully disclosed. AI did not participate in any automated decision-making within the job-posting evaluation workflow itself.
