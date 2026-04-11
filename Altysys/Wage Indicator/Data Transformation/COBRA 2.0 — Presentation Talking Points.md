# COBRA 2.0 — Platform Modernization & Security Presentation

**Duration:** ~60 minutes (including Q&A)

---

## Agenda & Time Allocation

| #   | Section                                                        | Duration | Source                |
| --- | -------------------------------------------------------------- | -------- | --------------------- |
| 1   | Opening & Context — Why This Transformation                    | 5 min    | Proposal + Meeting    |
| 2   | Our Understanding of the Landscape                             | 5 min    | Proposal Slides 4–5   |
| 3   | Strategic Paths — Version 1 vs Version 2                       | 5 min    | Proposal Slide 6      |
| 4   | Scope — Phase 1 & Phase 2                                      | 7 min    | Proposal Slides 8–13  |
| 5   | Architecture & Tech Stack                                      | 7 min    | Proposal Slides 15–18 |
| 6   | Key Feature Modules (AI, Living Wage, Ancillary)               | 5 min    | Proposal Slides 21–23 |
| 7   | Security Deep-Dive: Threat Modeling & Network                  | 5 min    | Security Doc          |
| 8   | Security Deep-Dive: Auth, Encryption & CI/CD                   | 7 min    | Security Doc          |
| 9   | Security Deep-Dive: Audit, Export Controls & Incident Response | 7 min    | Security Doc          |
| 10  | Timelines & Team Configuration                                 | 5 min    | Proposal Slides 25–31 |
| 11  | Before vs After — The Big Picture                              | 2 min    | Proposal Slide 33     |
| 12  | Q&A                                                            | 10 min   | —                     |

---

## 1. Opening & Context — Why This Transformation (5 min)

**Key talking points:**

- "COBRA is a 25+ year-old system — built on PostgreSQL and CSV files, with data scattered across Dropbox folders and Airflow tables. It covers 180 countries, 26 years of data, down to city-block granularity, on a quarterly cadence."
- "The system has become slow and inflexible due to incremental additions over two decades. Key-person dependencies, 30+ Excel files in Dropbox, manual workflows, and data governance gaps make it fragile."
- "This isn't a cosmetic refresh. COBRA 2.0 is a ground-up rebuild focused on scalability, flexibility, and future-proof architecture — while preserving the institutional knowledge embedded in the current system."
- "This session covers two things: **what we're building** (the platform modernization) and **how we're securing it** (the security & data governance posture). Both are foundational — security isn't a phase, it's embedded from day one."

---

## 2. Our Understanding of the Landscape (5 min)

**Key talking points:**

- "Our assessment is based on 14 flow diagrams and 9 documents provided by WageIndicator. We've mapped the entire ecosystem."
- Cover the data domains: minimum wages, cost of living, living wages, CBAs, salary benchmarks, labour law, gig economy — across 180+ countries and 75+ languages.
- "The language service layer is a major differentiator — consistent question structures allow serving content in 70 languages. COBRA 2.0 preserves and extends this."
- **Current infrastructure realities — be candid:**
  1. COBRA 2003 is the sole platform — single point of failure
  2. 30+ Excel files in Dropbox — ungoverned, unversioned
  3. Key-person dependencies — institutional knowledge locked in individuals
  4. Manual workflows — no automation, no audit trail
  5. Data governance gaps — no systematic access control or traceability
- "The immediate priority is the **CBA & Labour Law database**. Other databases follow in later phases."

---

## 3. Strategic Paths — Version 1 vs Version 2 (5 min)

**Key talking points:**

- "We're presenting two strategic transformation paths — not to complicate, but to give WageIndicator a real choice based on ambition and budget."
- **Version 1 — Rebuild:** Replicate and modernize current functionality on a clean, modern stack. Fix the infrastructure debt. Get to a stable, maintainable, governed platform.
- **Version 2 — Rebuild + Innovate:** Everything in V1, plus AI-powered annotation, automated data pipelines, Python-based living wage automation, and advanced data engineering capabilities.
- "Both versions converge on the same unified future architecture. V2 gets there faster and with more capability — but V1 is a solid foundation that V2 features can be layered onto later."
- "The architecture is designed so you're never locked into one path. V1 can evolve into V2 without rework."

---

## 4. Scope — Phase 1 & Phase 2 (7 min)

### Phase 1

