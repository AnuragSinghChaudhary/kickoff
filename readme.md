
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


------------------------------------------------------------

# 🔧 Module 2: Tech Stack Proposal (Updated for 2025 Brief)

### 🎯 Goal
Define a compliant, observable, scalable, and developer-friendly stack to support ExecAI's architecture and GDPR/AI Act obligations.

---

## 🧑‍💻 Frontend
| Layer     | Tech          | Rationale |
|-----------|---------------|-----------|
| Framework | **Next.js**   | Server-side rendering, fast routing, React ecosystem |
| Styling   | **Tailwind CSS** | Fast, customizable, responsive styling |
| State Mgmt| **Zustand** or **Redux Toolkit** | Simple yet powerful local state |
| Realtime  | **Socket.IO** or **Pusher** | For live feedback and task updates |

---

## 🔙 Backend & API Layer
| Layer         | Tech             | Rationale |
|---------------|------------------|-----------|
| Framework     | **FastAPI** (Python) | Async-ready, great for LLM pipelines |
| Job Queue     | **Celery + Redis**   | Reliable async task queue |
| API Gateway   | **Kong Gateway**     | Rate limiting, JWT, plug-ins |
| AuthN/AuthZ   | **Auth0 (EU region)** or **Keycloak** | Secure OAuth2 flows + RBAC |

---

## 🧠 LLM Orchestration
| Component       | Tech               | Rationale |
|------------------|--------------------|-----------|
| Prompt chaining  | **LangChain**      | Mature, modular LLM pipeline |
| Context engine   | **Qdrant** / **Weaviate** (EU-hosted) | GDPR-compliant vector DB |
| Primary model    | **Mistral 7B** or **Azure OpenAI (EU)** | Compliant + performant |
| Fallback model   | **OpenAI GPT-4 via DPA** | For edge-case coverage |
| Logging/token cost | **PromptLayer** or **Langfuse** | Transparent usage tracking |

---

## 📦 Data Layer
| Type           | Tech              | Rationale |
|----------------|-------------------|-----------|
| Structured data| **PostgreSQL**    | Reliable, ACID, GDPR-friendly |
| Object storage | **MinIO** (EU region) | S3-compatible, self-hosted |
| Logs/metrics   | **Loki + Prometheus + Grafana** | Observability trio |
| Secrets        | **Vault** or **AWS Secrets Manager** | Centralized secret control |

---

## 🚀 CI/CD & DevOps
| Component        | Tool                  | Rationale |
|------------------|------------------------|-----------|
| CI/CD pipeline    | **GitHub Actions**     | Native, integrated, easy |
| Containerization  | **Docker + Helm**      | Portable deployments |
| Infra-as-Code     | **Terraform**          | Cloud-agnostic + audit-ready |
| Deployment target | **Azure (EU)** or **Scaleway** | GDPR & AI Act compliant hosting |

---

## 🔒 Security & Compliance
| Area             | Enforcement                            |
|------------------|----------------------------------------|
| OAuth scopes     | Minimal API access (principle of least privilege) |
| Logging          | Structured logs, no raw PII            |
| Data retention   | TTL for logs and cache (e.g., 30–90d)  |
| DPA fallback     | Explicit consent + routing enforcement |
| Right to erasure | ID-based deletion pipeline in all layers |

---

## 📐 Justification Summary
- All tools chosen support **EU data residency** or can be self-hosted in compliant regions.
- Stack prioritizes **developer velocity**, **LLM flexibility**, and **fine-grained privacy control**.
- Modular, with room to grow from monolith to microservices as scale demands.


