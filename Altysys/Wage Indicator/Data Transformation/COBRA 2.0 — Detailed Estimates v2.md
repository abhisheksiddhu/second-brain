# COBRA 2.0 — Detailed Estimates (All Tasks)

| Sub-Component                               | Task Description                                                                                              | BE (PD) | FE (PD) | Total (PD) |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | :-----: | :-----: | :--------: |
| **M0: Discovery & Project Setup**           |                                                                                                               |         |         |            |
| Legacy Schema Audit                         | Map all COBRA databases, document table structures, row counts, relationships                                 |    3    |    0    |     3      |
| Data Profiling                              | Catalogue 30+ Excel files in Dropbox, identify schemas, data quality issues                                   |    2    |    0    |     2      |
| Schema Design                               | Unified PostgreSQL schema design — ERD, table definitions, normalization decisions, ADR                       |    3    |    0    |     3      |
| Infrastructure                              | Docker Compose setup, CI/CD pipelines, staging env on EU cloud                                                |    2    |    0    |     2      |
| Dev Environment                             | docker-compose.yml, seed data scripts, .env templates, onboarding README                                      |    1    |    0    |     1      |
| Security                                    | STRIDE threat modeling — first-pass threat register, map mitigations to backlog                               |    1    |    0    |     1      |
| LLM Evaluation                              | Test 3-5 sample documents against candidate models, accuracy comparison                                       |    3    |    0    |     3      |
| Sign-off                                    | Tech stack confirmation, ADR documentation, team kickoff                                                      |    1    |    0    |     1      |
| **M1: COBRA Core Platform**                 |                                                                                                               |         |         |            |
| Unified DB Schema                           | PostgreSQL schema DDL — create all core tables, constraints, foreign keys                                     |    3    |    0    |     3      |
| Unified DB Schema                           | Django model definitions and migration files for core schema                                                  |    2    |    0    |     2      |
| Unified DB Schema                           | Seed data — 180+ countries (ISO 3166), 75+ languages (ISO 639), currencies, regions                           |    2    |    0    |     2      |
| Unified DB Schema                           | Database indexing strategy — composite indexes, partial indexes for common query patterns                     |    2    |    0    |     2      |
| Unified DB Schema                           | Connection pooling (pgBouncer) and query performance baseline                                                 |    1    |    0    |     1      |
| Core Data Models                            | Country model — ISO codes, region, sub-region, currency, metadata, active flag                                |    2    |    0    |     2      |
| Core Data Models                            | Language model — locale code, script direction (LTR/RTL), fallback language chain                             |    2    |    0    |     2      |
| Core Data Models                            | Shared reference models — Industry, Sector, OccupationCode (ISCO/ISIC classifications)                        |    2    |    0    |     2      |
| Core Data Models                            | Base model mixins — TimestampMixin, SoftDeleteMixin, CountryScopedMixin, AuditableMixin                       |    2    |    0    |     2      |
| Authentication                              | User registration endpoint with email verification (send link, confirm token)                                 |    2    |    0    |     2      |
| Authentication                              | Registration form — fields, client validation, email verification screen                                      |    0    |    2    |     2      |
| Authentication                              | Login endpoint — JWT access/refresh token pair, session cookie option                                         |    1    |    0    |     1      |
| Authentication                              | Login page — form, error handling, redirect to dashboard                                                      |    0    |    1    |     1      |
| Authentication                              | Forgot password — generate reset token, send email, validate & reset                                          |    1    |    0    |     1      |
| Authentication                              | Reset password page — token validation, new password form, confirmation                                       |    0    |    1    |     1      |
| Authentication                              | Password policy enforcement (min length, complexity rules, breach check)                                      |    1    |    0    |     1      |
| Authentication                              | Logout, token refresh, session invalidation on password change                                                |    0    |    1    |     1      |
| Custom RBAC Engine                          | Permission model — module × action matrix (view, create, edit, delete, publish, export per module)            |    2    |    0    |     2      |
| Custom RBAC Engine                          | Role model with M2M relationship to permissions; role metadata (name, description, is_default)                |    1    |    0    |     1      |
| Custom RBAC Engine                          | Role CRUD API — create, update, clone, archive roles; prevent deletion of in-use roles                        |    2    |    0    |     2      |
| Custom RBAC Engine                          | Permission matrix UI — grid of modules vs. actions; toggle permissions per role; bulk select                  |    0    |    4    |     4      |
| Custom RBAC Engine                          | 6 default role templates seeded on first run (Admin, Data Manager, Annotator, Reviewer, API Consumer, Viewer) |    1    |    0    |     1      |
| Custom RBAC Engine                          | Permission-checking middleware — decorator-based endpoint protection; 403 on violation                        |    2    |    0    |     2      |
| Custom RBAC Engine                          | User → Role assignment UI — assign/revoke roles per user; bulk assignment                                     |    1    |    2    |     3      |
| Custom RBAC Engine                          | Permission-aware frontend rendering — hide/disable unauthorized menu items, buttons, routes                   |    0    |    1    |     1      |
| Custom RBAC Engine                          | Role change propagation — invalidate cached permissions on role update                                        |    1    |    0    |     1      |
| Admin Panel Shell                           | Admin layout shell — sidebar navigation, header bar, breadcrumbs, responsive design                           |    0    |    3    |     3      |
| Admin Panel Shell                           | Dashboard page — system stats, recent activity feed, quick action cards                                       |    2    |    3    |     5      |
| Admin Panel Shell                           | User management screens — list, create, edit, deactivate, view assigned roles/countries                       |    2    |    3    |     5      |
| Admin Panel Shell                           | System settings — site configuration, feature toggles, maintenance mode, email settings                       |    1    |    2    |     3      |
| Admin Panel Shell                           | Reusable Vue components — data tables with sort/filter/pagination, form controls, modals, toasts              |    0    |    1    |     1      |
| Admin Panel Shell                           | Django Admin customizations for superuser-only operations (raw model access)                                  |    1    |    0    |     1      |
| Audit Logging (Basic)                       | AuditLog model — user, action, resource type, resource ID, timestamp, IP address                              |    1    |    0    |     1      |
| Audit Logging (Basic)                       | Middleware for automatic audit log creation on API requests (POST, PUT, PATCH, DELETE)                        |    2    |    0    |     2      |
| Audit Logging (Basic)                       | Log export (CSV) for compliance                                                                               |    1    |    0    |     1      |
| Audit Logging (Basic)                       | Audit log viewer — filterable table (user, action, date range, module), paginated                             |    0    |    2    |     2      |
| Country-Scoped Access                       | UserCountryAssignment M2M model — assign users to one or more countries                                       |    1    |    0    |     1      |
| Country-Scoped Access                       | QuerySet manager with automatic country filtering (all model queries scoped to user's countries)              |    2    |    0    |     2      |
| Country-Scoped Access                       | Admin UI for assigning countries to users (multi-select, bulk assign)                                         |    1    |    1    |     2      |
| Country-Scoped Access                       | Country context switcher — header dropdown to select active country, persisted in session                     |    0    |    2    |     2      |
| Country-Scoped Access                       | Module-scoped permission extension — combine country scope + role permissions in access checks                |    1    |    0    |     1      |
| Multi-Language Framework                    | Translation key registry — model for managing translation strings, namespaced by module                       |    2    |    0    |     2      |
| Multi-Language Framework                    | 70-language locale file management — JSON/PO file structure, tooling for import/export                        |    2    |    0    |     2      |
| Multi-Language Framework                    | Locale detection middleware — Accept-Language header, user preference, URL prefix fallback                    |    2    |    0    |     2      |
| Multi-Language Framework                    | Vue i18n integration — plugin setup, lazy-loaded locale bundles, pluralization rules                          |    0    |    3    |     3      |
| Multi-Language Framework                    | Translation import/export CLI — manage.py commands for syncing locale files                                   |    2    |    0    |     2      |
| Multi-Language Framework                    | Locale selector component — dropdown in header, persists preference to user profile                           |    0    |    2    |     2      |
| Notification System                         | Notification model — type, recipient, title, message, read/unread, created_at, action_url                     |    1    |    0    |     1      |
| Notification System                         | Email notification service — Django template-based emails, SMTP/SES integration, async via Celery             |    2    |    0    |     2      |
| Notification System                         | In-app notification API — list, mark-as-read, mark-all-read, unread count                                     |    1    |    0    |     1      |
| Notification System                         | Notification center UI — bell icon with unread badge, dropdown panel, click-through to source                 |    0    |    3    |     3      |
| Notification System                         | User notification preferences — per-event-type opt-in/out (email, in-app toggles)                             |    1    |    2    |     3      |
| **M2: Labour Law Database**                 |                                                                                                               |         |         |            |
| Data Models                                 | Django models for law categories — minimum wages, working hours, leave, termination, social security          |    2    |    0    |     2      |
| Data Models                                 | Temporal validity fields — effective_from, effective_to, legislative_reference, gazette_url                   |    1    |    0    |     1      |
| Data Models                                 | Country-specific field configuration — JSONField schema per country for flexible field sets                   |    1    |    0    |     1      |
| Data Models                                 | Model serializers with field-level validation rules                                                           |    1    |    0    |     1      |
| Structured Data Entry UI                    | Dynamic form renderer — load country-specific field config, render appropriate input types                    |    1    |    3    |     4      |
| Structured Data Entry UI                    | Client + server-side validation — required fields, data type checks, cross-field rules                        |    1    |    1    |     2      |
| Structured Data Entry UI                    | Country context switching — changing country reloads field config and existing records                        |    1    |    2    |     3      |
| Structured Data Entry UI                    | Draft auto-save — periodic save to prevent data loss, explicit save button                                    |    1    |    1    |     2      |
| Structured Data Entry UI                    | Inline help — field-level tooltips with guidance text from admin configuration                                |    1    |    1    |     2      |
| Version-Controlled Records                  | RecordVersion model — full JSON snapshot of record on each save, version number, author                       |    2    |    0    |     2      |
| Version-Controlled Records                  | Version history API — list versions, retrieve specific version                                                |    1    |    0    |     1      |
| Version-Controlled Records                  | Version history list view — table of versions with date, author, action                                       |    0    |    1    |     1      |
| Version-Controlled Records                  | Side-by-side diff view — highlight field differences between two selected versions                            |    1    |    1    |     2      |
| Version-Controlled Records                  | Rollback to version — restore previous snapshot with confirmation dialog, creates new version                 |    1    |    1    |     2      |
| Publishing Workflow                         | Workflow state machine — Draft → Under Review → Published, with transition validation                         |    2    |    0    |     2      |
| Publishing Workflow                         | Role-gated transitions — only Reviewers/Admins can approve; Annotators submit for review                      |    1    |    0    |     1      |
| Publishing Workflow                         | Status transition UI — status badge, action buttons per state, comment on transition                          |    1    |    2    |     3      |
| Publishing Workflow                         | Publishing history log — track all state changes with timestamp, actor, comment                               |    1    |    1    |     2      |
| Publishing Workflow                         | Notification trigger — send email + in-app notification on review request / approval / rejection              |    0    |    1    |     1      |
| Country-Scoped Management                   | Extend core country-scoping to labour law API views and querysets                                             |    2    |    0    |     2      |
| Country-Scoped Management                   | Country filter in labour law list view — dropdown, persisted selection                                        |    0    |    1    |     1      |
| Country-Scoped Management                   | Bulk operations scoped by country — bulk publish, bulk assign reviewer                                        |    1    |    1    |     2      |
| Search & Retrieval (PG FTS)                 | PostgreSQL tsvector setup — GIN indexes, search configuration per language                                    |    2    |    0    |     2      |
| Search & Retrieval (PG FTS)                 | Search API — full-text query with filters (country, category, date range, status)                             |    1    |    0    |     1      |
| Search & Retrieval (PG FTS)                 | Search UI — search bar, filter panel, results list with highlighting, pagination                              |    0    |    2    |     2      |
| Search & Retrieval (PG FTS)                 | Sort options — relevance, date, country                                                                       |    0    |    1    |     1      |
| Legacy Migration Scripts                    | Analyze legacy labour law DB schema — document tables, columns, types, encoding                               |    1    |    0    |     1      |
| Legacy Migration Scripts                    | Write ETL scripts — transform legacy rows into unified schema format                                          |    2    |    0    |     2      |
| Legacy Migration Scripts                    | Data validation — row-count checks, referential integrity, null handling                                      |    1    |    0    |     1      |
| Legacy Migration Scripts                    | Migration dry-run on staging with reconciliation report                                                       |    1    |    0    |     1      |
| **M3: International Law DB**                |                                                                                                               |         |         |            |
| Content Schema & Models                     | Models for international conventions, ILO standards, treaty records                                           |    2    |    0    |     2      |
| Content Schema & Models                     | Ratification status model — country × convention with ratification date, status                               |    1    |    0    |     1      |
| Content Schema & Models                     | Serializers and API endpoints                                                                                 |    1    |    0    |     1      |
| Data Entry UI Adaptation                    | Adapt Module 2 form components with international law field configuration                                     |    1    |    2    |     3      |
| Data Entry UI Adaptation                    | Convention selector — searchable dropdown of ILO conventions / treaties                                       |    1    |    1    |     2      |
| Data Entry UI Adaptation                    | Cross-country applicability view — which countries ratified which convention                                  |    1    |    1    |     2      |
| Domain Business Rules                       | Ratification tracking logic — track status changes, effective dates                                           |    1    |    0    |     1      |
| Domain Business Rules                       | Applicability mapping — link international conventions to national labour law records                         |    1    |    1    |     2      |
| Domain Business Rules                       | Validation rules specific to international law records                                                        |    1    |    1    |     2      |
| Legacy Data Migration                       | Analyze legacy international law schema                                                                       |    1    |    0    |     1      |
| Legacy Data Migration                       | Write transformation scripts into unified schema                                                              |    2    |    0    |     2      |
| Legacy Data Migration                       | Validation and staging dry-run                                                                                |    1    |    0    |     1      |
| **M4: CBA Processing Engine**               |                                                                                                               |         |         |            |
| Document Ingestion                          | Upload API — accept PDF, DOCX; file type validation, size limits, virus scanning (ClamAV)                     |    2    |    0    |     2      |
| Document Ingestion                          | Upload UI — drag-and-drop zone, progress indicator, file list, metadata form                                  |    0    |    3    |     3      |
| Document Ingestion                          | File storage abstraction — local/S3-compatible, organized by country/year                                     |    1    |    0    |     1      |
| Document Ingestion                          | Document metadata extraction on upload — page count, language detection, file hash                            |    1    |    0    |     1      |
| Document Ingestion                          | Upload validation error handling — clear error messages, retry option                                         |    1    |    1    |     2      |
| OCR for Scanned PDFs                        | OCR pipeline integration — Tesseract or cloud OCR service for image-based PDFs                                |    2    |    0    |     2      |
| OCR for Scanned PDFs                        | Scanned PDF detection — heuristic to distinguish text-based vs. image-based pages                             |    1    |    0    |     1      |
| OCR for Scanned PDFs                        | OCR output normalization — clean extracted text, preserve page structure                                      |    1    |    0    |     1      |
| AI Document Conversion                      | PDF→text extraction pipeline — handle multi-column, tables, headers, footnotes                                |    3    |    0    |     3      |
| AI Document Conversion                      | DOCX→structured HTML conversion — preserve formatting, lists, tables                                          |    2    |    0    |     2      |
| AI Document Conversion                      | LLM-assisted structure detection — identify sections, articles, clauses using single LLM provider             |    3    |    0    |     3      |
| Structured Data Extraction                  | CBA data model field extraction — parties, effective dates, industry, coverage scope                          |    3    |    0    |     3      |
| Structured Data Extraction                  | Extraction prompt engineering — per-field prompts with few-shot examples                                      |    2    |    0    |     2      |
| Structured Data Extraction                  | Extraction output validation — type checking, range validation, mandatory field enforcement                   |    1    |    0    |     1      |
| HTML Cleanup & Formatting                   | HTML sanitization — strip unsafe tags, normalize structure, fix encoding                                      |    2    |    0    |     2      |
| HTML Cleanup & Formatting                   | Heading hierarchy enforcement — auto-correct heading levels, generate TOC                                     |    1    |    0    |     1      |
| HTML Cleanup & Formatting                   | Table and list normalization — consistent HTML structure for downstream consumption                           |    1    |    0    |     1      |
| Editor Review (HITL)                        | Review queue API — list pending documents, assignment, lock-on-open to prevent conflicts                      |    2    |    0    |     2      |
| Editor Review (HITL)                        | Side-by-side viewer — original document (PDF viewer) alongside converted HTML                                 |    0    |    3    |     3      |
| Editor Review (HITL)                        | Inline HTML editor — rich text editing of converted output, section-level accept/reject                       |    0    |    3    |     3      |
| Editor Review (HITL)                        | Approve / reject / request re-conversion workflow with comments                                               |    2    |    1    |     3      |
| CBA Metadata Management                     | CBA metadata model — parties, dates, coverage, industry (ISIC), region, legal status                          |    2    |    0    |     2      |
| CBA Metadata Management                     | Metadata entry form — pre-filled from AI extraction, editable by annotator                                    |    1    |    3    |     4      |
| CBA Metadata Management                     | Metadata validation rules — date logic, mandatory fields per status                                           |    1    |    1    |     2      |
| Legacy CBA Migration                        | Analyze legacy CBA schema and document storage structure                                                      |    1    |    0    |     1      |
| Legacy CBA Migration                        | Migration scripts — transform legacy CBA data into unified schema                                             |    2    |    0    |     2      |
| Legacy CBA Migration                        | File migration — move legacy documents to new storage structure                                               |    1    |    0    |     1      |
| Legacy CBA Migration                        | Validation and staging reconciliation                                                                         |    1    |    0    |     1      |
| **M5: AI Annotation Pipeline**              |                                                                                                               |         |         |            |
| LLM Integration Layer                       | Single LLM provider client — API wrapper with retry, timeout, error handling                                  |    2    |    0    |     2      |
| LLM Integration Layer                       | Token usage tracking and cost monitoring per request                                                          |    1    |    0    |     1      |
| LLM Integration Layer                       | EU data residency compliance validation — ensure no data leaves EU boundary                                   |    1    |    0    |     1      |
| Document Embedding                          | Document chunking strategy — split by sections/paragraphs, respect semantic boundaries                        |    2    |    0    |     2      |
| Document Embedding                          | Vector store setup — pgvector or similar, embedding generation for document chunks                            |    2    |    0    |     2      |
| Document Embedding                          | Semantic similarity retrieval — query similar document sections for context injection                         |    1    |    0    |     1      |
| LLM-Powered Extraction                      | Prompt templates per document type — CBA, labour law, international convention                                |    2    |    0    |     2      |
| LLM-Powered Extraction                      | Few-shot example management — maintain curated examples per document type/language                            |    2    |    0    |     2      |
| LLM-Powered Extraction                      | Extraction pipeline — chain prompts, parse structured output, handle partial failures                         |    2    |    0    |     2      |
| Confidence Scoring                          | Per-field confidence score computation — LLM self-assessment + heuristic validation                           |    2    |    0    |     2      |
| Confidence Scoring                          | Configurable thresholds — auto-accept above X%, mandatory review below Y%                                     |    1    |    0    |     1      |
| Confidence Scoring                          | Confidence score display in UI — color-coded indicators per field (green/yellow/red)                          |    0    |    2    |     2      |
| Confidence Scoring                          | Threshold configuration admin screen                                                                          |    1    |    1    |     2      |
| HITL Review Queue                           | Review queue model — items, assignment, priority, status (pending/in-review/approved/rejected)                |    2    |    0    |     2      |
| HITL Review Queue                           | Queue list view — sortable by confidence, date, language; filter by status, assignee                          |    0    |    2    |     2      |
| HITL Review Queue                           | Field-level review UI — accept/reject individual extracted fields, edit inline, add comments                  |    0    |    4    |     4      |
| HITL Review Queue                           | Batch operations — bulk approve high-confidence items, bulk assign to reviewer                                |    2    |    1    |     3      |
| HITL Review Queue                           | Annotation history — full trail of extraction → review → correction per field                                 |    1    |    1    |     2      |
| Model Evaluation                            | Ground truth dataset management — curated annotated documents for accuracy measurement                        |    2    |    0    |     2      |
| Model Evaluation                            | Accuracy metrics computation — precision, recall, F1 per field type, per language                             |    2    |    0    |     2      |
| Model Evaluation                            | Evaluation dashboard — accuracy trends over time, per-field breakdown, comparison charts                      |    1    |    3    |     4      |
| **M6: Pensions Database**                   |                                                                                                               |         |         |            |
| Pensions Data Models                        | Models — pension schemes, benefit types, eligibility criteria, contribution rates                             |    2    |    0    |     2      |
| Pensions Data Models                        | Country-specific pension variations — scheme subtypes, regional rules                                         |    1    |    0    |     1      |
| Pensions Data Models                        | Serializers and validation                                                                                    |    1    |    0    |     1      |
| Survey Integration                          | Wire pensions questionnaire definitions to form engine API                                                    |    1    |    0    |     1      |
| Survey Integration                          | Data binding — map survey responses to pensions data models                                                   |    1    |    0    |     1      |
| Survey Integration                          | Survey rendering within pensions module context                                                               |    0    |    2    |     2      |
| Survey Integration                          | Response submission and storage pipeline                                                                      |    1    |    1    |     2      |
| Country-Scoped Entry                        | Country context selection — filter schemes by selected country                                                |    1    |    1    |     2      |
| Country-Scoped Entry                        | Regional pension scheme variations — sub-national scheme support                                              |    1    |    1    |     2      |
| Publishing Workflow                         | Reuse Module 2 workflow engine — configure for pensions domain                                                |    2    |    0    |     2      |
| Publishing Workflow                         | Pensions-specific review rules — mandatory field checks before submission                                     |    1    |    0    |     1      |
| Publishing Workflow                         | Status management UI — reuse workflow components from Module 2                                                |    0    |    2    |     2      |
| Publishing Workflow                         | Notification integration — review/approval alerts for pensions records                                        |    1    |    1    |     2      |
| Legacy Migration                            | Analyze legacy pensions data structure                                                                        |    1    |    0    |     1      |
| Legacy Migration                            | Write migration scripts                                                                                       |    2    |    0    |     2      |
| Legacy Migration                            | Validation and staging dry-run                                                                                |    1    |    0    |     1      |
| **M7: Data Migration & Schema Unification** |                                                                                                               |         |         |            |
| Schema Analysis & Mapping                   | Document all source schemas — legacy CBA, Labour Law, Int'l Law, Pensions databases                           |    3    |    0    |     3      |
| Schema Analysis & Mapping                   | Field mapping matrix — source column → target column, data type conversions, encoding fixes                   |    3    |    0    |     3      |
| Schema Analysis & Mapping                   | Data quality assessment — null rates, duplicate detection, inconsistency report per source                    |    2    |    0    |     2      |
| DB Unification Scripts                      | CBA database migration script — transform & load into unified schema                                          |    3    |    0    |     3      |
| DB Unification Scripts                      | Labour Law database migration script                                                                          |    3    |    0    |     3      |
| DB Unification Scripts                      | International Law database migration script                                                                   |    2    |    0    |     2      |
| DB Unification Scripts                      | Pensions database migration script                                                                            |    2    |    0    |     2      |
| DB Unification Scripts                      | Cross-database reference resolution — link records across domains                                             |    2    |    0    |     2      |
| Excel/Dropbox Ingestion                     | Excel parser framework — handle varying formats, sheet structures, merged cells across 30+ files              |    3    |    0    |     3      |
| Excel/Dropbox Ingestion                     | Per-file ingestion scripts with field mapping and transformation rules                                        |    4    |    0    |     4      |
| Excel/Dropbox Ingestion                     | Data normalization — standardize country names, date formats, encoding, reference codes                       |    2    |    0    |     2      |
| Excel/Dropbox Ingestion                     | Error handling — skip vs. quarantine bad rows, generate exception report                                      |    1    |    0    |     1      |
| Validation & Reconciliation                 | Row-count reconciliation — source vs. target totals per table, per domain                                     |    2    |    0    |     2      |
| Validation & Reconciliation                 | Referential integrity checks — orphaned records, broken foreign keys                                          |    2    |    0    |     2      |
| Validation & Reconciliation                 | Data quality scoring — completeness, consistency, accuracy metrics per domain                                 |    2    |    0    |     2      |
| Validation & Reconciliation                 | Exception handling — quarantine queue for records failing validation                                          |    2    |    0    |     2      |
| Validation & Reconciliation                 | Validation dashboard — progress tracker, error summary, data quality charts, drill-down                       |    0    |    5    |     5      |
| Rollback Capability                         | Staged migration with named checkpoints — can resume from last successful stage                               |    2    |    0    |     2      |
| Rollback Capability                         | Pre-migration database snapshot automation — pg_dump before each stage                                        |    1    |    0    |     1      |
| Rollback Capability                         | Rollback script — restore to any checkpoint with referential integrity                                        |    2    |    0    |     2      |
| Migration Reporting                         | Migration run model — track jobs, stages, timing, status, error counts                                        |    1    |    0    |     1      |
| Migration Reporting                         | Progress dashboard — per-domain progress bars, row counts, stage status                                       |    1    |    3    |     4      |
| Migration Reporting                         | Sign-off workflow — domain-level sign-off by data manager, audit trail                                        |    1    |    2    |     3      |
| **M8: Export & Data Distribution**          |                                                                                                               |         |         |            |
| Tiered Export Framework                     | ExportProfile model — tier name, field inclusion list, format options, aggregation rules                      |    2    |    0    |     2      |
| Tiered Export Framework                     | Profile configuration admin UI — create/edit tiers, assign field sets, preview output                         |    1    |    3    |     4      |
| Tiered Export Framework                     | Export generation engine — serialize data per profile, output CSV/JSON/XLSX                                   |    2    |    0    |     2      |
| Tiered Export Framework                     | Async export job queue — Celery task for large exports, download-ready notification                           |    1    |    1    |     2      |
| Field-Level Filtering                       | Dynamic serializer — resolve API key → tier → included fields at runtime                                      |    2    |    0    |     2      |
| Field-Level Filtering                       | Field whitelist/blacklist configuration per tier                                                              |    1    |    1    |     2      |
| Field-Level Filtering                       | Nested field handling — control depth of related objects in output                                            |    1    |    1    |     2      |
| Aggregation Enforcement                     | Free-tier aggregation layer — compute averages, counts, ranges instead of raw records                         |    2    |    0    |     2      |
| Aggregation Enforcement                     | Aggregation rule configuration — per-field aggregation type, grouping dimensions                              |    1    |    0    |     1      |
| Aggregation Enforcement                     | Tier-check middleware — block raw record access for free-tier keys                                            |    1    |    0    |     1      |
| Statistical Watermarking                    | Row-ordering permutation algorithm — deterministic per-consumer seed                                          |    2    |    0    |     2      |
| Statistical Watermarking                    | Watermark embedding on export — transparent to consumer, detectable by WageIndicator                          |    1    |    0    |     1      |
| Statistical Watermarking                    | Leak detection utility — given leaked data, identify originating API key                                      |    1    |    0    |     1      |
| Bulk Export Approval                        | Configurable export threshold — row count / data volume trigger for approval requirement                      |    1    |    0    |     1      |
| Bulk Export Approval                        | Approval queue model — pending exports, assigned approver, status                                             |    1    |    0    |     1      |
| Bulk Export Approval                        | Approval UI — review export params, preview sample, approve/reject with comment                               |    1    |    3    |     4      |
| Bulk Export Approval                        | Post-approval file generation and download link with expiry                                                   |    1    |    1    |     2      |
| API Key Management                          | APIKey model — key hash, consumer, tier, scoped datasets, scoped countries, active flag                       |    2    |    0    |     2      |
| API Key Management                          | Key lifecycle API — issue, rotate, revoke; key shown once on creation                                         |    1    |    0    |     1      |
| API Key Management                          | Key management admin UI — list keys, filter by consumer/tier, rotate, revoke, view usage                      |    1    |    3    |     4      |
| API Key Management                          | Key authentication middleware — validate, resolve tier, inject scoping                                        |    1    |    1    |     2      |
| Rate Limiting & Revocation                  | Per-consumer rate limit configuration — tiered limits stored with API key                                     |    1    |    0    |     1      |
| Rate Limiting & Revocation                  | Django throttle layer — token bucket implementation with Redis backend                                        |    2    |    0    |     2      |
| Rate Limiting & Revocation                  | Instant revocation — key deactivation propagates immediately                                                  |    1    |    0    |     1      |
| Rate Limiting & Revocation                  | Rate limit status display in key management UI                                                                |    0    |    1    |     1      |
| **M9: Translation & Multilingual Support**  |                                                                                                               |         |         |            |
| Language Service Layer                      | Language-aware content serving API — resolve locale, return correct content version                           |    3    |    0    |     3      |
| Language Service Layer                      | Fallback chain — if content missing in requested language, serve primary with indicator                       |    2    |    0    |     2      |
| Language Service Layer                      | Language availability indicator — show which languages have content for a record                              |    1    |    2    |     3      |
| Language Service Layer                      | Language switcher integration — switch content language independently of UI language                          |    0    |    2    |     2      |
| Content Management                          | Content translation model — link base record to translated versions per language                              |    2    |    0    |     2      |
| Content Management                          | Translation status tracking — per-record, per-language status                                                 |    1    |    0    |     1      |
| Content Management                          | Content editing per locale — side-by-side original + translation, field-by-field                              |    1    |    3    |     4      |
| Content Management                          | Translation coverage dashboard — matrix of records × languages with completion %                              |    1    |    2    |     3      |
| Translation Workflow                        | Translator assignment — assign languages to translator users, workload view                                   |    2    |    2    |     4      |
| Translation Workflow                        | Translation task queue — pending items per translator, prioritization                                         |    1    |    1    |     2      |
| Translation Workflow                        | Review & publish translation — reviewer approval before translated content goes live                          |    2    |    1    |     3      |
| **M10: Dynamic Survey / Form Engine**       |                                                                                                               |         |         |            |
| Question Management UI                      | Question model — label, type, help text, order, section, active flag, validation rules                        |    2    |    0    |     2      |
| Question Management UI                      | QuestionSet / Form model — group questions, assign to domain (CBA, Pensions)                                  |    1    |    0    |     1      |
| Question Management UI                      | Question list management UI — table view, inline editing, status toggle                                       |    0    |    2    |     2      |
| Question Management UI                      | Add/edit question modal — all field types, validation config, help text                                       |    1    |    3    |     4      |
| Question Management UI                      | Drag-and-drop reordering — section-level and question-level ordering                                          |    0    |    2    |     2      |
| Question Management UI                      | Archive/restore questions — soft delete with impact notification                                              |    1    |    1    |     2      |
| Data Type Support                           | Input type implementations — text, number, date, boolean, free text (textarea)                                |    1    |    2    |     3      |
| Data Type Support                           | Selection types — single dropdown, multi-select, radio buttons, checkboxes                                    |    1    |    1    |     2      |
| Data Type Support                           | Answer option management — static lists, admin-editable choices per question                                  |    1    |    1    |     2      |
| Data Type Support                           | Validation engine — per-type rules (min/max, regex, required), custom validators                              |    1    |    0    |     1      |
| Required/Optional Flags                     | Required flag on question model, enforced in validation pipeline                                              |    1    |    0    |     1      |
| Required/Optional Flags                     | Conditional required — "required if Q_X is answered"                                                          |    1    |    0    |     1      |
| Required/Optional Flags                     | Visual indicators (asterisk, inline error) and admin toggle UI                                                |    0    |    2    |     2      |
| Conditional Visibility                      | VisibilityRule model — source question, operator, value, target question(s)                                   |    2    |    0    |     2      |
| Conditional Visibility                      | Rule evaluation engine — server-side validation that conditional questions are gated                          |    2    |    0    |     2      |
| Conditional Visibility                      | Visual rule builder UI — drag source question, select operator, set value, assign target                      |    0    |    5    |     5      |
| Conditional Visibility                      | Live preview — show/hide questions in real-time as rules are configured                                       |    0    |    3    |     3      |
| Conditional Visibility                      | Rule conflict detection — warn when rules contradict (circular dependencies)                                  |    2    |    2    |     4      |
| Nested Logic Support                        | AND/OR grouping model — rule groups with logical operators, arbitrary nesting depth                           |    2    |    0    |     2      |
| Nested Logic Support                        | Nested group evaluation engine — recursive condition resolution                                               |    2    |    0    |     2      |
| Nested Logic Support                        | Nested rule builder UI — add groups within groups, visual indentation, collapse/expand                        |    0    |    3    |     3      |
| Nested Logic Support                        | Depth limit enforcement and complexity warning                                                                |    1    |    1    |     2      |
| External API Dropdowns                      | External API connector model — endpoint URL, auth method, field mapping, cache TTL                            |    2    |    0    |     2      |
| External API Dropdowns                      | Proxy endpoint for external data — fetch, cache, normalize response                                           |    1    |    0    |     1      |
| External API Dropdowns                      | Admin configuration UI — specify endpoint, map response fields to option label/value                          |    0    |    2    |     2      |
| External API Dropdowns                      | Dynamic dropdown rendering — lazy-load options from proxy, search/filter                                      |    1    |    1    |     2      |
| Form Versioning                             | FormVersion model — snapshot of form definition on publish, version number, changelog                         |    2    |    0    |     2      |
| Form Versioning                             | Impact analysis — show how many collected responses reference each version                                    |    1    |    1    |     2      |
| Form Versioning                             | Version history and revert — list versions, diff, restore previous                                            |    1    |    1    |     2      |
| **M11: Unified API Gateway**                |                                                                                                               |         |         |            |
| API Design & Versioning                     | RESTful API design — endpoint naming, consistent response envelope, pagination standard                       |    2    |    0    |     2      |
| API Design & Versioning                     | API versioning strategy (URL path prefix: /api/v1/) with backward compat rules                                |    1    |    0    |     1      |
| API Design & Versioning                     | Shared serializers for all data domains with consistent field naming                                          |    2    |    0    |     2      |
| API Design & Versioning                     | Error response standardization — error codes, messages, field-level errors                                    |    1    |    0    |     1      |
| Per-Consumer Scoping                        | Consumer model — organization, contact, tier assignment, scope configuration                                  |    2    |    0    |     2      |
| Per-Consumer Scoping                        | Scope resolution middleware — API key → consumer → allowed datasets, countries, actions                       |    2    |    0    |     2      |
| Per-Consumer Scoping                        | Scope enforcement in querysets — automatic filtering based on resolved scope                                  |    1    |    0    |     1      |
| Rate Limiting                               | Tiered rate limit configuration — limits per tier (free/subscriber/partner)                                   |    1    |    0    |     1      |
| Rate Limiting                               | Django REST throttle classes with Redis-backed counters                                                       |    2    |    0    |     2      |
| Rate Limiting                               | Rate limit headers in responses (X-RateLimit-Remaining, X-RateLimit-Reset)                                    |    1    |    0    |     1      |
| Usage Analytics                             | Request logging model — consumer, endpoint, timestamp, response time, status code                             |    2    |    0    |     2      |
| Usage Analytics                             | Usage aggregation — daily/weekly/monthly totals per consumer, per endpoint                                    |    1    |    0    |     1      |
| Usage Analytics                             | Consumer usage dashboard — charts, top endpoints, quota utilization, time-series                              |    1    |    3    |     4      |
| Usage Analytics                             | Quota monitoring alerts — trigger notification at 80%/100% usage thresholds                                   |    0    |    1    |     1      |
| API Documentation                           | OpenAPI/Swagger spec auto-generation from Django REST serializers                                             |    1    |    0    |     1      |
| API Documentation                           | Swagger UI hosted at /api/docs/ with authentication support                                                   |    1    |    0    |     1      |
| API Documentation                           | Narrative API guide — getting started, authentication, pagination, examples                                   |    1    |    0    |     1      |
| **M12: LLM Query Interface**                |                                                                                                               |         |         |            |
| NL Query API                                | Query endpoint — accept text, language parameter; return structured answer + sources                          |    2    |    0    |     2      |
| NL Query API                                | RAG pipeline — retrieve relevant data chunks, inject context, generate response                               |    3    |    0    |     3      |
| NL Query API                                | Response formatting — structured JSON + natural language explanation + source citations                       |    1    |    0    |     1      |
| Restricted DB User                          | Dedicated PostgreSQL role with SELECT-only grants on approved tables                                          |    1    |    0    |     1      |
| Restricted DB User                          | Schema visibility restriction — hide internal tables, audit logs, user data                                   |    1    |    0    |     1      |
| Restricted DB User                          | Query execution sandbox — read-only connection pool with statement timeout                                    |    2    |    0    |     2      |
| Prompt Injection Guards                     | Input sanitization — strip injection patterns, detect adversarial prompts, length limits                      |    2    |    0    |     2      |
| Prompt Injection Guards                     | Output validation — detect data leakage, PII, off-topic responses before returning                            |    2    |    0    |     2      |
| Prompt Injection Guards                     | Context window restrictions — limit injected context to approved tables only                                  |    1    |    0    |     1      |
| Topic Boundary                              | Topic classifier — classify incoming query as in-scope / out-of-scope before LLM call                         |    2    |    0    |     2      |
| Topic Boundary                              | Approved topic registry — admin-configurable list of allowed topics/domains                                   |    1    |    0    |     1      |
| Topic Boundary                              | Out-of-scope response template — polite refusal with redirect to appropriate resource                         |    1    |    0    |     1      |
| Access Layer Integration                    | Authentication check — validate email/SMS registration or subscription before query                           |    2    |    0    |     2      |
| Access Layer Integration                    | Tier-based query limits — daily/monthly query caps per user tier                                              |    1    |    0    |     1      |
| Access Layer Integration                    | Query UI widget — input box, response display, source links, limit indicator                                  |    1    |    3    |     4      |
| Response Caching                            | Cache layer — Redis-based, keyed by normalized query + language + data version hash                           |    1    |    0    |     1      |
| Response Caching                            | Cache invalidation — trigger on data updates (publish events), TTL fallback                                   |    1    |    0    |     1      |
| Response Caching                            | Cache hit/miss monitoring and analytics                                                                       |    1    |    0    |     1      |
| **M13: Monitoring & Observability**         |                                                                                                               |         |         |            |
| Prometheus + Grafana                        | Prometheus setup with Docker Compose — Django metrics exporter, service discovery                             |    1    |    0    |     1      |
| Prometheus + Grafana                        | Grafana provisioning — datasource, default dashboards (system, Django, PG, Celery)                            |    1    |    0    |     1      |
| Prometheus + Grafana                        | Custom metrics — record counts per module, export volumes, LLM usage, queue depths                            |    1    |    0    |     1      |
| Alerting Rules                              | Security alerts — 403 spikes, failed login clusters, geo-anomalous access                                     |    1    |    0    |     1      |
| Alerting Rules                              | Application alerts — error rate thresholds, response time p95/p99, Celery queue backlog                       |    1    |    0    |     1      |
| Alerting Rules                              | Data pipeline alerts — migration failures, export anomalies, LLM API failures                                 |    1    |    0    |     1      |
| Alerting Rules                              | Alert routing — email + notification system integration, escalation rules                                     |    1    |    0    |     1      |
| Log Aggregation                             | Structured logging setup — JSON format, consistent fields (request_id, user_id, module)                       |    1    |    0    |     1      |
| Log Aggregation                             | Log aggregation stack — Loki or similar with Docker Compose, retention policies                               |    1    |    0    |     1      |
| Log Aggregation                             | Grafana log dashboard — search, filter, log-to-metric correlation                                             |    1    |    0    |     1      |
| Health Checks & SLA                         | Health check endpoints per service — /health/ with DB, Redis, Celery, storage checks                          |    1    |    0    |     1      |
| Health Checks & SLA                         | Uptime tracking — synthetic probes, availability calculation                                                  |    1    |    0    |     1      |
| Health Checks & SLA                         | SLA dashboard — uptime %, response time trends, incident timeline                                             |    1    |    0    |     1      |
| **M14: Security Hardening**                 |                                                                                                               |         |         |            |
| CI/CD Security Gates                        | SAST integration — Bandit for Python, ESLint security plugin for Vue.js, fail on critical                     |    2    |    0    |     2      |
| CI/CD Security Gates                        | Dependency scanning — pip-audit, npm audit; block merge on known critical CVEs                                |    1    |    0    |     1      |
| CI/CD Security Gates                        | Secret scanning — gitleaks in pre-commit hook + CI pipeline                                                   |    1    |    0    |     1      |
| CI/CD Security Gates                        | CI pipeline config — stage ordering, failure gates, bypass rules for false positives                          |    1    |    0    |     1      |
| Container Scanning                          | Trivy integration in build pipeline — scan base images + application image                                    |    1    |    0    |     1      |
| Container Scanning                          | Vulnerability suppression workflow — triage, document accepted risks, re-review cadence                       |    1    |    0    |     1      |
| Container Scanning                          | Base image policy — approved base images list, automated rebuild on upstream updates                          |    1    |    0    |     1      |
| DAST                                        | OWASP ZAP setup against staging environment — automated scan on deploy                                        |    1    |    0    |     1      |
| DAST                                        | ZAP scan profile tuning — auth handling, crawl scope, false positive suppression                              |    1    |    0    |     1      |
| DAST                                        | Advisory finding triage process — severity classification, sprint assignment                                  |    1    |    0    |     1      |
| Encryption Setup                            | TLS 1.2+ enforcement — reverse proxy config, HSTS headers, certificate management                             |    1    |    0    |     1      |
| Encryption Setup                            | Database encryption at rest — pgcrypto for sensitive fields (API keys, PII)                                   |    1    |    0    |     1      |
| Encryption Setup                            | Secrets management — environment-based injection, no secrets in code or config files                          |    1    |    0    |     1      |
| Encryption Setup                            | Backup encryption — AES-256 encrypted database backups                                                        |    1    |    0    |     1      |
| Incident Response                           | Runbooks — compromised API key, data leak, unauthorized access, DDoS response                                 |    1    |    0    |     1      |
| Incident Response                           | Incident severity classification and escalation matrix                                                        |    1    |    0    |     1      |
| Backup & Restore                            | Automated backup script — scheduled pg_dump, encrypted, offsite upload                                        |    1    |    0    |     1      |
| Backup & Restore                            | Restore drill — documented procedure, RTO/RPO validation test                                                 |    1    |    0    |     1      |
| **M15: Documentation & Handover**           |                                                                                                               |         |         |            |
| Architecture Docs                           | System architecture diagrams — component, deployment, data flow diagrams                                      |    2    |    0    |     2      |
| Architecture Docs                           | ADR (Architecture Decision Records) — consolidate all decisions made during project                           |    1    |    0    |     1      |
| Architecture Docs                           | Integration point documentation — external APIs, LLM provider, email service, OCR                             |    1    |    0    |     1      |
| API Documentation                           | Auto-generated OpenAPI spec — ensure all endpoints documented with examples                                   |    1    |    0    |     1      |
| API Documentation                           | Consumer onboarding guide — authentication, rate limits, pagination, code samples                             |    1    |    0    |     1      |
| API Documentation                           | Data dictionary — field definitions, types, enums, valid ranges for all API resources                         |    1    |    0    |     1      |
| Operational Runbooks                        | Deployment procedure — step-by-step for staging and production                                                |    1    |    0    |     1      |
| Operational Runbooks                        | Rollback procedure — DB rollback, application rollback, partial rollback                                      |    1    |    0    |     1      |
| Operational Runbooks                        | Scaling and maintenance guides — add capacity, rotate credentials, update dependencies                        |    1    |    0    |     1      |
| Admin User Guides                           | Admin panel walkthrough — screenshots, feature-by-feature guide                                               |    1    |    1    |     2      |
| Admin User Guides                           | Form engine admin guide — creating surveys, configuring rules, versioning                                     |    1    |    1    |     2      |
| Admin User Guides                           | Export configuration guide — setting up tiers, API keys, watermarking                                         |    0    |    1    |     1      |
| **TOTALS**                                  |                                                                                                               | **406** | **177** |  **583**   |
| **QA (25% of Dev)**                         |                                                                                                               |         |         |  **146**   |
| **GRAND TOTAL**                             |                                                                                                               |         |         |  **729**   |