- Core modules:
  - **COBRA Core** — the foundation: data models, admin, multi-language support
  - **Labour Law module** — structured data entry, versioning, publishing
  - **CBA Processing** — ingestion, parsing, structured extraction
  - **Migration engine** — data migration from legacy COBRA with validation
  - **Annotation system** — human annotation workflow (V2 adds AI annotation)
  - **Export system** — tiered data export with controls
  - **Translation support** — multilingual content management
  - **AI Annotation (V2 only)** — LLM-powered extraction with human-in-the-loop
- "Phase 1 delivers a working replacement for the core CBA and Labour Law workflows."

### Phase 2

- Extensions:
  - **Ancillary Data management** — web forms, versioning, governance, dependency engine
  - **Survey Configuration** — survey setup and management
  - **Living Wage module** — V1: docs + QA; V2: Python-based automated QA + mapping
  - **Unified API** — single API gateway for all data consumers
  - **Monitoring & Observability** — Prometheus, alerting, dashboards
  - **ETL Pipelines** — Airflow-based data transformation
  - **KoBoToolbox Integration** — field data collection integration
  - **Documentation** — technical and operational documentation

### Out of Scope — state clearly

- Plone CMS replacement, website redesign, salary survey logic, cloud provider selection, historical backfilling (beyond agreed scope), KoBoToolbox country deployments, Living Tariff rebuild, mobile app, full-scale AI
- "These are explicitly excluded — not forgotten. Some may become Phase 3 candidates."

### Assumptions

- WageIndicator provides data access, SME availability, coding frames, sample data, and script access
- Infrastructure provisioning is a joint responsibility
- LLM provider decisions are made collaboratively

---

## 5. Architecture & Tech Stack (7 min)

**Three architectural principles:**

1. **API-first** — every interaction goes through well-defined APIs. No direct DB access from frontend or external consumers.
2. **Cloud-agnostic** — runs on any Kubernetes cluster. No vendor lock-in. Aligned with WageIndicator's no-US-vendor policy.
3. **Audit-first** — every data mutation is logged before it's committed. Auditability is a first-class concern, not an afterthought.

**Tech stack walkthrough:**

| Layer          | Technology           | Why                                                                                  |
| -------------- | -------------------- | ------------------------------------------------------------------------------------ |
| Backend / API  | Django (Python)      | Mature, secure, excellent ORM, rich ecosystem for data-heavy apps                    |
| Frontend       | React                | Component-based, strong ecosystem, accessible                                        |
| Database       | PostgreSQL           | Battle-tested for complex queries, JSONB for flexible schemas, strong data integrity |
| Workflow / ETL | Apache Airflow       | Industry standard for data pipeline orchestration, DAG-based, observable             |
| Search         | Elasticsearch        | Full-text search across multilingual content, fast aggregation                       |
| Caching        | In-memory cache      | High-throughput caching layer (specific engine finalized in Discovery)                |
| Monitoring     | Prometheus + Grafana | Open-source, Kubernetes-native observability                                         |
| Analytics      | Metabase             | Self-hosted BI dashboards for WageIndicator team                                     |
| Infrastructure | Docker / Kubernetes  | Container orchestration, scaling, self-healing                                       |

**Cloud infrastructure context:**

- Single-region EU deployment — no multi-region needed
- Strict no-US-vendor policy — European provider: OVHcloud
- Self-hosted open source stack: K8s, MinIO, GitLab, Nextcloud, Airflow
- Data is non-PII / summary in nature — but governance is still critical for commercial data distribution
- Phased migration — project-by-project, not big-bang

---

## 6. Key Feature Modules (5 min)

### COBRA Engine Evolution

- Walk through legacy → V1 → V2 comparison: "Each version represents a step-change, not just incremental improvement."

### AI Annotation Pipeline (V2)

- Five-step pipeline: Ingestion → Embedding → LLM extraction → Confidence scoring → Human-in-the-loop review
- "The AI doesn't replace annotators — it gives them a pre-filled starting point. Confidence scores tell the human annotator where to focus attention."
- "This is where V2 delivers real productivity gains. CBA processing that takes hours can be reduced to minutes with human verification."

### Ancillary File System

- Web-based forms replace Excel/Dropbox workflows
- Versioning, governance, and a dependency engine — "when a minimum wage changes, the system knows which downstream calculations are affected."

### Living Wage Automation

- V1: Document-based with manual QA
- V2: Python-based automated calculation, automated QA, geographic mapping
- "This is WageIndicator's flagship research product — automating it reduces errors and speeds up the quarterly publication cycle."

---

