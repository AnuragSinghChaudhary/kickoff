
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

