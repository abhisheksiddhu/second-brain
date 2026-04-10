# COBRA 2.0 — Detailed Estimates (All Tasks)

| Module | Sub-Component | Task # | Task Description | BE (PD) | FE (PD) | Total (PD) |
|--------|--------------|--------|-----------------|:-------:|:-------:|:----------:|
| M0: Discovery & Project Setup | Legacy Schema Audit | 0.1 | Map all COBRA databases, document table structures, row counts, relationships | 3 | 0 | 3 |
| M0: Discovery & Project Setup | Data Profiling | 0.2 | Catalogue 30+ Excel files in Dropbox, identify schemas, data quality issues | 2 | 0 | 2 |
| M0: Discovery & Project Setup | Schema Design | 0.3 | Unified PostgreSQL schema design — ERD, table definitions, normalization decisions, ADR | 3 | 0 | 3 |
| M0: Discovery & Project Setup | Infrastructure | 0.4 | Docker Compose setup, CI/CD pipelines, staging env on EU cloud | 2 | 0 | 2 |
| M0: Discovery & Project Setup | Dev Environment | 0.5 | docker-compose.yml, seed data scripts, .env templates, onboarding README | 1 | 0 | 1 |
| M0: Discovery & Project Setup | Security | 0.6 | STRIDE threat modeling — first-pass threat register, map mitigations to backlog | 1 | 0 | 1 |
| M0: Discovery & Project Setup | LLM Evaluation | 0.7 | Test 3-5 sample documents against candidate models, accuracy comparison | 3 | 0 | 3 |
| M0: Discovery & Project Setup | Sign-off | 0.8 | Tech stack confirmation, ADR documentation, team kickoff | 1 | 0 | 1 |
| M1: COBRA Core Platform | Unified DB Schema | 1.1.1 | PostgreSQL schema DDL — create all core tables, constraints, foreign keys | 3 | 0 | 3 |
| M1: COBRA Core Platform | Unified DB Schema | 1.1.2 | Django model definitions and migration files for core schema | 2 | 0 | 2 |
| M1: COBRA Core Platform | Unified DB Schema | 1.1.3 | Seed data — 180+ countries (ISO 3166), 75+ languages (ISO 639), currencies, regions | 2 | 0 | 2 |
| M1: COBRA Core Platform | Unified DB Schema | 1.1.4 | Database indexing strategy — composite indexes, partial indexes for common query patterns | 2 | 0 | 2 |
| M1: COBRA Core Platform | Unified DB Schema | 1.1.5 | Connection pooling (pgBouncer) and query performance baseline | 1 | 0 | 1 |
| M1: COBRA Core Platform | Core Data Models | 1.2.1 | Country model — ISO codes, region, sub-region, currency, metadata, active flag | 2 | 0 | 2 |
| M1: COBRA Core Platform | Core Data Models | 1.2.2 | Language model — locale code, script direction (LTR/RTL), fallback language chain | 2 | 0 | 2 |
| M1: COBRA Core Platform | Core Data Models | 1.2.3 | Shared reference models — Industry, Sector, OccupationCode (ISCO/ISIC classifications) | 2 | 0 | 2 |
| M1: COBRA Core Platform | Core Data Models | 1.2.4 | Base model mixins — TimestampMixin, SoftDeleteMixin, CountryScopedMixin, AuditableMixin | 2 | 0 | 2 |
| M1: COBRA Core Platform | Authentication | 1.3.1 | User registration endpoint with email verification (send link, confirm token) | 2 | 0 | 2 |
| M1: COBRA Core Platform | Authentication | 1.3.2 | Registration form — fields, client validation, email verification screen | 0 | 2 | 2 |
| M1: COBRA Core Platform | Authentication | 1.3.3 | Login endpoint — JWT access/refresh token pair, session cookie option | 1 | 0 | 1 |
| M1: COBRA Core Platform | Authentication | 1.3.4 | Login page — form, error handling, redirect to dashboard | 0 | 1 | 1 |
| M1: COBRA Core Platform | Authentication | 1.3.5 | Forgot password — generate reset token, send email, validate & reset | 1 | 0 | 1 |
| M1: COBRA Core Platform | Authentication | 1.3.6 | Reset password page — token validation, new password form, confirmation | 0 | 1 | 1 |
| M1: COBRA Core Platform | Authentication | 1.3.7 | Password policy enforcement (min length, complexity rules, breach check) | 1 | 0 | 1 |
| M1: COBRA Core Platform | Authentication | 1.3.8 | Logout, token refresh, session invalidation on password change | 0 | 1 | 1 |
| M1: COBRA Core Platform | Custom RBAC Engine | 1.4.1 | Permission model — module × action matrix (view, create, edit, delete, publish, export per module) | 2 | 0 | 2 |
| M1: COBRA Core Platform | Custom RBAC Engine | 1.4.2 | Role model with M2M relationship to permissions; role metadata (name, description, is_default) | 1 | 0 | 1 |
| M1: COBRA Core Platform | Custom RBAC Engine | 1.4.3 | Role CRUD API — create, update, clone, archive roles; prevent deletion of in-use roles | 2 | 0 | 2 |
| M1: COBRA Core Platform | Custom RBAC Engine | 1.4.4 | Permission matrix UI — grid of modules vs. actions; toggle permissions per role; bulk select | 0 | 4 | 4 |
| M1: COBRA Core Platform | Custom RBAC Engine | 1.4.5 | 6 default role templates seeded on first run (Admin, Data Manager, Annotator, Reviewer, API Consumer, Viewer) | 1 | 0 | 1 |
| M1: COBRA Core Platform | Custom RBAC Engine | 1.4.6 | Permission-checking middleware — decorator-based endpoint protection; 403 on violation | 2 | 0 | 2 |
| M1: COBRA Core Platform | Custom RBAC Engine | 1.4.7 | User → Role assignment UI — assign/revoke roles per user; bulk assignment | 1 | 2 | 3 |
| M1: COBRA Core Platform | Custom RBAC Engine | 1.4.8 | Permission-aware frontend rendering — hide/disable unauthorized menu items, buttons, routes | 0 | 1 | 1 |
| M1: COBRA Core Platform | Custom RBAC Engine | 1.4.9 | Role change propagation — invalidate cached permissions on role update | 1 | 0 | 1 |
| M1: COBRA Core Platform | Admin Panel Shell | 1.5.1 | Admin layout shell — sidebar navigation, header bar, breadcrumbs, responsive design | 0 | 3 | 3 |
| M1: COBRA Core Platform | Admin Panel Shell | 1.5.2 | Dashboard page — system stats, recent activity feed, quick action cards | 2 | 3 | 5 |
| M1: COBRA Core Platform | Admin Panel Shell | 1.5.3 | User management screens — list, create, edit, deactivate, view assigned roles/countries | 2 | 3 | 5 |
| M1: COBRA Core Platform | Admin Panel Shell | 1.5.4 | System settings — site configuration, feature toggles, maintenance mode, email settings | 1 | 2 | 3 |
| M1: COBRA Core Platform | Admin Panel Shell | 1.5.5 | Reusable Vue components — data tables with sort/filter/pagination, form controls, modals, toasts | 0 | 1 | 1 |
| M1: COBRA Core Platform | Admin Panel Shell | 1.5.6 | Django Admin customizations for superuser-only operations (raw model access) | 1 | 0 | 1 |
| M1: COBRA Core Platform | Audit Logging (Basic) | 1.6.1 | AuditLog model — user, action, resource type, resource ID, timestamp, IP address | 1 | 0 | 1 |
| M1: COBRA Core Platform | Audit Logging (Basic) | 1.6.2 | Middleware for automatic audit log creation on API requests (POST, PUT, PATCH, DELETE) | 2 | 0 | 2 |
| M1: COBRA Core Platform | Audit Logging (Basic) | 1.6.3 | Log export (CSV) for compliance | 1 | 0 | 1 |
| M1: COBRA Core Platform | Audit Logging (Basic) | 1.6.4 | Audit log viewer — filterable table (user, action, date range, module), paginated | 0 | 2 | 2 |
| M1: COBRA Core Platform | Country-Scoped Access | 1.7.1 | UserCountryAssignment M2M model — assign users to one or more countries | 1 | 0 | 1 |
| M1: COBRA Core Platform | Country-Scoped Access | 1.7.2 | QuerySet manager with automatic country filtering (all model queries scoped to user's countries) | 2 | 0 | 2 |
| M1: COBRA Core Platform | Country-Scoped Access | 1.7.3 | Admin UI for assigning countries to users (multi-select, bulk assign) | 1 | 1 | 2 |
| M1: COBRA Core Platform | Country-Scoped Access | 1.7.4 | Country context switcher — header dropdown to select active country, persisted in session | 0 | 2 | 2 |
| M1: COBRA Core Platform | Country-Scoped Access | 1.7.5 | Module-scoped permission extension — combine country scope + role permissions in access checks | 1 | 0 | 1 |
| M1: COBRA Core Platform | Multi-Language Framework | 1.8.1 | Translation key registry — model for managing translation strings, namespaced by module | 2 | 0 | 2 |
| M1: COBRA Core Platform | Multi-Language Framework | 1.8.2 | 70-language locale file management — JSON/PO file structure, tooling for import/export | 2 | 0 | 2 |
| M1: COBRA Core Platform | Multi-Language Framework | 1.8.3 | Locale detection middleware — Accept-Language header, user preference, URL prefix fallback | 2 | 0 | 2 |
| M1: COBRA Core Platform | Multi-Language Framework | 1.8.4 | Vue i18n integration — plugin setup, lazy-loaded locale bundles, pluralization rules | 0 | 3 | 3 |
| M1: COBRA Core Platform | Multi-Language Framework | 1.8.5 | Translation import/export CLI — manage.py commands for syncing locale files | 2 | 0 | 2 |
| M1: COBRA Core Platform | Multi-Language Framework | 1.8.6 | Locale selector component — dropdown in header, persists preference to user profile | 0 | 2 | 2 |
| M1: COBRA Core Platform | Notification System | 1.9.1 | Notification model — type, recipient, title, message, read/unread, created_at, action_url | 1 | 0 | 1 |
| M1: COBRA Core Platform | Notification System | 1.9.2 | Email notification service — Django template-based emails, SMTP/SES integration, async via Celery | 2 | 0 | 2 |
| M1: COBRA Core Platform | Notification System | 1.9.3 | In-app notification API — list, mark-as-read, mark-all-read, unread count | 1 | 0 | 1 |
| M1: COBRA Core Platform | Notification System | 1.9.4 | Notification center UI — bell icon with unread badge, dropdown panel, click-through to source | 0 | 3 | 3 |
| M1: COBRA Core Platform | Notification System | 1.9.5 | User notification preferences — per-event-type opt-in/out (email, in-app toggles) | 1 | 2 | 3 |
| M2: Labour Law Database | Data Models | 2.1.1 | Django models for law categories — minimum wages, working hours, leave, termination, social security | 2 | 0 | 2 |
| M2: Labour Law Database | Data Models | 2.1.2 | Temporal validity fields — effective_from, effective_to, legislative_reference, gazette_url | 1 | 0 | 1 |
| M2: Labour Law Database | Data Models | 2.1.3 | Country-specific field configuration — JSONField schema per country for flexible field sets | 1 | 0 | 1 |
| M2: Labour Law Database | Data Models | 2.1.4 | Model serializers with field-level validation rules | 1 | 0 | 1 |
| M2: Labour Law Database | Structured Data Entry UI | 2.2.1 | Dynamic form renderer — load country-specific field config, render appropriate input types | 1 | 3 | 4 |
| M2: Labour Law Database | Structured Data Entry UI | 2.2.2 | Client + server-side validation — required fields, data type checks, cross-field rules | 1 | 1 | 2 |
| M2: Labour Law Database | Structured Data Entry UI | 2.2.3 | Country context switching — changing country reloads field config and existing records | 1 | 2 | 3 |
| M2: Labour Law Database | Structured Data Entry UI | 2.2.4 | Draft auto-save — periodic save to prevent data loss, explicit save button | 1 | 1 | 2 |
| M2: Labour Law Database | Structured Data Entry UI | 2.2.5 | Inline help — field-level tooltips with guidance text from admin configuration | 1 | 1 | 2 |
| M2: Labour Law Database | Version-Controlled Records | 2.3.1 | RecordVersion model — full JSON snapshot of record on each save, version number, author | 2 | 0 | 2 |
| M2: Labour Law Database | Version-Controlled Records | 2.3.2 | Version history API — list versions, retrieve specific version | 1 | 0 | 1 |
| M2: Labour Law Database | Version-Controlled Records | 2.3.3 | Version history list view — table of versions with date, author, action | 0 | 1 | 1 |
| M2: Labour Law Database | Version-Controlled Records | 2.3.4 | Side-by-side diff view — highlight field differences between two selected versions | 1 | 1 | 2 |
| M2: Labour Law Database | Version-Controlled Records | 2.3.5 | Rollback to version — restore previous snapshot with confirmation dialog, creates new version | 1 | 1 | 2 |
| M2: Labour Law Database | Publishing Workflow | 2.4.1 | Workflow state machine — Draft → Under Review → Published, with transition validation | 2 | 0 | 2 |
| M2: Labour Law Database | Publishing Workflow | 2.4.2 | Role-gated transitions — only Reviewers/Admins can approve; Annotators submit for review | 1 | 0 | 1 |
| M2: Labour Law Database | Publishing Workflow | 2.4.3 | Status transition UI — status badge, action buttons per state, comment on transition | 1 | 2 | 3 |
| M2: Labour Law Database | Publishing Workflow | 2.4.4 | Publishing history log — track all state changes with timestamp, actor, comment | 1 | 1 | 2 |
| M2: Labour Law Database | Publishing Workflow | 2.4.5 | Notification trigger — send email + in-app notification on review request / approval / rejection | 0 | 1 | 1 |
| M2: Labour Law Database | Country-Scoped Management | 2.5.1 | Extend core country-scoping to labour law API views and querysets | 2 | 0 | 2 |
| M2: Labour Law Database | Country-Scoped Management | 2.5.2 | Country filter in labour law list view — dropdown, persisted selection | 0 | 1 | 1 |
| M2: Labour Law Database | Country-Scoped Management | 2.5.3 | Bulk operations scoped by country — bulk publish, bulk assign reviewer | 1 | 1 | 2 |
| M2: Labour Law Database | Search & Retrieval (PG FTS) | 2.6.1 | PostgreSQL tsvector setup — GIN indexes, search configuration per language | 2 | 0 | 2 |
| M2: Labour Law Database | Search & Retrieval (PG FTS) | 2.6.2 | Search API — full-text query with filters (country, category, date range, status) | 1 | 0 | 1 |
| M2: Labour Law Database | Search & Retrieval (PG FTS) | 2.6.3 | Search UI — search bar, filter panel, results list with highlighting, pagination | 0 | 2 | 2 |
| M2: Labour Law Database | Search & Retrieval (PG FTS) | 2.6.4 | Sort options — relevance, date, country | 0 | 1 | 1 |
| M2: Labour Law Database | Legacy Migration Scripts | 2.7.1 | Analyze legacy labour law DB schema — document tables, columns, types, encoding | 1 | 0 | 1 |
| M2: Labour Law Database | Legacy Migration Scripts | 2.7.2 | Write ETL scripts — transform legacy rows into unified schema format | 2 | 0 | 2 |
| M2: Labour Law Database | Legacy Migration Scripts | 2.7.3 | Data validation — row-count checks, referential integrity, null handling | 1 | 0 | 1 |
| M2: Labour Law Database | Legacy Migration Scripts | 2.7.4 | Migration dry-run on staging with reconciliation report | 1 | 0 | 1 |
| M3: International Law DB | Content Schema & Models | 3.1.1 | Models for international conventions, ILO standards, treaty records | 2 | 0 | 2 |
| M3: International Law DB | Content Schema & Models | 3.1.2 | Ratification status model — country × convention with ratification date, status | 1 | 0 | 1 |
| M3: International Law DB | Content Schema & Models | 3.1.3 | Serializers and API endpoints | 1 | 0 | 1 |
| M3: International Law DB | Data Entry UI Adaptation | 3.2.1 | Adapt Module 2 form components with international law field configuration | 1 | 2 | 3 |
| M3: International Law DB | Data Entry UI Adaptation | 3.2.2 | Convention selector — searchable dropdown of ILO conventions / treaties | 1 | 1 | 2 |
| M3: International Law DB | Data Entry UI Adaptation | 3.2.3 | Cross-country applicability view — which countries ratified which convention | 1 | 1 | 2 |
| M3: International Law DB | Domain Business Rules | 3.3.1 | Ratification tracking logic — track status changes, effective dates | 1 | 0 | 1 |
| M3: International Law DB | Domain Business Rules | 3.3.2 | Applicability mapping — link international conventions to national labour law records | 1 | 1 | 2 |
| M3: International Law DB | Domain Business Rules | 3.3.3 | Validation rules specific to international law records | 1 | 1 | 2 |
| M3: International Law DB | Legacy Data Migration | 3.4.1 | Analyze legacy international law schema | 1 | 0 | 1 |
| M3: International Law DB | Legacy Data Migration | 3.4.2 | Write transformation scripts into unified schema | 2 | 0 | 2 |
| M3: International Law DB | Legacy Data Migration | 3.4.3 | Validation and staging dry-run | 1 | 0 | 1 |
| M4: CBA Processing Engine | Document Ingestion | 4.1.1 | Upload API — accept PDF, DOCX; file type validation, size limits, virus scanning (ClamAV) | 2 | 0 | 2 |
| M4: CBA Processing Engine | Document Ingestion | 4.1.2 | Upload UI — drag-and-drop zone, progress indicator, file list, metadata form | 0 | 3 | 3 |
| M4: CBA Processing Engine | Document Ingestion | 4.1.3 | File storage abstraction — local/S3-compatible, organized by country/year | 1 | 0 | 1 |
| M4: CBA Processing Engine | Document Ingestion | 4.1.4 | Document metadata extraction on upload — page count, language detection, file hash | 1 | 0 | 1 |
| M4: CBA Processing Engine | Document Ingestion | 4.1.5 | Upload validation error handling — clear error messages, retry option | 1 | 1 | 2 |
| M4: CBA Processing Engine | OCR for Scanned PDFs | 4.2.1 | OCR pipeline integration — Tesseract or cloud OCR service for image-based PDFs | 2 | 0 | 2 |
| M4: CBA Processing Engine | OCR for Scanned PDFs | 4.2.2 | Scanned PDF detection — heuristic to distinguish text-based vs. image-based pages | 1 | 0 | 1 |
| M4: CBA Processing Engine | OCR for Scanned PDFs | 4.2.3 | OCR output normalization — clean extracted text, preserve page structure | 1 | 0 | 1 |
| M4: CBA Processing Engine | AI Document Conversion | 4.3.1 | PDF→text extraction pipeline — handle multi-column, tables, headers, footnotes | 3 | 0 | 3 |
| M4: CBA Processing Engine | AI Document Conversion | 4.3.2 | DOCX→structured HTML conversion — preserve formatting, lists, tables | 2 | 0 | 2 |
| M4: CBA Processing Engine | AI Document Conversion | 4.3.3 | LLM-assisted structure detection — identify sections, articles, clauses using single LLM provider | 3 | 0 | 3 |
| M4: CBA Processing Engine | Structured Data Extraction | 4.4.1 | CBA data model field extraction — parties, effective dates, industry, coverage scope | 3 | 0 | 3 |
| M4: CBA Processing Engine | Structured Data Extraction | 4.4.2 | Extraction prompt engineering — per-field prompts with few-shot examples | 2 | 0 | 2 |
| M4: CBA Processing Engine | Structured Data Extraction | 4.4.3 | Extraction output validation — type checking, range validation, mandatory field enforcement | 1 | 0 | 1 |
| M4: CBA Processing Engine | HTML Cleanup & Formatting | 4.5.1 | HTML sanitization — strip unsafe tags, normalize structure, fix encoding | 2 | 0 | 2 |
| M4: CBA Processing Engine | HTML Cleanup & Formatting | 4.5.2 | Heading hierarchy enforcement — auto-correct heading levels, generate TOC | 1 | 0 | 1 |
| M4: CBA Processing Engine | HTML Cleanup & Formatting | 4.5.3 | Table and list normalization — consistent HTML structure for downstream consumption | 1 | 0 | 1 |
| M4: CBA Processing Engine | Editor Review (HITL) | 4.6.1 | Review queue API — list pending documents, assignment, lock-on-open to prevent conflicts | 2 | 0 | 2 |
| M4: CBA Processing Engine | Editor Review (HITL) | 4.6.2 | Side-by-side viewer — original document (PDF viewer) alongside converted HTML | 0 | 3 | 3 |
| M4: CBA Processing Engine | Editor Review (HITL) | 4.6.3 | Inline HTML editor — rich text editing of converted output, section-level accept/reject | 0 | 3 | 3 |
| M4: CBA Processing Engine | Editor Review (HITL) | 4.6.4 | Approve / reject / request re-conversion workflow with comments | 2 | 1 | 3 |
| M4: CBA Processing Engine | CBA Metadata Management | 4.7.1 | CBA metadata model — parties, dates, coverage, industry (ISIC), region, legal status | 2 | 0 | 2 |
| M4: CBA Processing Engine | CBA Metadata Management | 4.7.2 | Metadata entry form — pre-filled from AI extraction, editable by annotator | 1 | 3 | 4 |
| M4: CBA Processing Engine | CBA Metadata Management | 4.7.3 | Metadata validation rules — date logic, mandatory fields per status | 1 | 1 | 2 |
| M4: CBA Processing Engine | Legacy CBA Migration | 4.8.1 | Analyze legacy CBA schema and document storage structure | 1 | 0 | 1 |
| M4: CBA Processing Engine | Legacy CBA Migration | 4.8.2 | Migration scripts — transform legacy CBA data into unified schema | 2 | 0 | 2 |
| M4: CBA Processing Engine | Legacy CBA Migration | 4.8.3 | File migration — move legacy documents to new storage structure | 1 | 0 | 1 |
| M4: CBA Processing Engine | Legacy CBA Migration | 4.8.4 | Validation and staging reconciliation | 1 | 0 | 1 |
| M5: AI Annotation Pipeline | LLM Integration Layer | 5.1.1 | Single LLM provider client — API wrapper with retry, timeout, error handling | 2 | 0 | 2 |
| M5: AI Annotation Pipeline | LLM Integration Layer | 5.1.2 | Token usage tracking and cost monitoring per request | 1 | 0 | 1 |
| M5: AI Annotation Pipeline | LLM Integration Layer | 5.1.3 | EU data residency compliance validation — ensure no data leaves EU boundary | 1 | 0 | 1 |
| M5: AI Annotation Pipeline | Document Embedding | 5.2.1 | Document chunking strategy — split by sections/paragraphs, respect semantic boundaries | 2 | 0 | 2 |
| M5: AI Annotation Pipeline | Document Embedding | 5.2.2 | Vector store setup — pgvector or similar, embedding generation for document chunks | 2 | 0 | 2 |
| M5: AI Annotation Pipeline | Document Embedding | 5.2.3 | Semantic similarity retrieval — query similar document sections for context injection | 1 | 0 | 1 |
| M5: AI Annotation Pipeline | LLM-Powered Extraction | 5.3.1 | Prompt templates per document type — CBA, labour law, international convention | 2 | 0 | 2 |
| M5: AI Annotation Pipeline | LLM-Powered Extraction | 5.3.2 | Few-shot example management — maintain curated examples per document type/language | 2 | 0 | 2 |
| M5: AI Annotation Pipeline | LLM-Powered Extraction | 5.3.3 | Extraction pipeline — chain prompts, parse structured output, handle partial failures | 2 | 0 | 2 |
| M5: AI Annotation Pipeline | Confidence Scoring | 5.4.1 | Per-field confidence score computation — LLM self-assessment + heuristic validation | 2 | 0 | 2 |
| M5: AI Annotation Pipeline | Confidence Scoring | 5.4.2 | Configurable thresholds — auto-accept above X%, mandatory review below Y% | 1 | 0 | 1 |
| M5: AI Annotation Pipeline | Confidence Scoring | 5.4.3 | Confidence score display in UI — color-coded indicators per field (green/yellow/red) | 0 | 2 | 2 |
| M5: AI Annotation Pipeline | Confidence Scoring | 5.4.4 | Threshold configuration admin screen | 1 | 1 | 2 |
| M5: AI Annotation Pipeline | HITL Review Queue | 5.5.1 | Review queue model — items, assignment, priority, status (pending/in-review/approved/rejected) | 2 | 0 | 2 |
| M5: AI Annotation Pipeline | HITL Review Queue | 5.5.2 | Queue list view — sortable by confidence, date, language; filter by status, assignee | 0 | 2 | 2 |
| M5: AI Annotation Pipeline | HITL Review Queue | 5.5.3 | Field-level review UI — accept/reject individual extracted fields, edit inline, add comments | 0 | 4 | 4 |
| M5: AI Annotation Pipeline | HITL Review Queue | 5.5.4 | Batch operations — bulk approve high-confidence items, bulk assign to reviewer | 2 | 1 | 3 |
| M5: AI Annotation Pipeline | HITL Review Queue | 5.5.5 | Annotation history — full trail of extraction → review → correction per field | 1 | 1 | 2 |
| M5: AI Annotation Pipeline | Model Evaluation | 5.6.1 | Ground truth dataset management — curated annotated documents for accuracy measurement | 2 | 0 | 2 |
| M5: AI Annotation Pipeline | Model Evaluation | 5.6.2 | Accuracy metrics computation — precision, recall, F1 per field type, per language | 2 | 0 | 2 |
| M5: AI Annotation Pipeline | Model Evaluation | 5.6.3 | Evaluation dashboard — accuracy trends over time, per-field breakdown, comparison charts | 1 | 3 | 4 |
| M6: Pensions Database | Pensions Data Models | 6.1.1 | Models — pension schemes, benefit types, eligibility criteria, contribution rates | 2 | 0 | 2 |
| M6: Pensions Database | Pensions Data Models | 6.1.2 | Country-specific pension variations — scheme subtypes, regional rules | 1 | 0 | 1 |
| M6: Pensions Database | Pensions Data Models | 6.1.3 | Serializers and validation | 1 | 0 | 1 |
| M6: Pensions Database | Survey Integration | 6.2.1 | Wire pensions questionnaire definitions to form engine API | 1 | 0 | 1 |
| M6: Pensions Database | Survey Integration | 6.2.2 | Data binding — map survey responses to pensions data models | 1 | 0 | 1 |
| M6: Pensions Database | Survey Integration | 6.2.3 | Survey rendering within pensions module context | 0 | 2 | 2 |
| M6: Pensions Database | Survey Integration | 6.2.4 | Response submission and storage pipeline | 1 | 1 | 2 |
| M6: Pensions Database | Country-Scoped Entry | 6.3.1 | Country context selection — filter schemes by selected country | 1 | 1 | 2 |
| M6: Pensions Database | Country-Scoped Entry | 6.3.2 | Regional pension scheme variations — sub-national scheme support | 1 | 1 | 2 |
| M6: Pensions Database | Publishing Workflow | 6.4.1 | Reuse Module 2 workflow engine — configure for pensions domain | 2 | 0 | 2 |
| M6: Pensions Database | Publishing Workflow | 6.4.2 | Pensions-specific review rules — mandatory field checks before submission | 1 | 0 | 1 |
| M6: Pensions Database | Publishing Workflow | 6.4.3 | Status management UI — reuse workflow components from Module 2 | 0 | 2 | 2 |
| M6: Pensions Database | Publishing Workflow | 6.4.4 | Notification integration — review/approval alerts for pensions records | 1 | 1 | 2 |
| M6: Pensions Database | Legacy Migration | 6.5.1 | Analyze legacy pensions data structure | 1 | 0 | 1 |
| M6: Pensions Database | Legacy Migration | 6.5.2 | Write migration scripts | 2 | 0 | 2 |
| M6: Pensions Database | Legacy Migration | 6.5.3 | Validation and staging dry-run | 1 | 0 | 1 |
| M7: Data Migration | Schema Analysis & Mapping | 7.1.1 | Document all source schemas — legacy CBA, Labour Law, Int'l Law, Pensions databases | 3 | 0 | 3 |
| M7: Data Migration | Schema Analysis & Mapping | 7.1.2 | Field mapping matrix — source column → target column, data type conversions, encoding fixes | 3 | 0 | 3 |
| M7: Data Migration | Schema Analysis & Mapping | 7.1.3 | Data quality assessment — null rates, duplicate detection, inconsistency report per source | 2 | 0 | 2 |
| M7: Data Migration | DB Unification Scripts | 7.2.1 | CBA database migration script — transform & load into unified schema | 3 | 0 | 3 |
| M7: Data Migration | DB Unification Scripts | 7.2.2 | Labour Law database migration script | 3 | 0 | 3 |
| M7: Data Migration | DB Unification Scripts | 7.2.3 | International Law database migration script | 2 | 0 | 2 |
| M7: Data Migration | DB Unification Scripts | 7.2.4 | Pensions database migration script | 2 | 0 | 2 |
| M7: Data Migration | DB Unification Scripts | 7.2.5 | Cross-database reference resolution — link records across domains | 2 | 0 | 2 |
| M7: Data Migration | Excel/Dropbox Ingestion | 7.3.1 | Excel parser framework — handle varying formats, sheet structures, merged cells across 30+ files | 3 | 0 | 3 |
| M7: Data Migration | Excel/Dropbox Ingestion | 7.3.2 | Per-file ingestion scripts with field mapping and transformation rules | 4 | 0 | 4 |
| M7: Data Migration | Excel/Dropbox Ingestion | 7.3.3 | Data normalization — standardize country names, date formats, encoding, reference codes | 2 | 0 | 2 |
| M7: Data Migration | Excel/Dropbox Ingestion | 7.3.4 | Error handling — skip vs. quarantine bad rows, generate exception report | 1 | 0 | 1 |
| M7: Data Migration | Validation & Reconciliation | 7.4.1 | Row-count reconciliation — source vs. target totals per table, per domain | 2 | 0 | 2 |
| M7: Data Migration | Validation & Reconciliation | 7.4.2 | Referential integrity checks — orphaned records, broken foreign keys | 2 | 0 | 2 |
| M7: Data Migration | Validation & Reconciliation | 7.4.3 | Data quality scoring — completeness, consistency, accuracy metrics per domain | 2 | 0 | 2 |
| M7: Data Migration | Validation & Reconciliation | 7.4.4 | Exception handling — quarantine queue for records failing validation | 2 | 0 | 2 |
| M7: Data Migration | Validation & Reconciliation | 7.4.5 | Validation dashboard — progress tracker, error summary, data quality charts, drill-down | 0 | 5 | 5 |
| M7: Data Migration | Rollback Capability | 7.5.1 | Staged migration with named checkpoints — can resume from last successful stage | 2 | 0 | 2 |
| M7: Data Migration | Rollback Capability | 7.5.2 | Pre-migration database snapshot automation — pg_dump before each stage | 1 | 0 | 1 |
| M7: Data Migration | Rollback Capability | 7.5.3 | Rollback script — restore to any checkpoint with referential integrity | 2 | 0 | 2 |
| M7: Data Migration | Migration Reporting | 7.6.1 | Migration run model — track jobs, stages, timing, status, error counts | 1 | 0 | 1 |
| M7: Data Migration | Migration Reporting | 7.6.2 | Progress dashboard — per-domain progress bars, row counts, stage status | 1 | 3 | 4 |
| M7: Data Migration | Migration Reporting | 7.6.3 | Sign-off workflow — domain-level sign-off by data manager, audit trail | 1 | 2 | 3 |
| M8: Export & Distribution | Tiered Export Framework | 8.1.1 | ExportProfile model — tier name, field inclusion list, format options, aggregation rules | 2 | 0 | 2 |
| M8: Export & Distribution | Tiered Export Framework | 8.1.2 | Profile configuration admin UI — create/edit tiers, assign field sets, preview output | 1 | 3 | 4 |
| M8: Export & Distribution | Tiered Export Framework | 8.1.3 | Export generation engine — serialize data per profile, output CSV/JSON/XLSX | 2 | 0 | 2 |
| M8: Export & Distribution | Tiered Export Framework | 8.1.4 | Async export job queue — Celery task for large exports, download-ready notification | 1 | 1 | 2 |
| M8: Export & Distribution | Field-Level Filtering | 8.2.1 | Dynamic serializer — resolve API key → tier → included fields at runtime | 2 | 0 | 2 |
| M8: Export & Distribution | Field-Level Filtering | 8.2.2 | Field whitelist/blacklist configuration per tier | 1 | 1 | 2 |
| M8: Export & Distribution | Field-Level Filtering | 8.2.3 | Nested field handling — control depth of related objects in output | 1 | 1 | 2 |
| M8: Export & Distribution | Aggregation Enforcement | 8.3.1 | Free-tier aggregation layer — compute averages, counts, ranges instead of raw records | 2 | 0 | 2 |
| M8: Export & Distribution | Aggregation Enforcement | 8.3.2 | Aggregation rule configuration — per-field aggregation type, grouping dimensions | 1 | 0 | 1 |
| M8: Export & Distribution | Aggregation Enforcement | 8.3.3 | Tier-check middleware — block raw record access for free-tier keys | 1 | 0 | 1 |
| M8: Export & Distribution | Statistical Watermarking | 8.4.1 | Row-ordering permutation algorithm — deterministic per-consumer seed | 2 | 0 | 2 |
| M8: Export & Distribution | Statistical Watermarking | 8.4.2 | Watermark embedding on export — transparent to consumer, detectable by WageIndicator | 1 | 0 | 1 |
| M8: Export & Distribution | Statistical Watermarking | 8.4.3 | Leak detection utility — given leaked data, identify originating API key | 1 | 0 | 1 |
| M8: Export & Distribution | Bulk Export Approval | 8.5.1 | Configurable export threshold — row count / data volume trigger for approval requirement | 1 | 0 | 1 |
| M8: Export & Distribution | Bulk Export Approval | 8.5.2 | Approval queue model — pending exports, assigned approver, status | 1 | 0 | 1 |
| M8: Export & Distribution | Bulk Export Approval | 8.5.3 | Approval UI — review export params, preview sample, approve/reject with comment | 1 | 3 | 4 |
| M8: Export & Distribution | Bulk Export Approval | 8.5.4 | Post-approval file generation and download link with expiry | 1 | 1 | 2 |
| M8: Export & Distribution | API Key Management | 8.6.1 | APIKey model — key hash, consumer, tier, scoped datasets, scoped countries, active flag | 2 | 0 | 2 |
| M8: Export & Distribution | API Key Management | 8.6.2 | Key lifecycle API — issue, rotate, revoke; key shown once on creation | 1 | 0 | 1 |
| M8: Export & Distribution | API Key Management | 8.6.3 | Key management admin UI — list keys, filter by consumer/tier, rotate, revoke, view usage | 1 | 3 | 4 |
| M8: Export & Distribution | API Key Management | 8.6.4 | Key authentication middleware — validate, resolve tier, inject scoping | 1 | 1 | 2 |
| M8: Export & Distribution | Rate Limiting & Revocation | 8.7.1 | Per-consumer rate limit configuration — tiered limits stored with API key | 1 | 0 | 1 |
| M8: Export & Distribution | Rate Limiting & Revocation | 8.7.2 | Django throttle layer — token bucket implementation with Redis backend | 2 | 0 | 2 |
| M8: Export & Distribution | Rate Limiting & Revocation | 8.7.3 | Instant revocation — key deactivation propagates immediately | 1 | 0 | 1 |
| M8: Export & Distribution | Rate Limiting & Revocation | 8.7.4 | Rate limit status display in key management UI | 0 | 1 | 1 |
| M9: Translation & Multilingual | Language Service Layer | 9.1.1 | Language-aware content serving API — resolve locale, return correct content version | 3 | 0 | 3 |
| M9: Translation & Multilingual | Language Service Layer | 9.1.2 | Fallback chain — if content missing in requested language, serve primary with indicator | 2 | 0 | 2 |
| M9: Translation & Multilingual | Language Service Layer | 9.1.3 | Language availability indicator — show which languages have content for a record | 1 | 2 | 3 |
| M9: Translation & Multilingual | Language Service Layer | 9.1.4 | Language switcher integration — switch content language independently of UI language | 0 | 2 | 2 |
| M9: Translation & Multilingual | Content Management | 9.2.1 | Content translation model — link base record to translated versions per language | 2 | 0 | 2 |
| M9: Translation & Multilingual | Content Management | 9.2.2 | Translation status tracking — per-record, per-language status | 1 | 0 | 1 |
| M9: Translation & Multilingual | Content Management | 9.2.3 | Content editing per locale — side-by-side original + translation, field-by-field | 1 | 3 | 4 |
| M9: Translation & Multilingual | Content Management | 9.2.4 | Translation coverage dashboard — matrix of records × languages with completion % | 1 | 2 | 3 |
| M9: Translation & Multilingual | Translation Workflow | 9.3.1 | Translator assignment — assign languages to translator users, workload view | 2 | 2 | 4 |
| M9: Translation & Multilingual | Translation Workflow | 9.3.2 | Translation task queue — pending items per translator, prioritization | 1 | 1 | 2 |
| M9: Translation & Multilingual | Translation Workflow | 9.3.3 | Review & publish translation — reviewer approval before translated content goes live | 2 | 1 | 3 |
| M10: Form Engine | Question Management UI | 10.1.1 | Question model — label, type, help text, order, section, active flag, validation rules | 2 | 0 | 2 |
| M10: Form Engine | Question Management UI | 10.1.2 | QuestionSet / Form model — group questions, assign to domain (CBA, Pensions) | 1 | 0 | 1 |
| M10: Form Engine | Question Management UI | 10.1.3 | Question list management UI — table view, inline editing, status toggle | 0 | 2 | 2 |
| M10: Form Engine | Question Management UI | 10.1.4 | Add/edit question modal — all field types, validation config, help text | 1 | 3 | 4 |
| M10: Form Engine | Question Management UI | 10.1.5 | Drag-and-drop reordering — section-level and question-level ordering | 0 | 2 | 2 |
| M10: Form Engine | Question Management UI | 10.1.6 | Archive/restore questions — soft delete with impact notification | 1 | 1 | 2 |
| M10: Form Engine | Data Type Support | 10.2.1 | Input type implementations — text, number, date, boolean, free text (textarea) | 1 | 2 | 3 |
| M10: Form Engine | Data Type Support | 10.2.2 | Selection types — single dropdown, multi-select, radio buttons, checkboxes | 1 | 1 | 2 |
| M10: Form Engine | Data Type Support | 10.2.3 | Answer option management — static lists, admin-editable choices per question | 1 | 1 | 2 |
| M10: Form Engine | Data Type Support | 10.2.4 | Validation engine — per-type rules (min/max, regex, required), custom validators | 1 | 0 | 1 |
| M10: Form Engine | Required/Optional Flags | 10.3.1 | Required flag on question model, enforced in validation pipeline | 1 | 0 | 1 |
| M10: Form Engine | Required/Optional Flags | 10.3.2 | Conditional required — "required if Q_X is answered" | 1 | 0 | 1 |
| M10: Form Engine | Required/Optional Flags | 10.3.3 | Visual indicators (asterisk, inline error) and admin toggle UI | 0 | 2 | 2 |
| M10: Form Engine | Conditional Visibility | 10.4.1 | VisibilityRule model — source question, operator, value, target question(s) | 2 | 0 | 2 |
| M10: Form Engine | Conditional Visibility | 10.4.2 | Rule evaluation engine — server-side validation that conditional questions are gated | 2 | 0 | 2 |
| M10: Form Engine | Conditional Visibility | 10.4.3 | Visual rule builder UI — drag source question, select operator, set value, assign target | 0 | 5 | 5 |
| M10: Form Engine | Conditional Visibility | 10.4.4 | Live preview — show/hide questions in real-time as rules are configured | 0 | 3 | 3 |
| M10: Form Engine | Conditional Visibility | 10.4.5 | Rule conflict detection — warn when rules contradict (circular dependencies) | 2 | 2 | 4 |
| M10: Form Engine | Nested Logic Support | 10.5.1 | AND/OR grouping model — rule groups with logical operators, arbitrary nesting depth | 2 | 0 | 2 |
| M10: Form Engine | Nested Logic Support | 10.5.2 | Nested group evaluation engine — recursive condition resolution | 2 | 0 | 2 |
| M10: Form Engine | Nested Logic Support | 10.5.3 | Nested rule builder UI — add groups within groups, visual indentation, collapse/expand | 0 | 3 | 3 |
| M10: Form Engine | Nested Logic Support | 10.5.4 | Depth limit enforcement and complexity warning | 1 | 1 | 2 |
| M10: Form Engine | External API Dropdowns | 10.6.1 | External API connector model — endpoint URL, auth method, field mapping, cache TTL | 2 | 0 | 2 |
| M10: Form Engine | External API Dropdowns | 10.6.2 | Proxy endpoint for external data — fetch, cache, normalize response | 1 | 0 | 1 |
| M10: Form Engine | External API Dropdowns | 10.6.3 | Admin configuration UI — specify endpoint, map response fields to option label/value | 0 | 2 | 2 |
| M10: Form Engine | External API Dropdowns | 10.6.4 | Dynamic dropdown rendering — lazy-load options from proxy, search/filter | 1 | 1 | 2 |
| M10: Form Engine | Form Versioning | 10.7.1 | FormVersion model — snapshot of form definition on publish, version number, changelog | 2 | 0 | 2 |
| M10: Form Engine | Form Versioning | 10.7.2 | Impact analysis — show how many collected responses reference each version | 1 | 1 | 2 |
| M10: Form Engine | Form Versioning | 10.7.3 | Version history and revert — list versions, diff, restore previous | 1 | 1 | 2 |
| M11: Unified API Gateway | API Design & Versioning | 11.1.1 | RESTful API design — endpoint naming, consistent response envelope, pagination standard | 2 | 0 | 2 |
| M11: Unified API Gateway | API Design & Versioning | 11.1.2 | API versioning strategy (URL path prefix: /api/v1/) with backward compat rules | 1 | 0 | 1 |
| M11: Unified API Gateway | API Design & Versioning | 11.1.3 | Shared serializers for all data domains with consistent field naming | 2 | 0 | 2 |
| M11: Unified API Gateway | API Design & Versioning | 11.1.4 | Error response standardization — error codes, messages, field-level errors | 1 | 0 | 1 |
| M11: Unified API Gateway | Per-Consumer Scoping | 11.2.1 | Consumer model — organization, contact, tier assignment, scope configuration | 2 | 0 | 2 |
| M11: Unified API Gateway | Per-Consumer Scoping | 11.2.2 | Scope resolution middleware — API key → consumer → allowed datasets, countries, actions | 2 | 0 | 2 |
| M11: Unified API Gateway | Per-Consumer Scoping | 11.2.3 | Scope enforcement in querysets — automatic filtering based on resolved scope | 1 | 0 | 1 |
| M11: Unified API Gateway | Rate Limiting | 11.3.1 | Tiered rate limit configuration — limits per tier (free/subscriber/partner) | 1 | 0 | 1 |
| M11: Unified API Gateway | Rate Limiting | 11.3.2 | Django REST throttle classes with Redis-backed counters | 2 | 0 | 2 |
| M11: Unified API Gateway | Rate Limiting | 11.3.3 | Rate limit headers in responses (X-RateLimit-Remaining, X-RateLimit-Reset) | 1 | 0 | 1 |
| M11: Unified API Gateway | Usage Analytics | 11.4.1 | Request logging model — consumer, endpoint, timestamp, response time, status code | 2 | 0 | 2 |
| M11: Unified API Gateway | Usage Analytics | 11.4.2 | Usage aggregation — daily/weekly/monthly totals per consumer, per endpoint | 1 | 0 | 1 |
| M11: Unified API Gateway | Usage Analytics | 11.4.3 | Consumer usage dashboard — charts, top endpoints, quota utilization, time-series | 1 | 3 | 4 |
| M11: Unified API Gateway | Usage Analytics | 11.4.4 | Quota monitoring alerts — trigger notification at 80%/100% usage thresholds | 0 | 1 | 1 |
| M11: Unified API Gateway | API Documentation | 11.5.1 | OpenAPI/Swagger spec auto-generation from Django REST serializers | 1 | 0 | 1 |
| M11: Unified API Gateway | API Documentation | 11.5.2 | Swagger UI hosted at /api/docs/ with authentication support | 1 | 0 | 1 |
| M11: Unified API Gateway | API Documentation | 11.5.3 | Narrative API guide — getting started, authentication, pagination, examples | 1 | 0 | 1 |
| M12: LLM Query Interface | NL Query API | 12.1.1 | Query endpoint — accept text, language parameter; return structured answer + sources | 2 | 0 | 2 |
| M12: LLM Query Interface | NL Query API | 12.1.2 | RAG pipeline — retrieve relevant data chunks, inject context, generate response | 3 | 0 | 3 |
| M12: LLM Query Interface | NL Query API | 12.1.3 | Response formatting — structured JSON + natural language explanation + source citations | 1 | 0 | 1 |
| M12: LLM Query Interface | Restricted DB User | 12.2.1 | Dedicated PostgreSQL role with SELECT-only grants on approved tables | 1 | 0 | 1 |
| M12: LLM Query Interface | Restricted DB User | 12.2.2 | Schema visibility restriction — hide internal tables, audit logs, user data | 1 | 0 | 1 |
| M12: LLM Query Interface | Restricted DB User | 12.2.3 | Query execution sandbox — read-only connection pool with statement timeout | 2 | 0 | 2 |
| M12: LLM Query Interface | Prompt Injection Guards | 12.3.1 | Input sanitization — strip injection patterns, detect adversarial prompts, length limits | 2 | 0 | 2 |
| M12: LLM Query Interface | Prompt Injection Guards | 12.3.2 | Output validation — detect data leakage, PII, off-topic responses before returning | 2 | 0 | 2 |
| M12: LLM Query Interface | Prompt Injection Guards | 12.3.3 | Context window restrictions — limit injected context to approved tables only | 1 | 0 | 1 |
| M12: LLM Query Interface | Topic Boundary | 12.4.1 | Topic classifier — classify incoming query as in-scope / out-of-scope before LLM call | 2 | 0 | 2 |
| M12: LLM Query Interface | Topic Boundary | 12.4.2 | Approved topic registry — admin-configurable list of allowed topics/domains | 1 | 0 | 1 |
| M12: LLM Query Interface | Topic Boundary | 12.4.3 | Out-of-scope response template — polite refusal with redirect to appropriate resource | 1 | 0 | 1 |
| M12: LLM Query Interface | Access Layer Integration | 12.5.1 | Authentication check — validate email/SMS registration or subscription before query | 2 | 0 | 2 |
| M12: LLM Query Interface | Access Layer Integration | 12.5.2 | Tier-based query limits — daily/monthly query caps per user tier | 1 | 0 | 1 |
| M12: LLM Query Interface | Access Layer Integration | 12.5.3 | Query UI widget — input box, response display, source links, limit indicator | 1 | 3 | 4 |
| M12: LLM Query Interface | Response Caching | 12.6.1 | Cache layer — Redis-based, keyed by normalized query + language + data version hash | 1 | 0 | 1 |
| M12: LLM Query Interface | Response Caching | 12.6.2 | Cache invalidation — trigger on data updates (publish events), TTL fallback | 1 | 0 | 1 |
| M12: LLM Query Interface | Response Caching | 12.6.3 | Cache hit/miss monitoring and analytics | 1 | 0 | 1 |
| M13: Monitoring | Prometheus + Grafana | 13.1.1 | Prometheus setup with Docker Compose — Django metrics exporter, service discovery | 1 | 0 | 1 |
| M13: Monitoring | Prometheus + Grafana | 13.1.2 | Grafana provisioning — datasource, default dashboards (system, Django, PG, Celery) | 1 | 0 | 1 |
| M13: Monitoring | Prometheus + Grafana | 13.1.3 | Custom metrics — record counts per module, export volumes, LLM usage, queue depths | 1 | 0 | 1 |
| M13: Monitoring | Alerting Rules | 13.2.1 | Security alerts — 403 spikes, failed login clusters, geo-anomalous access | 1 | 0 | 1 |
| M13: Monitoring | Alerting Rules | 13.2.2 | Application alerts — error rate thresholds, response time p95/p99, Celery queue backlog | 1 | 0 | 1 |
| M13: Monitoring | Alerting Rules | 13.2.3 | Data pipeline alerts — migration failures, export anomalies, LLM API failures | 1 | 0 | 1 |
| M13: Monitoring | Alerting Rules | 13.2.4 | Alert routing — email + notification system integration, escalation rules | 1 | 0 | 1 |
| M13: Monitoring | Log Aggregation | 13.3.1 | Structured logging setup — JSON format, consistent fields (request_id, user_id, module) | 1 | 0 | 1 |
| M13: Monitoring | Log Aggregation | 13.3.2 | Log aggregation stack — Loki or similar with Docker Compose, retention policies | 1 | 0 | 1 |
| M13: Monitoring | Log Aggregation | 13.3.3 | Grafana log dashboard — search, filter, log-to-metric correlation | 1 | 0 | 1 |
| M13: Monitoring | Health Checks & SLA | 13.4.1 | Health check endpoints per service — /health/ with DB, Redis, Celery, storage checks | 1 | 0 | 1 |
| M13: Monitoring | Health Checks & SLA | 13.4.2 | Uptime tracking — synthetic probes, availability calculation | 1 | 0 | 1 |
| M13: Monitoring | Health Checks & SLA | 13.4.3 | SLA dashboard — uptime %, response time trends, incident timeline | 1 | 0 | 1 |
| M14: Security Hardening | CI/CD Security Gates | 14.1.1 | SAST integration — Bandit for Python, ESLint security plugin for Vue.js, fail on critical | 2 | 0 | 2 |
| M14: Security Hardening | CI/CD Security Gates | 14.1.2 | Dependency scanning — pip-audit, npm audit; block merge on known critical CVEs | 1 | 0 | 1 |
| M14: Security Hardening | CI/CD Security Gates | 14.1.3 | Secret scanning — gitleaks in pre-commit hook + CI pipeline | 1 | 0 | 1 |
| M14: Security Hardening | CI/CD Security Gates | 14.1.4 | CI pipeline config — stage ordering, failure gates, bypass rules for false positives | 1 | 0 | 1 |
| M14: Security Hardening | Container Scanning | 14.2.1 | Trivy integration in build pipeline — scan base images + application image | 1 | 0 | 1 |
| M14: Security Hardening | Container Scanning | 14.2.2 | Vulnerability suppression workflow — triage, document accepted risks, re-review cadence | 1 | 0 | 1 |
| M14: Security Hardening | Container Scanning | 14.2.3 | Base image policy — approved base images list, automated rebuild on upstream updates | 1 | 0 | 1 |
| M14: Security Hardening | DAST | 14.3.1 | OWASP ZAP setup against staging environment — automated scan on deploy | 1 | 0 | 1 |
| M14: Security Hardening | DAST | 14.3.2 | ZAP scan profile tuning — auth handling, crawl scope, false positive suppression | 1 | 0 | 1 |
| M14: Security Hardening | DAST | 14.3.3 | Advisory finding triage process — severity classification, sprint assignment | 1 | 0 | 1 |
| M14: Security Hardening | Encryption Setup | 14.4.1 | TLS 1.2+ enforcement — reverse proxy config, HSTS headers, certificate management | 1 | 0 | 1 |
| M14: Security Hardening | Encryption Setup | 14.4.2 | Database encryption at rest — pgcrypto for sensitive fields (API keys, PII) | 1 | 0 | 1 |
| M14: Security Hardening | Encryption Setup | 14.4.3 | Secrets management — environment-based injection, no secrets in code or config files | 1 | 0 | 1 |
| M14: Security Hardening | Encryption Setup | 14.4.4 | Backup encryption — AES-256 encrypted database backups | 1 | 0 | 1 |
| M14: Security Hardening | Incident Response | 14.5.1 | Runbooks — compromised API key, data leak, unauthorized access, DDoS response | 1 | 0 | 1 |
| M14: Security Hardening | Incident Response | 14.5.2 | Incident severity classification and escalation matrix | 1 | 0 | 1 |
| M14: Security Hardening | Backup & Restore | 14.6.1 | Automated backup script — scheduled pg_dump, encrypted, offsite upload | 1 | 0 | 1 |
| M14: Security Hardening | Backup & Restore | 14.6.2 | Restore drill — documented procedure, RTO/RPO validation test | 1 | 0 | 1 |
| M15: Documentation | Architecture Docs | 15.1.1 | System architecture diagrams — component, deployment, data flow diagrams | 2 | 0 | 2 |
| M15: Documentation | Architecture Docs | 15.1.2 | ADR (Architecture Decision Records) — consolidate all decisions made during project | 1 | 0 | 1 |
| M15: Documentation | Architecture Docs | 15.1.3 | Integration point documentation — external APIs, LLM provider, email service, OCR | 1 | 0 | 1 |
| M15: Documentation | API Documentation | 15.2.1 | Auto-generated OpenAPI spec — ensure all endpoints documented with examples | 1 | 0 | 1 |
| M15: Documentation | API Documentation | 15.2.2 | Consumer onboarding guide — authentication, rate limits, pagination, code samples | 1 | 0 | 1 |
| M15: Documentation | API Documentation | 15.2.3 | Data dictionary — field definitions, types, enums, valid ranges for all API resources | 1 | 0 | 1 |
| M15: Documentation | Operational Runbooks | 15.3.1 | Deployment procedure — step-by-step for staging and production | 1 | 0 | 1 |
| M15: Documentation | Operational Runbooks | 15.3.2 | Rollback procedure — DB rollback, application rollback, partial rollback | 1 | 0 | 1 |
| M15: Documentation | Operational Runbooks | 15.3.3 | Scaling and maintenance guides — add capacity, rotate credentials, update dependencies | 1 | 0 | 1 |
| M15: Documentation | Admin User Guides | 15.4.1 | Admin panel walkthrough — screenshots, feature-by-feature guide | 1 | 1 | 2 |
| M15: Documentation | Admin User Guides | 15.4.2 | Form engine admin guide — creating surveys, configuring rules, versioning | 1 | 1 | 2 |
| M15: Documentation | Admin User Guides | 15.4.3 | Export configuration guide — setting up tiers, API keys, watermarking | 0 | 1 | 1 |
| **TOTALS** | | | | **406** | **177** | **583** |
| **QA (25% of Dev)** | | | | | | **146** |
| **GRAND TOTAL** | | | | | | **729** |
