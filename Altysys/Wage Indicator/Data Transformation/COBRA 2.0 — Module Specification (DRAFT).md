# COBRA 2.0 Platform Modernization — Module Specification

### Altysys → WageIndicator

---

> **Status:** DRAFT — Detailed Breakdown
> **Total Modules:** 16 (including Discovery)
> **Total Development Effort:** 576 person-days
> **QA Effort (25% of dev):** 144 person-days
> **Total Estimated Effort:** 720 person-days
> **Estimation Basis:** Indicative · Backend + Frontend split
> **Discovery:** Flat 2 weeks (not included in PD totals)

---

## Module Summary

|  #  | Module                              | Backend (PD) | Frontend (PD) | Total (PD) |  Dependencies  |
| :-: | ----------------------------------- | :----------: | :-----------: | :--------: | :------------: |
|  0  | Discovery & Project Setup           |      —       |       —       |  2 weeks   |       —        |
|  1  | COBRA Core Platform                 |      53      |      28       |     81     |    Module 0    |
|  2  | Labour Law Database                 |      34      |      22       |     56     |    Module 1    |
|  3  | International Law Database          |      14      |       6       |     20     |  Module 1, 2   |
|  4  | CBA Processing Engine               |      36      |      15       |     51     |    Module 1    |
|  5  | AI Annotation Pipeline              |      31      |      14       |     45     |    Module 4    |
|  6  | Pensions Database                   |      17      |       8       |     25     |  Module 1, 10  |
|  7  | Data Migration & Schema Unification |      46      |      10       |     56     | Module 1, 2, 4 |
|  8  | Export & Data Distribution          |      31      |      15       |     46     |  Module 1, 11  |
|  9  | Translation & Multilingual          |      16      |      13       |     29     |    Module 1    |
| 10  | Dynamic Survey / Form Engine        |      30      |      33       |     63     |    Module 1    |
| 11  | Unified API Gateway                 |      22      |       4       |     26     |    Module 1    |
| 12  | LLM Query Interface                 |      26      |       3       |     29     |  Module 1, 11  |
| 13  | Monitoring & Observability          |      15      |       0       |     15     |    Module 0    |
| 14  | Security Hardening                  |      19      |       0       |     19     |    Module 0    |
| 15  | Documentation & Handover            |      12      |       3       |     15     |      All       |
|     | **Dev Subtotal**                    |   **402**    |    **174**    |  **576**   |                |
|     | **QA (25%)**                        |              |               |  **144**   |                |
|     | **Grand Total**                     |              |               |  **720**   |                |

---

## Module Details

---

### Module 0: Discovery & Project Setup

**Purpose:** Establish infrastructure, align on architecture, profile legacy data, and set up the development environment — flat 2-week engagement regardless of team size.

| Sub-Component                        | Notes                                                                                  |
| ------------------------------------ | -------------------------------------------------------------------------------------- |
| Legacy schema audit & data profiling | Map all existing COBRA databases, 30+ Excel files in Dropbox, Airflow table structures |
| Unified schema design                | Design target PostgreSQL schema consolidating all legacy sources into one database     |
| Infrastructure provisioning          | K8s cluster, CI/CD pipelines, staging/prod environments on EU cloud (Hetzner/OVH)      |
| Dev environment setup                | Docker-compose local dev, seed data, onboarding docs                                   |
| STRIDE threat modeling               | First-pass threat register against architecture; mitigations mapped to backlog         |
| LLM provider evaluation              | Test documents against candidate models (Mistral, Dragon LLM, EU alternatives)         |
| Architecture sign-off                | Final tech stack confirmation, ADR documentation, team alignment                       |

**Dependencies:** None — kick-off module
**Risks:** Legacy data access delays; client SME availability; infrastructure provisioning lead times

---

### Module 1: COBRA Core Platform

**Purpose:** Foundation layer — unified database, admin panel, RBAC, audit logging, multi-language framework, and country-scoped access. Every other module builds on this.

