# Job Posting Validity Checker
### 🥇 1st Place — SEC 2025 Hackathon

A web application that automatically validates job postings for compliance with Ontario's 2026 Job Posting Transparency Act. Paste a raw posting or fill in a form — get an instant VALID / INVALID verdict with a transparency score and a plain-English explanation of any violations.

---

## Team — codeXperts

| Member | Role | Contributions |
|---|---|---|
| **Minsik Kim** | Backend & ML | Built the FastAPI backend and all machine learning logic — a hybrid rule-based + Logistic Regression text classifier and a Random Forest transparency scoring model trained with scikit-learn |
| **Tan Dat** | Frontend & DevOps | Developed the frontend application and connected it to the backend API; set up Docker containerization and the full deployment pipeline |
| **Khai Ngo** | UI/UX | Designed and implemented the user interface — tabbed layout, form and text-input modes, and color-coded result display |

---

## How It Works

1. **Submit** a job posting — either as raw text or via a structured form
2. **Rules engine** checks for required fields, salary range limits, AI disclosure, and other Ontario 2026 requirements
3. **ML model** scores overall transparency if no hard violations are found
4. **Results** show the verdict (VALID / INVALID), confidence %, transparency score, and any missing fields

---

## Tech Stack

| Layer | Technologies |
|---|---|
| Backend | Python · FastAPI · scikit-learn · pandas |
| Frontend | React · TypeScript · Vite · Tailwind CSS |
| DevOps | Docker · Docker Compose |

---

## Quick Start

**Docker (recommended)**
```bash
docker compose up --build
```
Frontend → http://localhost:5173 · Backend → http://localhost:8000

**Manual**
```bash
# Backend
cd backend && pip install -r requirements.txt
uvicorn main:app --reload

# Frontend
cd frontend && npm install && npm run dev
```

---

## AI Usage Disclosure

OpenAI ChatGPT and GitHub Copilot were used to assist with code refactoring, debugging, and documentation. All AI-generated suggestions were reviewed and validated by the team before integration. No fully AI-generated modules were used.

In accordance with the **Working for Workers Four Act, 2024 (S.O. 2024, c.3 – Bill 149)**, AI use in this project is fully disclosed. AI tools did not participate in any automated decision-making within the evaluation workflow.
