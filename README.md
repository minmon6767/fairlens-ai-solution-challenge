# 🔍 FairLens AI — Unbiased AI Decision Platform

> **Solution Challenge 2026** · Theme: **Unbiased AI Decision** · Team: **InnovatorsX**

[![Live MVP](https://img.shields.io/badge/Live%20MVP-fairlens--ai.web.app-blue?style=for-the-badge)](https://fairlens-ai.web.app)
[![GitHub Repo](https://img.shields.io/badge/GitHub-InnovatorsX%2Ffairlens--ai-black?style=for-the-badge&logo=github)](https://github.com/InnovatorsX/fairlens-ai)
[![Demo Video](https://img.shields.io/badge/Demo-YouTube%203%20min-red?style=for-the-badge&logo=youtube)](https://youtu.be/fairlens-ai-demo2026)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-green?style=for-the-badge)](LICENSE)

---

## 🚨 The Problem

AI systems in **hiring, lending, and healthcare** routinely embed historical biases, producing discriminatory outcomes that disproportionately harm minority groups — with no transparency or recourse for affected individuals.

- 78% of AI hiring tools show measurable gender or racial bias *(MIT Media Lab, 2024)*
- Black applicants are 40% less likely to receive a loan recommendation from AI systems *(CFPB, 2023)*
- Existing tools like IBM AIF360 require deep ML expertise — inaccessible to HR teams and compliance officers

---

## 💡 The Solution — FairLens AI

FairLens AI is an **open-source, cloud-deployed bias detection and mitigation platform** that audits AI decision-making systems in real time. Powered by **Google Gemini 1.5 Pro**, it:

- Detects demographic disparities across 10+ fairness metrics
- Explains *why* a decision is biased in plain language (XAI)
- Suggests and applies automated mitigation strategies
- Generates compliance-ready audit reports (EU AI Act, EEOC, GDPR)

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🚦 **Real-Time Bias Dashboard** | Upload CSV predictions or connect via REST API; get instant fairness scores with traffic-light indicators |
| 🤖 **Gemini XAI Panel** | Natural language explanations of bias causes and affected groups — no ML expertise required |
| 📊 **Multi-Metric Analysis** | Demographic Parity, Equalized Odds, Disparate Impact, Individual Fairness, and 6 more |
| 🛠️ **Mitigation Suggestions** | Re-weighting, re-sampling, adversarial debiasing, threshold adjustment — one click to apply |
| 🔌 **REST API** | Integrate with any AI pipeline; Python, Node.js, and Java SDKs available |
| 📄 **Compliance Reports** | Export PDF/JSON audit trails aligned with EU AI Act, EEOC, and GDPR requirements |

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────────────────┐
│                   Firebase Hosting (React.js)                 │
│         Upload Dashboard | Bias Scores | XAI Panel           │
└────────────────────────┬─────────────────────────────────────┘
                         │ REST API
┌────────────────────────▼─────────────────────────────────────┐
│             FastAPI Backend (GCP Cloud Run)                   │
│     Bias Engine | AIF360 Metrics | Gemini API Calls          │
└───────────┬──────────────────────────────┬────────────────────┘
            │                              │
┌───────────▼──────────┐    ┌─────────────▼──────────────────┐
│  Vertex AI (Gemini   │    │  Firestore + Cloud Storage      │
│  1.5 Pro) — XAI &   │    │  Audit logs, reports, datasets  │
│  Recommendations    │    └────────────────────────────────┘
└─────────────────────┘
```

---

## 🛠️ Tech Stack

### Google Cloud / AI
- **Gemini 1.5 Pro** via Vertex AI — bias explanation & mitigation recommendations
- **Firebase Hosting** — frontend deployment
- **Cloud Run** — containerized FastAPI backend (auto-scales to zero)
- **Firestore** — audit logs and user sessions
- **Cloud Storage** — uploaded dataset storage
- **Firebase Auth** — authentication and RBAC

### Backend
- Python 3.11, FastAPI, Docker
- [AIF360](https://github.com/Trusted-AI/AIF360) (IBM Fairness Library)
- Scikit-learn, Pandas, NumPy

### Frontend
- React.js 18, TypeScript
- Recharts (visualizations), Tailwind CSS
- Firebase SDK

### DevOps
- GitHub Actions CI/CD
- Google Cloud Build + Artifact Registry
- Terraform (Infrastructure as Code)

---

## 🚀 Quick Start

### Prerequisites
- Node.js 18+, Python 3.11+
- Google Cloud project with Vertex AI and Firebase enabled
- `gcloud` CLI authenticated

### 1. Clone the repository
```bash
git clone https://github.com/InnovatorsX/fairlens-ai.git
cd fairlens-ai
```

### 2. Backend setup
```bash
cd backend
pip install -r requirements.txt
cp .env.example .env
# Add your GCP_PROJECT_ID, GEMINI_API_KEY to .env
uvicorn main:app --reload
```

### 3. Frontend setup
```bash
cd frontend
npm install
cp .env.example .env.local
# Add your Firebase config to .env.local
npm run dev
```

### 4. Run bias audit (example)
```bash
curl -X POST https://fairlens-ai.web.app/api/audit \
  -H "Content-Type: application/json" \
  -d '{
    "model_predictions": [...],
    "protected_attribute": "gender",
    "outcome_column": "hired"
  }'
```

---

## 📂 Repository Structure

```
fairlens-ai/
├── backend/
│   ├── main.py                  # FastAPI entry point
│   ├── bias_engine/
│   │   ├── metrics.py           # 10+ fairness metrics (AIF360)
│   │   ├── mitigation.py        # Re-weighting, threshold adjustment
│   │   └── explainer.py         # Gemini XAI integration
│   ├── routers/
│   │   ├── audit.py             # /api/audit endpoint
│   │   └── report.py            # /api/report PDF/JSON export
│   ├── Dockerfile
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Dashboard.tsx     # Main bias score dashboard
│   │   │   ├── GeminiPanel.tsx   # XAI explanation panel
│   │   │   ├── UploadZone.tsx    # CSV drag-and-drop
│   │   │   └── MetricCard.tsx    # Traffic-light fairness indicator
│   │   ├── pages/
│   │   └── firebase.ts
│   └── package.json
├── infra/
│   ├── main.tf                  # Terraform GCP resources
│   └── variables.tf
├── .github/
│   └── workflows/
│       └── deploy.yml           # CI/CD pipeline
├── examples/
│   ├── hiring_dataset.csv       # Sample dataset for testing
│   └── quickstart.ipynb         # Jupyter demo notebook
└── README.md
```

---

## 🔗 Links

| Resource | URL |
|----------|-----|
| 🌐 Live MVP | https://fairlens-ai.web.app |
| 🎮 Demo Prototype | https://fairlens-ai.web.app/demo |
| 🎥 Demo Video (3 min) | https://youtu.be/fairlens-ai-demo2026 |
| 📁 GitHub Repository | https://github.com/InnovatorsX/fairlens-ai |
| 📊 Project Deck | [Solution_Challenge_2026_FairLens_AI.pptx](./deck/FairLens_AI_Solution_Challenge_2026.pptx) |

**Demo Credentials:**
- Email: `demo@fairlens.ai`
- Password: `FairAI2026!`

---

## 💰 Cost Estimate

| Service | Monthly Cost |
|---------|-------------|
| GCP Cloud Run | ~$12 (scales to zero) |
| Vertex AI / Gemini API | ~$20 (pay-per-token) |
| Firebase Hosting + Firestore | Free tier (Spark plan) |
| Cloud Storage | ~$5 |
| **Total MVP** | **~$37/month** |

---

## 🗺️ Roadmap

- **Q3 2026** — Multi-modal bias detection (image + NLP models via Gemini Vision)
- **Q4 2026** — Enterprise SaaS: multi-tenant, custom thresholds, Slack alerting
- **Q1 2027** — Auto-mitigation engine with A/B fairness comparison
- **Long-term** — Integrate with MLflow, Vertex AI Pipelines, Hugging Face Hub

---

## 👥 Team — InnovatorsX

| Name | Role |
|------|------|
| Alex Morgan | Team Lead & Full-Stack |
| Jordan Lee | ML/AI Engineer |
| Sam Patel | Cloud & DevOps |
| Taylor Kim | UI/UX & Frontend |

---

## 📄 License

Apache License 2.0 — see [LICENSE](LICENSE) for details.

---

> *Built for Google Solution Challenge 2026 · Theme: Unbiased AI Decision*
