## M1: COBRA Core Platform

### Authentication [All Users]

**1. Login Page**

- Email + password form
- "Forgot password?" link
- Error states (invalid credentials, locked account)
- Redirect to CBA Document List on success

**2. Forgot Password Page**

- Email input
- Success state ("check your email") — same message regardless of whether email exists

**3. Reset Password Page**

- Token validation on load
- New password + confirmation form
- Expired/invalid token state
- Success → redirect to login

**4. First Login — Change Password**

- Forced password change on first login (temp password set by admin)
- New password + confirmation form
- Password strength indicator + policy hints

---

### App Shell [All Authenticated Users]

**5. Global Layout Shell**

- Sidebar navigation — collapsible, grouped by module (context-sensitive by role)
- Header bar — logo, country context switcher (dropdown, persisted), locale selector (language dropdown), notification bell (unread badge), user avatar + menu (profile, logout)
- Breadcrumb bar — hierarchical navigation (e.g. Root > Countries > Sierra Leone > [CBA Title])
- Permission-aware rendering — hide/disable menu items, buttons, routes based on role

**6. Notification Center**

- Bell icon dropdown panel — list of recent notifications, unread highlighting
- Mark as read / mark all as read
- Click-through to source (e.g. review request → review screen)
- Full notifications page (paginated, filterable by type)

**7. Notification Preferences**

- Per-event-type toggles: email on/off, in-app on/off
- Event types: review requests, approvals, rejections, export completions, system alerts

---

### User & Role Administration [Admin]

**8. User List**

- Table: name, email, roles, assigned countries, status (active/deactivated), last login
- Sort, filter, search
- Bulk actions (activate, deactivate)
- Create user button

**9. User Create / Edit**

- Form: name, email, temporary password (on create), role assignment (multi-select), country assignment (multi-select)
- Deactivate toggle (not delete)
- View assigned roles and countries at a glance

**10. Role Management — Permission Matrix**

- Grid view: rows = roles, columns = modules × actions (view, create, edit, delete, publish, export)
- Toggle checkboxes per cell
- Bulk select (all actions for a module, all modules for an action)
- Clone role, archive role
- 6 default templates pre-seeded (Admin, Data Manager, Annotator, Reviewer, API Consumer, Read-Only Viewer)

**11. User → Role Assignment**

- Select user → assign/revoke roles
- Bulk assignment (select multiple users → assign role)

**12. Country Assignment to Users**

- Multi-select country picker per user
- Bulk assign (select user group → assign countries)

---

### Country Management [Admin, Data Manager]

**13. Country List**

- Table: country ID/slug, country name (linked), owner, created, modified, state
- Sort by modified date
- Search / filter
- Add country button
- Row-level actions (edit, delete)

**14. Country Detail — Contents Tab**

- Breadcrumb: Root > Countries > [Country Name]
- Tabs: Contents | Edit | Coverage
- List of CBAs within this country — table: ID/slug, title (linked), owner, created, modified, state
- "+ New CountryProfile" button
- Add CBA / Paste / Clear paste buffer actions
- Row-level actions per CBA (delete, edit, cut, copy)

**15. Country Detail — Edit Tab**

- Country metadata form:
  - Country Numeric Code (ISO 3166, required)
  - Administrative division ID (for autonomous regions like Zanzibar)
  - CBA Browser Title Template (placeholder tokens: {title}, {country}, {sector})
  - CBA Meta Description Template (placeholder tokens)
  - Field-level help text/instructions
- Save / Cancel buttons

**16. Country Detail — Coverage Tab**

- Coverage data view for this country (coverage statistics, data completeness)

---

### Image / Asset Management [Admin]

**17. Image Library**

- Grid or list of uploaded images/assets
- Upload new image
- Delete / replace
- Image metadata (filename, dimensions, upload date)
- Used-by reference (which records reference this image)

---

### System Administration [Admin]

**18. System Settings**

- Site configuration (site name, default language, timezone)
- Feature toggles (enable/disable modules)
- Maintenance mode toggle
- Email settings (SMTP config, sender address)

**19. Audit Log Viewer**