| Sub-Component                                  | Backend (PD) | Frontend (PD) | Notes                                                                             |
| ---------------------------------------------- | :----------: | :-----------: | --------------------------------------------------------------------------------- |
| Unified database schema implementation         |      10      |       0       | Single PostgreSQL instance consolidating all legacy separate databases            |
| Core data models (country, language, metadata) |      8       |       0       | 180+ countries, 75+ languages, shared reference data                              |
| Admin panel                                    |      8       |      12       | Django admin customization + React admin UI for non-technical users               |
| User & role management (RBAC)                  |      8       |       5       | 6 roles: Admin, Data Manager, Annotator, Reviewer, API Consumer, Read-Only Viewer |
| Audit logging engine                           |      6       |       3       | Append-only table, no UPDATE/DELETE grants, payload hashing, tamper detection     |
| Country-scoped access control                  |      5       |       3       | Query-layer filtering by user's assigned countries; module-scoped permissions     |
| Multi-language framework                       |      8       |       5       | 70-language service layer, translation key management, locale switching           |
| **Subtotal**                                   |    **53**    |    **28**     |                                                                                   |

**Dependencies:** Module 0 (Discovery)
**Risks:** Unified schema design complexity — 25+ years of legacy structures to consolidate. Multi-language framework must support the existing content serving pattern in 70 languages without regression.

---

### Module 2: Labour Law Database

**Purpose:** Structured data management for national labour law records — data entry, versioning, publishing, and search across 180+ countries.

| Sub-Component                      | Backend (PD) | Frontend (PD) | Notes                                                            |
| ---------------------------------- | :----------: | :-----------: | ---------------------------------------------------------------- |
| Labour law data models             |      5       |       0       | Country-specific fields, temporal validity, legislative metadata |
| Structured data entry UI           |      5       |       8       | Form-based entry with validation, country context switching      |
| Version-controlled records         |      5       |       3       | Full history, diff view, rollback to any version                 |
| Publishing workflow                |      5       |       4       | Draft → Review → Published pipeline with role-based gates        |
| Country-scoped management          |      3       |       2       | Extends core country-scoping to labour law domain                |
| Search & retrieval (Elasticsearch) |      6       |       5       | Full-text multilingual search, faceted filtering, aggregations   |
| Legacy schema migration scripts    |      5       |       0       | Transform legacy labour law data into unified schema             |
| **Subtotal**                       |    **34**    |    **22**     |                                                                  |

**Dependencies:** Module 1 (Core Platform)
**Risks:** Legacy data quality and completeness; coverage gaps across 180+ countries may require manual cleanup

---

### Module 3: International Law Database

**Purpose:** International labour standards & conventions database — structurally mirrors Labour Law (Module 2) with distinct question sets and content schema. Reduced effort due to shared architecture.

| Sub-Component                  | Backend (PD) | Frontend (PD) | Notes                                                         |
| ------------------------------ | :----------: | :-----------: | ------------------------------------------------------------- |
| Content schema & data models   |      4       |       0       | International conventions, treaties, ILO standards            |
| Data entry UI adaptation       |      3       |       4       | Adapted from Labour Law UI with different field configuration |
| Domain-specific business rules |      3       |       2       | Ratification tracking, applicability mapping across countries |
| Legacy data migration scripts  |      4       |       0       | Transform existing international law data into unified schema |
| **Subtotal**                   |    **14**    |     **6**     |                                                               |

**Dependencies:** Module 1 (Core Platform), Module 2 (Labour Law — reuses architecture patterns)
**Risks:** Low — mirrors Module 2 structurally. Main risk is content schema clarity from WageIndicator SMEs.

---

### Module 4: CBA Processing Engine

**Purpose:** End-to-end pipeline for Collective Bargaining Agreement ingestion — from raw document upload through AI-powered conversion to clean structured HTML with human review.

| Sub-Component                  | Backend (PD) | Frontend (PD) | Notes                                                                    |
| ------------------------------ | :----------: | :-----------: | ------------------------------------------------------------------------ |
| Document ingestion (upload)    |      5       |       4       | PDF, HTML, DOCX upload; file validation, virus scanning, metadata        |
| AI-powered document conversion |      8       |       0       | PDF → structured HTML via document AI (Mistral / Dragon LLM)             |
| Structured data extraction     |      6       |       0       | Extract fields from converted documents into CBA data model              |
| HTML cleanup & formatting      |      4       |       0       | Headings, lists, tables — clean well-structured output                   |
| Editor review step (HITL)      |      4       |       7       | Side-by-side original vs. converted view; inline editing; approve/reject |
| CBA metadata management        |      4       |       4       | Parties, dates, coverage, industry codes, country/region tagging         |
| Legacy CBA schema migration    |      5       |       0       | Transform existing CBA data into unified schema                          |
| **Subtotal**                   |    **36**    |    **15**     |                                                                          |

