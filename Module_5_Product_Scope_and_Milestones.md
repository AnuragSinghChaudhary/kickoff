
# 🛠️ Module 5: v1 Product Scope & Milestones (Updated for 2025 Brief)

### 🎯 Goal
Define the MVP scope of ExecAI with clear priorities, dependencies, and a milestone timeline targeting a Q4 2025 pilot release.

---

## ✅ Must-Have Features (MVP)

| Module           | Feature                                       | Notes |
|------------------|-----------------------------------------------|-------|
| Email            | Inbox summary, deadline detection             | Core utility for execs |
| Calendar         | Smart rescheduling, contextual to-dos         | Time-blocking via APIs |
| Meetings         | STT + post-meeting action summaries           | Consent-based recording |
| Command Center   | Admin dashboard: cost, usage, logs            | RBAC required |
| Feedback System  | Thumbs up/down UI + data collection           | Needed for learning loop |
| LLM Core         | Prompt builder + EU LLM orchestration         | Vector-aware summaries |

---

## 🚧 Nice-to-Have Features (Post-MVP)

| Module           | Feature                                       | Justification |
|------------------|-----------------------------------------------|----------------|
| Email            | Smart reply suggestions                       | Improves UX, not critical |
| Meetings         | Pre-meeting briefings                         | Add-on for exec prep |
| Command Center   | Advanced satisfaction/NPS tracking            | Better suited post-scale |
| Learning Loop    | Active fine-tuning trigger workflows          | Needs large dataset |
| Admin Tools      | Granular audit logs, retention config         | Legal support for scale-up |

---

## 🧱 Dependencies Map

| Feature                     | Dependencies |
|-----------------------------|--------------|
| Inbox Summary               | OAuth + Email API |
| Calendar Rescheduling       | OAuth + Calendar API |
| Meeting Summaries           | STT engine + vector DB |
| Feedback Loop               | Frontend UI + prompt mapping |
| Command Center              | Observability stack (logs, metrics) |
| LLM Pipeline                | LangChain + vector store setup |

---

## 📅 Milestone Timeline (2025–2026)

| Month     | Milestone                                       |
|-----------|-------------------------------------------------|
| Month 1   | Kickoff: infra + OAuth working                  |
| Month 2–3 | Email & Calendar modules functional             |
| Month 4   | Meeting STT → Summary pipeline live             |
| Month 5   | LLM orchestrator integrated                     |
| Month 6   | Command Center + basic observability            |
| Month 7   | Feedback loop wired into UI                     |
| Month 8   | Internal testing + privacy audits               |
| Month 9   | Pilot launch (10 clients)                       |
| Month 10  | Feedback iteration sprint                       |
| Month 11  | MVP launch (100 clients, Q4 2025)               |

---

## ✅ Summary

- Feature set focuses on core executive value
- Delivery staged for high output in <12 months
- Feedback loop built in before go-live