- Filterable table: user, action type, resource type, module, date range, IP address
- Paginated
- Detail view per log entry (full payload diff)
- CSV export for compliance

---

## M2: Labour Law Database [Data Manager, Annotator, Reviewer]

**20. Labour Law Record List**

- Table: country, category (min wages/working hours/leave/etc.), status (Draft/Under Review/Published), last modified, author
- Filters: country dropdown, category, status, date range
- Search bar (full-text)
- Sort by: relevance, date, country
- Bulk operations: bulk publish, bulk assign reviewer (scoped by country)

**21. Labour Law Data Entry Form**

- Dynamic form renderer — fields change based on selected country configuration
- Field types: text, number, date, dropdown, free text
- Temporal validity fields: effective_from, effective_to, legislative_reference, gazette_url
- Client + server-side validation, required field indicators (asterisk)
- Draft auto-save (periodic + explicit save button)
- Field-level tooltips / inline help (admin-configured guidance text)
- Country context switching — changing country reloads field config and existing records

**22. Labour Law Version History**

- Table: version number, date, author, action summary
- Side-by-side diff view — highlight field differences between two selected versions
- Rollback to version — confirmation dialog, creates new version on rollback

**23. Labour Law Publishing Workflow**

- Status badge (Draft / Under Review / Published) — color-coded
- Transition action buttons (context-sensitive: Submit for Review, Approve, Reject, Unpublish)
- Comment field on transitions
- Publishing history log — all state changes with timestamp, actor, comment
- Notification trigger on transition (email + in-app)

**24. Labour Law Search Results**

- Search bar with type-ahead
- Filter panel: country, category, date range, status
- Results list with keyword highlighting
- Pagination
- Sort options: relevance, date, country

---

## M3: International Law Database [Data Manager, Annotator, Reviewer]

**25. International Law Record List**

- Same pattern as Labour Law list
- Convention/treaty-specific columns

**26. International Law Data Entry Form**

- Adapted from Labour Law form with international law field configuration
- Convention selector — searchable dropdown of ILO conventions / treaties

**27. Cross-Country Ratification View**

- Matrix: countries (rows) × conventions (columns)
- Ratification status per cell (ratified, signed, not ratified) with dates
- Filter by convention, region, status

---

## M4: CBA Processing Engine [Data Manager, Annotator, Reviewer]

**28. CBA Document List** _(Landing page after login)_

- Table: CBA title, country, parties, industry, upload date, status (Uploaded / Converting / Ready for Review / Approved), assignee
- Filters: country, status, industry, date range
- Search
- Bulk assignment

**29. CBA Document Upload**

- Drag-and-drop upload zone (PDF)
- Upload progress indicator
- File list (for multi-file upload)
- Metadata form on upload: country, expected language, industry, parties (if known)
- Validation errors with retry option
- File type + size limit enforcement

**30. CBA — Contents Tab (Read-Only Document View)**

- Full CBA document rendered as HTML — read-only, no editing
- Table of contents sidebar / section jump links (generated from headings)
- Breadcrumb: Root > Countries > [Country] > [CBA Title]
- Tab bar: **Contents** | Edit | Annotate

**31. CBA — Edit Tab (Metadata Entry)**

- Tab bar: Contents | **Edit** | Annotate
- Form pre-filled from AI extraction (editable)
- Fields: parties (employer side, union side), effective dates (start/end), coverage scope, industry code (ISIC — searchable dropdown), country, region, legal status
- Date pickers, searchable dropdowns for industry/country
- Validation rules (date logic, mandatory fields per status)
- Save / submit for review

**32. CBA Document Review — Side-by-Side (HITL)**

- Left pane: Original document viewer (PDF render)
- Right pane: AI-converted structured HTML
- Inline HTML editor (rich text editing of converted output)
- Section-level accept/reject controls
- Approve / Reject / Request re-conversion buttons
- Comment field on decision
- Document conversion status indicator
- Navigation: next/previous document in queue

---

## M5: AI Annotation Pipeline

### Annotation Interface [Annotator]

**33. CBA — Annotate Tab (Split-Pane Annotation Screen)**

**Left Pane — Document Viewer:**