**Dependencies:** Module 1 (Core Platform)
**Risks:** AI conversion quality varies by document type and language. Discovery-phase testing critical for model selection. Editor review UX must be polished — this is a daily-use tool for annotators.

---

### Module 5: AI Annotation Pipeline

**Purpose:** LLM-powered extraction and annotation of CBA and legal documents — automated pre-filling with confidence scoring and human-in-the-loop verification.

| Sub-Component                   | Backend (PD) | Frontend (PD) | Notes                                                                        |
| ------------------------------- | :----------: | :-----------: | ---------------------------------------------------------------------------- |
| LLM integration layer           |      6       |       0       | Abstraction over multiple LLM providers; EU-compliant models; retry/fallback |
| Document embedding pipeline     |      5       |       0       | Vector store for document chunks; semantic similarity for context retrieval  |
| LLM-powered extraction          |      6       |       0       | Prompt engineering for field extraction; few-shot examples per document type |
| Confidence scoring              |      4       |       3       | Per-field confidence scores; threshold-based auto-accept vs. manual review   |
| Human-in-the-loop review queue  |      5       |       8       | Queue UI, field-level accept/reject, batch operations, annotation history    |
| Model evaluation & benchmarking |      5       |       3       | A/B testing framework; accuracy tracking; model comparison dashboard         |
| **Subtotal**                    |    **31**    |    **14**     |                                                                              |

**Dependencies:** Module 4 (CBA Processing Engine)
**Risks:** LLM accuracy on multilingual legal documents. Cost management of LLM API calls at scale. Prompt injection hardening for any user-facing LLM interaction.

---

### Module 6: Pensions Database

**Purpose:** Survey-based pensions data collection using the Dynamic Survey / Form Engine — country-scoped questionnaires with versioned records and publishing workflow.

| Sub-Component                      | Backend (PD) | Frontend (PD) | Notes                                                                 |
| ---------------------------------- | :----------: | :-----------: | --------------------------------------------------------------------- |
| Pensions data models               |      4       |       0       | Country-specific pension schemes, benefit types, eligibility criteria |
| Survey integration (via Module 10) |      3       |       3       | Connect pensions questionnaires to form engine; data binding          |
| Country-scoped data entry          |      2       |       2       | Country context selection, regional pension scheme variations         |
| Publishing workflow                |      4       |       3       | Draft → Review → Published; role-gated like Labour Law                |
| Legacy pensions data migration     |      4       |       0       | Transform existing pensions data into unified schema                  |
| **Subtotal**                       |    **17**    |     **8**     |                                                                       |

**Dependencies:** Module 1 (Core Platform), Module 10 (Dynamic Survey / Form Engine)
**Risks:** Pensions data structure clarity — need SME input on country-specific variations. Depends on Module 10 being complete first.

---

### Module 7: Data Migration & Schema Unification

**Purpose:** Migrate all legacy COBRA data into the unified PostgreSQL schema — consolidating separate databases, 30+ Excel files, and Dropbox-resident data into one governed system.

| Sub-Component                    | Backend (PD) | Frontend (PD) | Notes                                                                                   |
| -------------------------------- | :----------: | :-----------: | --------------------------------------------------------------------------------------- |
| Legacy schema analysis & mapping |      8       |       0       | Document all source schemas, field mappings, data types, encoding across all legacy DBs |
| Database unification scripts     |      12      |       0       | Merge separate CBA, Labour Law, Int'l Law, Pensions DBs into single PostgreSQL          |
| Excel/Dropbox file ingestion     |      10      |       0       | Parse 30+ Excel files, normalize, validate, load into unified schema                    |
| Validation & reconciliation      |      8       |       5       | Row-count checks, referential integrity, data quality reports, exception handling       |
| Rollback capability              |      5       |       0       | Point-in-time recovery, staged migration with checkpoint/resume                         |
| Migration reporting dashboard    |      3       |       5       | Progress tracking, error summaries, data quality metrics, sign-off workflow             |
| **Subtotal**                     |    **46**    |    **10**     |                                                                                         |

