# BNP Paribas — AI-Driven Synthetic Persona Simulator

**Tools:** Python · Streamlit · Azure Prompt Flow · Azure OpenAI (GPT-4) · Azure ML Studio  
**Context:** MSc Data Analytics for Business — KEDGE Business School Hackathon (2025)  
**Team:** Vigneshwari Nalla · Ekta Sharma · Nicolas Vavassori · Juan Sebastian Salamanca Melo · Obinna Chukwu

---

## Overview

A full-stack AI application that generates synthetic customer personas for BNP Paribas Personal Finance. The system allows bank analysts to simulate conversations with realistic AI-driven customer profiles — enabling faster, cheaper market research without relying on real customer data.

**Business problem:** Real consumer panels are costly, slow to build, and often incomplete. Banks need a way to simulate customer behavior before launching financial products.

**Solution:** AI-generated synthetic personas grounded in real macro-economic data (Spanish INE datasets), validated against anonymised BNP Paribas data, and evaluated for human-likeness using a dual-audit scoring system.

---

## Live Demo

The app is built with **Streamlit** and connects to an **Azure ML real-time inference endpoint** powered by **Azure Prompt Flow + GPT-4**.

```
streamlit run app.py
```

> Note: Requires a valid Azure ML endpoint key. The Azure endpoint is hosted on BNP's infrastructure and is not publicly accessible. The app code is fully available for reference.

---

## The 4 Personas

| Persona | Age / Income | Key Traits |
|---|---|---|
| Young Independent Professional | 25–35, €1,000–€2,000 | Single, digital-first, career-focused |
| Young Urban Family | 30–40, €1,000–€2,200 | Couple with 1–2 kids, budget-conscious |
| Mature Independent Adult | 46–55, €1,000–€2,200 | Single, cautious, low-tech preference |
| Family Financial Provider | 45–61, €1,000–€2,500 | Married with children, family-focused |

---

## Architecture

```
User Question
      │
      ▼
Azure Prompt Flow (Multi-node cognitive architecture)
      │
      ├── C1_yp  → young_professionals persona node
      ├── C2_yu  → young_urban persona node
      ├── C3_mi  → mature_independent persona node
      └── C4_fp  → family_providers persona node
              │
              ▼
         Answer Node (GPT-4, JSON-mode)
              │
              ▼
         Evaluator Node (Forensic audit)
              │
              ▼
         Output → Streamlit UI
```

### Technology Stack

| Layer | Technology |
|---|---|
| Orchestration | Azure Prompt Flow |
| LLM | Azure OpenAI (GPT-4) |
| Inference Endpoint | Azure ML Studio (Real-Time) |
| Data Enrichment | Python (pandas) + Spanish INE datasets |
| Frontend | Streamlit |
| Dev Environment | GitHub Codespaces (.devcontainer) |

---

## Dual Evaluation System

Every persona response is scored across two audits:

**Alignment Audit** — Is the response coherent with the persona?
- Voice & Tone Consistency
- Economic/Situational Grounding
- Motivational Coherence
- Behavioral Plausibility
- Absence of LLM Bias
- Contextual Specificity

**Integrity Audit** — Does it sound genuinely human?
- Confidence score (0–1)
- Behavioral Red Flags
- Human Truth Synthesis
- Hallucination Risk rating

---

## Data Enrichment Methodology

Personas are grounded in real macro-economic data to eliminate hallucinations:

- **INE (Instituto Nacional de Estadística):** Filtered by municipality code to extract median income brackets (`renta_media_hogar`)
- **Regional housing data:** Used `precio_alquiler_m2` (rent per m²) to calculate realistic disposable income per profile

---

## How to Run Locally

```bash
# Clone the repo
git clone https://github.com/vigneshwari2408/bnp-paribas-persona-simulator.git
cd bnp-paribas-persona-simulator

# Install dependencies
pip install -r requirements.txt

# Run the app
streamlit run app.py
```

> The app will launch but requires an active Azure ML endpoint key to generate responses. Contact the team for demo access.

---

## Key Learnings

- Azure Prompt Flow enables visual orchestration of complex multi-node LLM pipelines
- Grounding LLM outputs with real statistical data dramatically reduces hallucination
- Dual-audit evaluation (alignment + integrity) is more robust than single-metric validation
- Synthetic personas can reliably substitute real customer panels for early-stage product research

---

## About

**Vigneshwari Nalla** — MSc Data Analytics for Business, KEDGE Business School  
[LinkedIn](https://linkedin.com/in/vigna24) · [Portfolio](https://vigna2408.github.io)