- Full CBA document text rendered as HTML
- Text selection / highlighting — user selects (highlights) text passages relevant to annotation questions
- Color-coded highlights:
  - Yellow: text already linked to a completed annotation
  - Green: text currently being selected
  - Red/orange: flagged or conflicting annotation
- Selected text becomes a "source snippet" linked to the active question on the right
- Scroll sync option with right pane
- **Auto-scroll + flash on locate** — when annotator clicks the search/locate icon (🔍) next to a question on the right, the document scrolls to and briefly flashes/highlights the text passage previously linked to that question

**Right Pane — Annotation Form:**

- Tab bar: Contents | Edit | **Annotate**
- **Category tab bar** — horizontal scrollable tabs:
  - General CBA data, Job Titles, Training, Social Security & Pensions, Employment Contracts, Sickness & Disability, Health & Medical Assistance, Work/Family Balance Arrangements, Gender Equality Issues, Working hours, Wages, Workers' Representation & Conflicts, New Technologies & Green Clauses, Coverage
- Active category highlighted (teal/accent color)
- **Questions rendered dynamically per category** — driven by form engine (Module 10)

**Question types observed:**

- Yes/No toggle buttons
- Searchable dropdown (single-select)
- Searchable dropdown (multi-select) — selected items as removable chips above dropdown, search box within dropdown list
- Date picker (calendar widget)
- Number input
- Free text input
- Codebook version selector (number input with hint text like "Please select 6")

**Per-question interaction elements:**

- **Required field indicator**: Red asterisk (★) on mandatory questions
- **Instruction / help text**: Below question label (e.g. "You can select multiple values", "Please be as accurate as possible", "Google the name of the company...")
- **AI suggestion icon** (🌐 globe): Shown next to questions where AI has pre-filled a suggested answer — human reviews and confirms/overrides
- **Search/locate icon** (🔍): Scrolls left pane to linked text passage + flashes highlight to draw attention
- **Add annotation icon** (➕ red plus): For adding additional annotation entries to a question
- **Source text snippet pills**: After selecting text + answering, the selected text appears as a colored pill/chip near the answer — with × to remove. Multiple snippets linkable per answer
- **Conditional questions**: Follow-up questions appear/hide dynamically based on previous answers (e.g. "Are you able to specify the above industry in more detail?" → Yes/No → sub-industry dropdown appears)

**Key validation behavior:**

- "Please select a text for this clause first" — popup/toast when trying to answer a question that requires linked text without first selecting a passage

---

### Review Queue [Reviewer]

**34. Annotation Review Queue**

- Table: CBA title, country, language, annotation date, annotator, status (Pending Review / Reviewed / Rejected)
- Sort by: date, country, language
- Filter by: status, annotator, country
- Batch operations: bulk assign to reviewer

**35. Field-Level Annotation Review**

- Per-field view: annotator's answer, linked source text snippet(s), AI suggestion (if any)
- Accept / Reject / Edit per field
- Inline edit for corrections
- Comment per field
- Navigate between fields; clicking a field scrolls + highlights the linked passage in document view

---

## M6: Pensions Database [Data Manager, Annotator, Reviewer]

**36. Pensions Record List**

- Table: country, pension scheme, status, last modified
- Filters: country, scheme type, status
- Search

**37. Pensions Data Entry (Survey-Based)**

- Form rendered by Dynamic Survey Engine (Module 10)
- Country context selection → filters schemes by country
- Regional pension scheme variations (sub-national support)
- Response submission pipeline

**38. Pensions Publishing Workflow**

- Same pattern as Labour Law (Draft → Review → Published)
- Role-gated transitions
- Mandatory field checks before submission

---

## M7: Data Migration & Schema Unification [Admin, Data Manager]

**39. Migration Validation Dashboard**