**Dependencies:** Module 1 (unified schema must exist), Modules 2 & 4 (domain-specific models defined)
**Risks:** Highest-risk module. Legacy data quality is unknown. 25+ years of accumulated data across fragmented systems. Schema conflicts between separate databases. Manual cleanup effort may be underestimated. Requires dedicated WageIndicator SME availability for data questions.

---

### Module 8: Export & Data Distribution

**Purpose:** Controlled, tiered data export with field filtering, watermarking, and maker-checker approval — ensuring WageIndicator controls what data goes to whom and how much.

| Sub-Component                        | Backend (PD) | Frontend (PD) | Notes                                                                      |
| ------------------------------------ | :----------: | :-----------: | -------------------------------------------------------------------------- |
| Tiered export framework              |      6       |       4       | Configurable export profiles per consumer tier (free, subscriber, partner) |
| Field-level filtering                |      4       |       2       | Dynamic serialization — each API key maps to field inclusion/exclusion     |
| Aggregation enforcement              |      4       |       0       | Free tier gets aggregated data only; raw records restricted to paid tiers  |
| Statistical watermarking             |      4       |       0       | Row ordering permutation per consumer for leak tracing                     |
| Bulk export approval (maker-checker) |      4       |       4       | Configurable threshold; second-user approval before file generation        |
| API key management                   |      5       |       4       | Issue, scope, rotate, revoke keys; admin UI for key lifecycle              |
| Rate limiting & revocation           |      4       |       1       | Per-consumer rate limits at proxy + app layer; instant revocation          |
| **Subtotal**                         |    **31**    |    **15**     |                                                                            |

**Dependencies:** Module 1 (Core Platform), Module 11 (Unified API Gateway)
**Risks:** Watermarking logic needs validation that it doesn't distort analytical use of exported data. Rate limiting tuning requires real usage patterns.

---

### Module 9: Translation & Multilingual Support

**Purpose:** Multi-language content management and translation workflow — preserving the existing 70-language service layer while adding structured workflow tooling.

| Sub-Component                     | Backend (PD) | Frontend (PD) | Notes                                                              |
| --------------------------------- | :----------: | :-----------: | ------------------------------------------------------------------ |
| Language service layer            |      6       |       4       | Continuation of existing multi-language serving; API-based locale  |
| Multi-language content management |      5       |       5       | Content editing per locale, translation status tracking per record |
| Translation workflow              |      5       |       4       | Assign languages to translators, track progress, review & publish  |
| **Subtotal**                      |    **16**    |    **13**     |                                                                    |

**Dependencies:** Module 1 (Core Platform — multi-language framework)
**Risks:** Existing language service layer complexity — 70 languages with consistent question structures. Must not break current content serving during migration.

---

### Module 10: Dynamic Survey / Form Engine

**Purpose:** Admin-configurable form builder — question management, conditional logic, nested rules, and external API-fed dropdowns. Powers CBA surveys, Pensions questionnaire, and future survey-based databases.

| Sub-Component                                | Backend (PD) | Frontend (PD) | Notes                                                                 |
| -------------------------------------------- | :----------: | :-----------: | --------------------------------------------------------------------- |
| Question management UI                       |      5       |       8       | Add, edit, reorder, archive questions; drag-and-drop ordering         |
| Data type support                            |      4       |       4       | Text, number, date, dropdown, multi-select, boolean, free text        |
| Required/optional flags                      |      2       |       2       | Per-question configuration by admins, validation enforcement          |
| Conditional visibility (visual rule builder) |      6       |      10       | "If Q_A = X, show Q_B" — visual UI, no-code rule creation             |
| Nested logic support                         |      5       |       4       | Conditions within conditions; AND/OR grouping; arbitrary depth        |
| External API-fed dropdowns                   |      4       |       3       | Admin specifies endpoint + field mapping; dynamic population          |
| Form versioning                              |      4       |       2       | Version history, ability to revert, impact analysis on collected data |
| **Subtotal**                                 |    **30**    |    **33**     |                                                                       |