## 7. Security Deep-Dive: Threat Modeling & Network (5 min)

### Threat Modeling — STRIDE

- "Security in COBRA 2.0 isn't reactive. We use STRIDE — a structured framework to identify threats before code is written."
- Applied at two checkpoints: Discovery & Design (Weeks 1–2) and UAT / Pre-Production
- Highlight 2 concrete examples:
  - **Tampering:** "What if someone modifies wage data or deletes audit entries? → Append-only audit tables. The application cannot delete its own records."
  - **Elevation of Privilege:** "What if an Annotator escalates to Admin? → Permissions enforced server-side. The backend validates every request regardless of frontend state."
- "The threat register is a living document reviewed every sprint."

### Network Security & DB Isolation

- "The database is never directly accessible from the internet. Period."
- Walk through the layered architecture:
  - Public → Reverse Proxy (WAF, rate limiting, TLS) → Internal network → FastAPI / Airflow → Private subnet → PostgreSQL / Elasticsearch
  - K8s NetworkPolicy restricts DB ingress to labeled app pods only
  - No direct SSH — admin only via bastion host with MFA + audit logging
- "Even if someone compromises the web layer, the database is on a separate network segment."

---

## 8. Security Deep-Dive: Auth, Encryption & CI/CD (7 min)

### Authentication — three mechanisms for three user types

1. **WageIndicator staff:** Session auth + MFA. Short session TTLs (30 min idle, 8 hr absolute).
2. **External API consumers:** API keys hashed with SHA-256 (plaintext never stored). Each key scoped to specific datasets, countries, rate limits.
3. **Internal service-to-service:** Short-lived JWTs (5-min TTL), asymmetrically signed. Even internal services don't get permanent credentials.

### Authorization — this is where WageIndicator's control lives

- **RBAC:** Six defined roles — Admin, Data Manager, Annotator, Reviewer, API Consumer, Read-Only Viewer
- **Module-scoped:** Access to CBA ≠ access to Labour Law
- **Country-scoped:** Regional partners restricted to assigned geographies at the query layer
- **Action-level:** View, edit, approve, export, delete are independent permissions
- **Server-side enforcement only:** Backend validates every request. Frontend hides buttons for UX — the backend is the enforcement boundary.

### Encryption

- TLS 1.3 external, mTLS internal (pod-to-pod)
- AES-256 at rest for Postgres, encrypted backups, Vault-managed secrets
- "No stage where data sits unencrypted."

### CI/CD Security Gates

- Six automated gates — four are hard blockers:
  - SAST, dependency scanning, container image scan, secret detection — all block deployment
  - DAST — advisory, triaged within sprint
  - STRIDE review at UAT — blocks go-live
- "Code with security issues cannot ship. It's not a judgment call — it's automated enforcement."

---

## 9. Security Deep-Dive: Audit, Export Controls & Incident Response (7 min)

### Audit Logging

- Every mutation, access event, and admin action is logged: who, what, when, where, which record, payload hash for tamper detection
- Application DB user has INSERT-only on audit table — no UPDATE, no DELETE
- Archived to encrypted storage after 90 days with checksum verification
- "If the logs stop flowing, an alert fires. We detect tampering _and_ suppression."

### Export & Data Distribution Controls — the commercial control layer

- **Tiered data access:** Public tier = country summaries. Premium = city-level detail. Platform enforces per consumer.
- **Field-level filtering:** Show/hide specific fields per API key. Government sees full detail; commercial consumer sees aggregates.
- **Rate limiting:** Two layers — proxy and application. Double enforcement.
- **Bulk export approval (maker-checker):** Large exports require second-person approval. No unilateral extraction.
- **Watermarking & leak tracing:** Every export tagged (export ID, consumer ID, timestamp). Row ordering permuted per consumer. Leaks are traceable to the exact consumer and event.
- **Instant key revocation:** One action, takes effect on next request.

### Incident Response

- Automated alerting: 403 spikes, unusual export volumes, login failures, unexpected geolocations
- Documented runbooks: compromised key, suspected leak, unauthorized access
- Encrypted backups tested quarterly with restore drills

---

## 10. Timelines & Team Configuration (5 min)

### Timelines

| Phase     | Version 1    | Version 2       |
| --------- | ------------ | --------------- |
| Phase 1   | 3 months     | 5.5 months      |
| Phase 2   | 4 months     | 6 months        |
| **Total** | **7 months** | **11.5 months** |