- Per-domain progress bars (Labour Law, CBA, Int'l Law, Pensions, Excel files)
- Row count reconciliation: source vs. target per table
- Data quality charts (completeness, consistency scores)
- Error summary with drill-down to individual failed records
- Exception/quarantine queue — records failing validation, with edit + retry

**40. Migration Sign-Off**

- Per-domain sign-off checklist
- Data manager approval per domain
- Audit trail of sign-offs

---

## M8: Export & Data Distribution [Admin, Data Manager]

**41. Export Profile Configuration**

- Create/edit export tiers (free, subscriber, partner)
- Field inclusion/exclusion per tier (checkbox list per data domain)
- Aggregation rule setup per tier (free tier gets averages only, paid gets raw)
- Output format selection (CSV, JSON, XLSX)
- Preview sample output

**42. Bulk Export Approval Queue**

- Pending exports list: requester, data scope, row count, timestamp
- Review export parameters + preview sample data
- Approve / Reject with comment
- Post-approval: download link with expiry

**43. API Key Management**

- Table: consumer name, key (masked), tier, scoped datasets, scoped countries, status (active/revoked), usage stats
- Create key — shown once on creation
- Rotate key, Revoke key (instant)
- Rate limit status and configuration per key
- Filter by consumer/tier

**44. Export History / Download Center**

- List of past exports: date, tier, format, row count, status, download link (if not expired)
- Async export job status (queued → processing → ready → expired)

---

## M9: Translation & Multilingual Support [Admin, Data Manager, Translator]

### Vocabulary / Translation Management [Admin, Data Manager]

**45. Vocabulary List**

- Table: vocabulary ID/slug, title (linked), owner, created, modified, state
- Row-level actions (delete, edit, cut, copy)
- Add new vocabulary
- Deprecated vocabulary indicators (e.g. "DO NOT USE. WILL BE GONE SOON")
- Search / filter

**46. Vocabulary Detail — Edit Tab**

- Vocabulary metadata form: Name (required), Short description (meta), Keywords
- Save / Cancel

**47. Vocabulary — CSV Editor Tab**

- Inline editable grid/table:
  - Columns: id, value (fallback), then one column per language (EN, NL, FR, PT, SW, ES, BA, EL, DE, etc.)
  - Rows: vocabulary terms with per-language translations
  - All cells directly editable
- Help text / instructions banner explaining:
  - id and value are required, id must be unique
  - "value" column is the fallback when no translation exists
  - FILTER column usage for locale-specific visibility
- Save button (top and bottom of grid)
- Paste / Clear paste buffer actions

**48. Vocabulary — Upload CSV Tab**

- CSV file upload with drag-and-drop or file picker
- **Replace-all warning**: Clear destructive action warning that upload will replace ALL existing vocabulary entries
- Preview of incoming data before confirmation
- Upload + confirm flow

### Translation Content Management [Admin, Data Manager, Translator]

**49. Translation Coverage Dashboard**

- Matrix: records (rows) × languages (columns)
- Completion percentage per cell — color-coded (complete/partial/missing)
- Filter by module (Labour Law, CBA, etc.), country, language

**50. Side-by-Side Translation Editor**

- Left: original language content (field-by-field)
- Right: target language translation (editable fields)
- Translation status per field (translated / needs review / missing)
- Save + submit for review

**51. Translator Assignment & Workload**

- Assign languages to translator users
- Workload view: items per translator, pending/complete counts
- Translation task queue: prioritized list of pending items per translator

**52. Translation Review & Publish**

- Reviewer approval screen before translated content goes live
- Accept / Reject per field or per record

---

## M10: Dynamic Survey / Form Engine [Admin]

_Replaces the legacy Ace Editor XML/HTML template system entirely. No raw code editing — all form definition is visual._

**53. Template List** _(replaces Root > Templates)_

- Table: template name (linked), domain type (LabourLaw, CBA, CountryProfile), version, question count, status (draft/published), owner, created, modified
- Create new template, clone existing
- Row-level actions

**54. Question List Management**

- Table view of all questions in a form — inline editing, status toggle (active/archived)
- Drag-and-drop reordering (section-level and question-level)
- Archive / restore questions (soft delete with impact warning: "X responses reference this question")
- Section grouping headers

**55. Add / Edit Question Modal**

- Question label (multi-language)
- Question type selector (text, number, date, boolean, dropdown, multi-select, radio, checkbox, free text)
- Help text / instruction text
- Required flag toggle, "conditionally required" option
- Validation rules: min/max, regex, custom validators
- Answer options management (for dropdowns/multi-select): static list editor, option reordering
- External API dropdown config: endpoint URL, auth method, field mapping (label/value), cache TTL
- Vocabulary binding — link a dropdown to an existing vocabulary (from M9)
- Preview of the question as it would render

**56. Visual Conditional Visibility Rule Builder**

- Source question selector
- Operator picker (equals, not equals, contains, greater than, etc.)
- Value input
- Target question(s) to show/hide
- AND/OR grouping — nested groups with visual indentation, collapse/expand
- Rule conflict detection with warning (circular dependency detection)
- Live preview — questions show/hide in real-time as rules are configured
- Depth limit enforcement with complexity warning

**57. Form Versioning**

- Version history list: version number, publish date, changelog
- Diff view between versions (added/removed/changed questions)
- Impact analysis: how many responses reference each version
- Revert to previous version

**58. Form Live Preview**

- Full rendering of current form definition as end-user would see it
- Test conditional logic by filling dummy answers
- Responsive preview (desktop/mobile)

---

## M11: Unified API Gateway [Admin]

**59. Consumer Usage Dashboard**

- Per-consumer charts: requests over time, top endpoints, response time
- Quota utilization (% of rate limit used)
- Time-series views (daily/weekly/monthly)
- Quota monitoring alerts configuration (80%/100% thresholds)

**60. API Documentation Portal (Scalar)**

- Auto-generated from FastAPI OpenAPI spec
- Interactive try-it-out with API key authentication
- Narrative getting-started guide, code samples

---

## M12: LLM Query Interface [Public / Subscriber]

**61. LLM Query Widget (embeddable on public website)**

- Text input box for natural language questions
- Language selector
- Response display: natural language answer + source citations + data tables
- Usage limit indicator (remaining queries for current tier)
- Authentication check (email/SMS registration or subscription validation)
- Polite refusal message for out-of-scope queries

### LLM Admin [Admin]

**62. Topic Boundary Configuration**

- Approved topic registry: add/remove/edit allowed topics/domains
- Out-of-scope response template editor

---

## M13: Monitoring & Observability [Admin only]

**63. Grafana Dashboards** _(external tool, pre-configured)_

- System metrics (CPU, memory, disk, network)
- FastAPI request metrics (latency, error rate, throughput)
- PostgreSQL metrics (connections, query performance)
- Celery queue depth and task metrics
- Custom metrics: record counts per module, export volumes, LLM API usage
- Alert rules: 403 spikes, failed login clusters, error rate thresholds, queue backlogs

_No custom in-app dashboard — Grafana is the dashboard._

---

## Cross-Cutting UX Notes for Designer

1. **Hierarchical content navigation**: Existing system uses Root → category (Templates/Vocabularies/Countries) → items → detail. Breadcrumbs throughout.
2. **Consistent tab pattern**: Most entities use Contents | Edit | [Domain-specific tab]. Tabs change per entity type.
3. **Three-tab CBA view**: Contents | Edit | Annotate — three distinct modes for the same CBA record.
4. **Text↔Answer linking is the core annotation interaction**: Highlight-then-annotate is the fundamental pattern.
5. **Search/locate icon per question**: Clicking scrolls the document to and flashes the linked passage — bidirectional navigation.
6. **Multi-snippet answers**: A single question can accumulate multiple text selections from different parts of the document.
7. **Color-coded highlights**: Communicate annotation state at a glance (yellow = done, green = current, red = flagged).
8. **AI as assistant, not authority**: AI suggestions are visual indicators (globe icon), always requiring human confirmation — no auto-acceptance.
9. **Codebook versioning per CBA**: Tracks which coding standard was applied.
10. **Instruction richness**: Each question can carry detailed guidance text shown inline.
11. **Vocabulary ↔ Form engine binding**: Dropdowns in annotation/survey forms can be backed by vocabularies from M9.
12. **Destructive action warnings**: CSV vocabulary upload warns that it replaces all — apply this pattern to any replace-all operations.
13. **Row-level actions**: Existing system shows inline action icons per row (delete, edit, cut, copy) — preserve quick-access pattern.
14. **FastAPI + Scalar**: Backend is FastAPI, API docs use Scalar.