**Dependencies:** Module 1 (Core Platform)
**Risks:** Visual rule builder is the most complex frontend component in the system. Nested logic edge cases. Must be intuitive enough for non-technical admins — poor UX undermines the module's value.

---

### Module 11: Unified API Gateway

**Purpose:** Single API surface for all external consumers — per-consumer scoping, rate limiting, usage analytics, and auto-generated documentation.

| Sub-Component                    | Backend (PD) | Frontend (PD) | Notes                                                         |
| -------------------------------- | :----------: | :-----------: | ------------------------------------------------------------- |
| API surface design & versioning  |      6       |       0       | RESTful API, versioned endpoints, consistent response format  |
| Per-consumer scoping             |      5       |       0       | Scope by datasets, countries, actions per API key             |
| Rate limiting                    |      4       |       0       | Tiered rate limits at reverse proxy + Django throttle layer   |
| Usage analytics                  |      4       |       4       | Request tracking, consumer usage dashboards, quota monitoring |
| Auto-generated API documentation |      3       |       0       | OpenAPI/Swagger spec auto-gen from Django serializers         |
| **Subtotal**                     |    **22**    |     **4**     |                                                               |

**Dependencies:** Module 1 (Core Platform)
**Risks:** API design must accommodate all current and near-future data consumers. Breaking changes after launch are costly.

---

### Module 12: LLM Query Interface

**Purpose:** Natural language query API for the public website — users ask questions in plain language, the LLM answers using approved WageIndicator data with strict scope boundaries.

| Sub-Component                  | Backend (PD) | Frontend (PD) | Notes                                                                          |
| ------------------------------ | :----------: | :-----------: | ------------------------------------------------------------------------------ |
| Natural language query API     |      6       |       0       | Endpoint accepts text queries, returns structured + natural language responses |
| Restricted database user setup |      4       |       0       | Dedicated DB users with SELECT-only on approved tables; no schema visibility   |
| Prompt injection guardrails    |      5       |       0       | Input sanitization, output validation, context window restrictions             |
| Topic boundary enforcement     |      4       |       0       | Application-layer rules limiting LLM to WageIndicator-approved topics only     |
| Access layer integration       |      4       |       3       | Compatible with existing email/SMS registration and subscription tiers         |
| Response caching               |      3       |       0       | Cache frequent queries; invalidation on data updates                           |
| **Subtotal**                   |    **26**    |     **3**     |                                                                                |

**Dependencies:** Module 1 (Core Platform), Module 11 (Unified API Gateway)
**Risks:** Prompt injection is the primary security concern. Strict guardrails are non-negotiable. LLM cost at scale — usage-based pricing means costs grow with adoption. Response quality for multilingual queries needs testing.

---

### Module 13: Monitoring & Observability

**Purpose:** Full observability stack — metrics, alerting, log aggregation, and health monitoring for all platform components.

| Sub-Component                  | Backend (PD) | Frontend (PD) | Notes                                                                       |
| ------------------------------ | :----------: | :-----------: | --------------------------------------------------------------------------- |
| Prometheus + Grafana setup     |      4       |       0       | Metrics collection, retention policies, Kubernetes-native service discovery |
| Alerting rules                 |      4       |       0       | 403 spikes, export anomalies, login failures, geo-anomalies, DAG failures   |
| Log aggregation                |      4       |       0       | Centralized logging, structured log format, search & filter                 |
| Health checks & SLA dashboards |      3       |       0       | Per-service health endpoints, uptime tracking, SLA reporting                |
| **Subtotal**                   |    **15**    |     **0**     |                                                                             |

**Dependencies:** Module 0 (infrastructure must exist)
**Risks:** Low — standard observability stack. Alerting thresholds need tuning with real traffic.

---

### Module 14: Security Hardening (Cross-cutting)

**Purpose:** CI/CD security gates, encryption setup, incident response playbooks, and operational security practices applied across all modules.

