
# 🔍 Module 1: ExecAI SaaS Architecture (Updated for 2025 Brief)

### 🎯 **Goal**
Design a GDPR- and AI Act-compliant, scalable LLM-based SaaS architecture for "ExecAI," a digital assistant helping executives manage:
- Emails
- Calendars & tasks
- Meetings
- Dashboards
- Feedback loops (learning system)

---

## 🧱 Core Business & Technical Assumptions
| Parameter                | Value |
|--------------------------|-------|
| Users                    | < 5,000 (Q4 2025 MVP) |
| Budget                   | €500,000 (12 months) |
| LLM Call SLO             | Avg. cost < €0.05 |
| Latency SLO              | p95 < 2 seconds |
| Data Policy              | “Privacy by design” — no client data leaves EEA without DPA |
| Compliance               | GDPR + EU AI Act (high transparency) |

---

## 🧩 Domain Breakdown & Constraints

| Domain          | Feature Summary                                         | Tech Constraints |
|------------------|----------------------------------------------------------|------------------|
| **Email**         | Inbox-zero summary, smart replies, follow-ups           | OAuth: MS 365/Google; EU processing only |
| **Calendar**      | Smart rescheduling, contextual to-dos                   | Google/Outlook APIs; time-blocking logic |
| **Meetings**      | Recording, STT, summaries (pre/post), action items      | Zoom/Meet/Teams integration; STT → Vector → LLM |
| **Command Center**| Dashboard: logs, usage, cost, audit                     | RBAC, OpenTelemetry, encryption at rest |
| **Learning Loop** | Feedback UX (thumbs), privacy sandbox for fine-tuning  | EU-only training, fallback LLM (DPA gated) |

---

## 🧠 System Architecture Overview

```plaintext
[User Devices]
    │
    ▼
[API Gateway] ───▶ [OAuth Auth Layer]
    │
    ▼
[Service Layer: Email / Calendar / Meetings / Feedback / Command]
    │             │           │             │
    │             ▼           ▼             ▼
    │        [External APIs: Google/MS, Zoom] 
    │
    ▼
[LLM Orchestrator] ──▶ [Prompt Builder + Retriever (LangChain)]
    │                          │
    │                          └────▶ [Vector Store (Qdrant EU)]
    │
    ├─▶ [Fine-tuned EU-hosted LLM (e.g., Mistral, Azure EU)]
    └─▶ [Fallback LLM (OpenAI via DPA)]
    ▼
[Output Processor & Cost Monitor]
    │
    ▼
[Client + Logging + Feedback Collector]
```

---

## 🔒 Privacy & Compliance Enforcement

- 🔐 **Data Flow Boundaries**: All PII processed within EEA unless explicitly routed through DPA-covered fallback
- 🧹 **Anonymization**: Prompt layer strips raw email/text identifiers
- 📦 **Retention Policy**: Logs auto-deleted or obfuscated post-90 days
- 🚫 **No Shadow Copying**: No offsite model storage unless fine-tuning opt-in given

---

## ⚙️ Performance & Cost Strategy

| Category     | Strategy |
|--------------|----------|
| **Latency**  | Async STT + background embedding; prefetch data chunks; lightweight summarization |
| **Cost**     | Token-limited LLM usage; Redis caching of summaries; fallback models behind routing logic |
| **Monitoring**| OpenTelemetry + Prometheus (p95, € per call, prompt length tracking) |