- "V1 gets you to a stable, governed platform in 7 months. V2 adds AI and automation capabilities in 11.5 months."
- Phases overlap intentionally — as Phase 1 stabilizes, Phase 2 ramps up.

### Team Configuration

|                 | Version 1                                              | Version 2                     |
| --------------- | ------------------------------------------------------ | ----------------------------- |
| **Total FTE**   | 4.75                                                   | 7.0                           |
| Core roles      | Tech Lead, Backend, Frontend, QA, UX, Delivery Manager | Same as V1                    |
| Additional (V2) | —                                                      | AI/ML Engineer, Data Engineer |

- "V2 adds dedicated AI/ML and data engineering capacity — that's what enables the annotation pipeline and living wage automation."
- Managed delivery model: Altysys owns end-to-end execution with defined sprint cadence and stakeholder checkpoints.

---

## 11. Before vs After — The Big Picture (2 min)

Walk through transformations — make it tangible:

| Area                | Before (COBRA Legacy)            | After (COBRA 2.0)                                        |
| ------------------- | -------------------------------- | -------------------------------------------------------- |
| **Annotation**      | Manual, paper/Excel-based        | Structured workflows (V1), AI-assisted (V2)              |
| **Labour Law**      | Static documents, manual updates | Versioned, structured, searchable                        |
| **Files**           | 30+ Excel files in Dropbox       | Web-based forms, versioned, governed, dependency-tracked |
| **Surveys**         | Manual configuration             | Configurable survey system                               |
| **Living Wage**     | Manual calculation + manual QA   | Document-based QA (V1), automated Python pipelines (V2)  |
| **Knowledge**       | Locked in individuals            | Documented, systemized, auditable                        |
| **Access Control**  | Ad-hoc                           | Role-based, module-scoped, country-scoped, action-level  |
| **Data Governance** | None                             | Full audit trail, export controls, tiered distribution   |

- "The goal isn't just new technology — it's moving from a system that depends on people remembering things, to a platform that enforces governance automatically."

**Closing statement:**

"COBRA 2.0 gives WageIndicator three things: a modern, maintainable platform; full control over who accesses what; and a foundation that can evolve with AI and automation without rework. WageIndicator becomes the gatekeeper — not just a user of the system."

---

## 12. Q&A (10 min)

### Anticipated Questions

| Likely Question                               | Prepared Response                                                                                                  |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| "Why Django over Node or Go?"                 | Mature ORM, strong admin framework, excellent for data-heavy applications, large Python/AI ecosystem for V2        |
| "Can we start with V1 and upgrade to V2?"     | Yes — architecturally designed for this. V2 capabilities layer on without rework.                                  |
| "What about the Plone CMS?"                   | Explicitly out of scope. Can be Phase 3 if desired. Current focus is CBA & Labour Law.                             |
| "How do we handle the migration from legacy?" | Dedicated migration engine with validation. Phased, project-by-project — not big-bang.                             |
| "What if we want to change cloud providers?"  | Cloud-agnostic architecture (K8s + Docker). No vendor lock-in. Can move between any EU provider.                   |
| "How do we prove compliance to regulators?"   | Immutable audit trail, export traceability, encryption posture — all searchable and exportable.                    |
| "What about GDPR?"                            | EU-only infra, no US vendors, data minimization via field filtering, audit trail for data subject access requests. |
| "Can partners be restricted by geography?"    | Yes — country-scoped permissions enforced at the database query layer.                                             |
| "What happens if an API key is compromised?"  | Instant revocation — one action, takes effect on the next request. Full audit trail available for forensic review. |

---

## Presenter Notes

- **Narrative arc:** Start with the problem (legacy pain), move to the solution (what we're building), then demonstrate control (security & governance). End with the transformation picture.
- **Pacing:** Sections 4 (Scope) and 8–9 (Security Auth + Audit/Export) are the heaviest. If running long, compress Section 6 (Feature Modules) — the slides carry that content.
- **Audience read:** If the room is more business than technical, spend less time on network diagrams and CI/CD, more time on Before/After, access control, and export controls.
- **Visuals to prepare:** Network architecture diagram, AI annotation pipeline flow, timeline gantt, before/after comparison table.
- **Leave-behinds:** Share the proposal deck (V03), plus both versions of the security document — V1 for their technical team, V2 for business stakeholders.
- **Sensitive items:** Do not discuss specific commercials/pricing in this session unless the audience is pre-cleared. The deck has a Commercials section — handle it separately if needed.