| Sub-Component                                | Backend (PD) | Frontend (PD) | Notes                                                                     |
| -------------------------------------------- | :----------: | :-----------: | ------------------------------------------------------------------------- |
| CI/CD security gates (SAST, dependency scan) |      5       |       0       | Bandit, pip-audit, gitleaks — block merge on critical/high findings       |
| Container image scanning                     |      3       |       0       | Trivy on build; block push on critical vulnerabilities                    |
| DAST (dynamic scanning)                      |      3       |       0       | OWASP ZAP on staging; advisory findings triaged within sprint             |
| Encryption setup (at-rest, in-transit, mTLS) |      4       |       0       | TLS 1.2+, AES-256, pod-to-pod mTLS, pgcrypto for sensitive fields         |
| Incident response playbooks                  |      2       |       0       | Documented runbooks for compromised keys, data leaks, unauthorized access |
| Backup & restore validation                  |      2       |       0       | Encrypted backups, quarterly restore drills, RTO/RPO validation           |
| **Subtotal**                                 |    **19**    |     **0**     |                                                                           |

**Dependencies:** Module 0 (infrastructure)
**Risks:** Low — well-understood practices. Ongoing discipline required post-delivery.

---

### Module 15: Documentation & Handover

**Purpose:** Technical and operational documentation to ensure WageIndicator can operate, maintain, and extend the platform independently.

| Sub-Component               | Backend (PD) | Frontend (PD) | Notes                                                        |
| --------------------------- | :----------: | :-----------: | ------------------------------------------------------------ |
| Technical architecture docs |      4       |       0       | System diagrams, data flows, integration points, ADRs        |
| API documentation           |      3       |       0       | Auto-generated OpenAPI + narrative guides for consumers      |
| Operational runbooks        |      3       |       0       | Deployment, rollback, incident response, scaling procedures  |
| Admin user guides           |      2       |       3       | End-user documentation for admin panel, form engine, exports |
| **Subtotal**                |    **12**    |     **3**     |                                                              |

**Dependencies:** All modules (documentation produced incrementally, finalized at end)
**Risks:** Low — provided team documents as they build. Risk is documentation falling behind development.

---

## Assumptions

1. **Client Inputs**
   - WageIndicator provides timely access to all legacy databases, Dropbox files, and COBRA 2003 system
   - Subject matter experts available for at least 8 hours/week for data questions, schema validation, and form/survey design
   - Coding frames and classification standards provided upfront
   - Sample data for all domains (Labour Law, CBA, Pensions, International Law) available within Discovery phase

2. **Technical**
   - Single PostgreSQL instance is sufficient for unified schema (no sharding needed at current scale)
   - EU cloud infrastructure (Hetzner/OVHcloud) is provisioned and accessible before development starts
   - LLM provider decision (Mistral, Dragon LLM, or alternative) is finalized during Discovery
   - Elasticsearch cluster available for search features
   - GitLab or GitHub repository access granted to Altysys team

3. **Process**
   - Feedback cycles of ≤ 5 business days on deliverables requiring client review
   - Sprint demos every 2 weeks with WageIndicator stakeholder participation
   - Schema migration can proceed domain-by-domain (Labour Law → CBA → Int'l Law → Pensions) — no big-bang requirement
   - User acceptance testing (UAT) participation from WageIndicator with at least 2 designated testers

---

## Out of Scope

| Item                                         | Reason                                                                             |
| -------------------------------------------- | ---------------------------------------------------------------------------------- |
| **Automated Law Change Detection**           | Monitored pipeline for legal source changes — deferred to future phase             |
| **Ancillary Data Management**                | Excel/Dropbox replacement for legacy data files and surveys — not in current scope |
| **Living Wage Module**                       | Python-based automated calculation and QA — deferred to future phase               |
| **ETL & Data Pipelines**                     | Airflow-based orchestration — deferred to future phase                             |
| **KoBoToolbox Integration**                  | Field data collection sync — not in current scope                                  |
| **Analytics & Reporting (Metabase)**         | BI dashboards — deferred to future phase                                           |
| Plone CMS replacement                        | As per original proposal                                                           |
| Website redesign                             | As per original proposal                                                           |
| Salary Survey logic                          | As per original proposal                                                           |
| Historical backfilling (beyond agreed scope) | As per original proposal                                                           |
| Mobile app                                   | As per original proposal                                                           |
| LLM fine-tuning on WageIndicator data        | Model works with data at query time; no permanent training on proprietary data     |
