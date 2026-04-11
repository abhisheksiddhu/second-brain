# Security & Data Governance — COBRA 2.0

---

## Version 1 — Technical Team

### Security Architecture & Controls — COBRA 2.0

This document details the security posture for COBRA 2.0 at the implementation level. It covers threat modeling methodology, network security, access control enforcement, data governance controls, and security validation gates across the delivery lifecycle.

---

### 1. Threat Modeling — STRIDE Framework

We apply **STRIDE** at two defined points in the delivery lifecycle:

| Phase                    | When                                    | Objective                                                                                                               |
| ------------------------ | --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| **Discovery & Design**   | Before architecture sign-off (Week 1–2) | Identify threats per component _before_ code is written. Output: threat register + mitigations mapped to backlog items. |
| **UAT / Pre-Production** | Before go-live                          | Re-evaluate against the running system. Validate that mitigations are implemented. Identify residual risks.             |

**STRIDE applied to COBRA 2.0 components:**

| Threat Category                | Target Components                                 | Example Threat                                                  | Mitigation                                                                                                                    |
| ------------------------------ | ------------------------------------------------- | --------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **S — Spoofing**               | Django auth, API keys, admin panel                | Attacker impersonates a valid API consumer or admin user        | MFA on admin accounts; API keys scoped per consumer with HMAC signing; session tokens with short TTL and rotation             |
| **T — Tampering**              | Postgres records, audit logs, exported files      | Attacker or insider modifies wage data or deletes audit entries | Append-only audit log table (no UPDATE/DELETE grants); DB triggers on critical tables; checksums on exported files            |
| **R — Repudiation**            | Data mutations, export events, approval workflows | User denies they approved a data export                         | Immutable audit log capturing user ID, timestamp, IP, action, and payload hash; separate log store from operational DB        |
| **I — Information Disclosure** | API responses, DB queries, Elasticsearch indices  | Over-fetching via API returns fields the consumer shouldn't see | Field-level serialization scoped per API key; Elasticsearch index-level security; no raw query exposure                       |
| **D — Denial of Service**      | API gateway, Airflow DAGs, ingestion endpoints    | Bulk API calls overwhelm the system or trigger runaway DAGs     | Per-consumer rate limiting at reverse proxy; Airflow concurrency limits; request size caps                                    |
| **E — Elevation of Privilege** | Django admin, RBAC, DB roles                      | Annotator escalates to Admin via permission manipulation        | Permission groups enforced server-side only (never trust frontend); DB roles with least-privilege; no shared service accounts |

The threat register is a living document — reviewed at sprint boundaries and updated when new modules are introduced.

---

### 2. Network Security & DB Isolation

The database is **never directly accessible** from the internet or from any component other than the application layer.

```
┌──────────────────────────────────────────────────────────┐
│                    Public Internet                        │
└──────────────────┬───────────────────────────────────────┘
                   │ HTTPS (443)
          ┌────────▼────────┐
          │  Reverse Proxy   │  ← WAF rules, rate limiting,
          │  (Nginx/Traefik) │    TLS termination, IP allowlist
          └────────┬────────┘
                   │ Internal network only
       ┌───────────┼───────────────┐
       │           │               │
┌──────▼──┐  ┌────▼─────┐  ┌──────▼──────┐
│ Django   │  │ React    │  │ Airflow     │
│ API      │  │ (static) │  │ Workers     │
└──────┬───┘  └──────────┘  └──────┬──────┘
       │ TCP 5432 (private net)    │
       │  ┌────────────────────┐   │
       └──► PostgreSQL         ◄───┘
          │ (firewall-gated)   │
          │ Public IP, but     │
          │ accepts only from  │
          │ app CIDR / pod IPs │
          └────────────────────┘
```

**Enforcement details:**

| Control                       | Implementation                                                                                                                                       |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **DB network binding**        | PostgreSQL has a public IP but firewall rules restrict all inbound connections. Only whitelisted application IPs are allowed.                         |
| **Firewall / Security group** | Ingress to port 5432 allowed **only** from application pod CIDR range or specific service IPs. All other sources denied.                             |
| **K8s NetworkPolicy**         | Kubernetes NetworkPolicy restricts DB pod ingress to labeled app pods only. No other namespace or pod can reach the DB.                              |
| **No direct DB access**       | Direct SSH to DB server disabled. DB administration only via a bastion host with MFA and full audit logging.                                         |
| **Elasticsearch isolation**   | Same pattern — ES cluster on private subnet, accessible only from Django API pods and Airflow workers. No public endpoint.                           |
| **Airflow metadata DB**       | Separate Postgres instance, same network isolation. Airflow webserver has read-only access to metadata; DAG execution uses a scoped service account. |

---

### 3. Authentication & Authorization

**Authentication stack:**

| Layer                                  | Mechanism                                                                                                                                                                       |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Admin users (WageIndicator staff)**  | Django session-based auth with MFA. Cookies marked HTTP-only, Secure, SameSite. Session TTL: 30 min idle, 8 hr absolute. CSRF protection enforced.                              |
| **API consumers (external partners)**  | API key authentication. Keys are hashed (SHA-256) in DB — plaintext never stored. Each key is scoped to: allowed datasets, allowed countries, allowed actions, rate limit tier. |
| **Service-to-service (Airflow ↔ API)** | Internal short-lived JWT tokens (5 min TTL), asymmetrically signed (RS256). Issued from a shared secrets store, validated by Django middleware.                                 |

**Authorization model:**

- **Role-based (RBAC):** Defined permission groups — Admin, Data Manager, Annotator, Reviewer, API Consumer, Read-Only Viewer. Each role has an explicit whitelist of allowed actions. No implicit access.
- **Module-scoped:** Permissions are scoped per module (CBA, Labour Law, Living Wage, etc.). Access to one module does not grant access to another.
- **Country-scoped:** Data queries are filtered by the user's assigned countries at the query layer. A regional partner cannot access or export data outside their geography.
- **Action-level granularity:** `view`, `edit`, `approve`, `export`, and `delete` are separate permissions. An annotator can edit but not approve. A viewer can see but not export.
- **Object-level (where needed):** For sensitive records such as specific CBA ownership, permissions can be assigned at the individual record level.
- **Server-side enforcement only:** Frontend hides UI elements for UX convenience, but the backend is the sole enforcement boundary. Every request is validated regardless of how it arrives.
- **DB-level mirroring:** The application DB user has only `SELECT`, `INSERT`, `UPDATE` on operational tables. `DELETE` is restricted to an admin migration role. Audit tables have **no** `UPDATE` or `DELETE` grants for any application role.

---

### 4. Data-at-Rest & In-Transit Encryption

| Layer                     | Encryption             | Detail                                                                                                                                                                              |
| ------------------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **In transit (external)** | TLS 1.3               | Terminated at the reverse proxy. Strong cipher suites only.                                                                                                                         |
| **In transit (internal)** | mTLS                   | Pod-to-pod encrypted via service mesh (Linkerd or equivalent) or K8s-native TLS.                                                                                                    |
| **Postgres at rest**      | AES-256 full-disk      | Provider-level block storage encryption. Column-level encryption via `pgcrypto` available for specific sensitive fields.                                                            |
| **Backups**               | Encrypted before write | DB dumps encrypted with GPG or provider-managed encryption. Backup keys rotated quarterly.                                                                                          |
| **Elasticsearch**         | Encrypted indices      | Node-level encryption at rest. TLS for inter-node communication.                                                                                                                    |
| **Secrets**               | Vault-managed          | DB passwords, API signing keys, LLM tokens stored in HashiCorp Vault or K8s Secrets with encrypted etcd. Rotated on schedule. Never in source code, env files, or container images. |

---

### 5. CI/CD Security Gates

Every deployment passes through:

| Gate                                | Stage                | Blocks Deploy?                                    |
| ----------------------------------- | -------------------- | ------------------------------------------------- |
| **SAST** (Static analysis)          | PR / merge request   | Yes — critical/high findings block merge          |
| **Dependency scanning**             | PR / merge request   | Yes — known CVEs in dependencies block merge      |
| **Container image scan**            | Build pipeline       | Yes — critical vulns block image push             |
| **Secret detection**                | Pre-commit hook + CI | Yes — hardcoded secrets block commit              |
| **DAST** (Dynamic scan)             | Staging deploy       | Advisory — findings triaged within sprint         |
| **STRIDE review**                   | UAT milestone        | Yes — unmitigated high-risk threats block go-live |

---

### 6. Audit Logging Design

**Every data mutation, access event, and administrative action is captured.**

```
FastAPI App  ────►  Audit Log Table  ────►  Log Archival
(middleware)       (append-only)           (encrypted object storage)
```

**What gets logged per event:**

| Field                  | Description                                                          |
| ---------------------- | -------------------------------------------------------------------- |
| Event ID (UUID)        | Unique identifier                                                    |
| Timestamp (UTC)        | When it happened                                                     |
| User / API key hash    | Who did it                                                           |
| Action type            | `CREATE`, `UPDATE`, `DELETE`, `EXPORT`, `LOGIN`, `PERMISSION_CHANGE` |
| Module                 | `cba`, `labour_law`, `living_wage`, etc.                             |
| Resource type & ID     | Which table and which record                                         |
| Payload hash (SHA-256) | Hash of the data at time of action — enables tamper detection        |
| Source IP & User Agent | Where and how the request originated                                 |
| Country scope          | Countries affected by this action                                    |

**Integrity guarantees:**

- Application DB user has `INSERT` only on the audit table. No `UPDATE`, no `DELETE`.
- Archived to encrypted object storage (MinIO or equivalent) after 90 days. Archives are checksum-verified.
- Monitoring alert triggers if audit log volume drops unexpectedly — indicates possible bypass.

---

### 7. Export & Data Distribution Controls

| Control                     | Where Enforced                             | How                                                                                                                                                            |
| --------------------------- | ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Field filtering**         | API serialization layer                    | Each API key maps to a data tier config that defines which fields are included/excluded per model. Applied dynamically at serialization.                       |
| **Aggregation enforcement** | Query layer                                | Free-tier consumers receive pre-aggregated results (country-level averages). Raw records are never returned for restricted tiers.                              |
| **Rate limiting**           | Reverse proxy + application throttle layer | Per-consumer rate limits at both the proxy (outer defense) and application layer (inner enforcement).                                                          |
| **Bulk export approval**    | Application workflow (maker-checker)       | Exports exceeding a configurable row threshold require a second user's approval before the system generates the file.                                          |
| **Watermarking**            | Export pipeline                            | Exported files include metadata (export ID, consumer ID, timestamp). Row ordering is subtly permuted per consumer as a statistical watermark for leak tracing. |
| **Key revocation**          | API key management                         | WageIndicator can revoke any API key instantly. Revocation is checked on every request (DB lookup, not cache) — takes effect within one request cycle.         |

---

### 8. Incident Response Posture

| Aspect                | Approach                                                                                                                                                                                     |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Detection**         | Prometheus alerting rules for: spike in 403s, unusual export volumes, login failures exceeding threshold, access from unexpected geolocations.                                               |
| **Response playbook** | Documented runbooks for: compromised API key (revoke + audit trail review), suspected data leak (trace via watermark + audit log), unauthorized access attempt (block IP + forensic review). |
| **Recovery**          | Encrypted backups tested quarterly with restore drills. RTO/RPO targets defined per data tier during discovery.                                                                              |

---

---

## Version 2 — Business Team

### Security & Data Governance — COBRA 2.0

WageIndicator's question has three parts: **Is the system secure?** **Can we control who sees what?** **Can we control what data goes out, to whom, and how much?** The answer to all three is yes — by design, not as an afterthought.

---

#### System Security

| Concern                  | How It's Addressed                                                                                                                                    |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Data stays in Europe** | Single-region EU deployment on European provider (OVHcloud). No US vendors involved. No data leaves EU jurisdiction.              |
| **Encrypted everywhere** | All data encrypted in transit (TLS) and at rest (AES-256). Backups encrypted. Secrets stored in a vault — never in code.                              |
| **Audited by design**    | Every action — data edits, exports, permission changes, logins — is logged with who, what, when, and from where. Logs are immutable and tamper-proof. |
| **Tested before launch** | Formal threat modeling during design phase. Security scans run automatically on every code change. Dynamic security testing before go-live.           |

---

#### Access Control — Who Gets What

WageIndicator retains full control over permissions:

| Capability                  | What It Means                                                                                                                                                    |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Role-based access**       | Each user gets a defined role (Admin, Data Manager, Annotator, Reviewer, API Consumer, Viewer). Roles have explicit permissions — no one gets access by default. |
| **Module-level boundaries** | Access to CBA data doesn't mean access to Labour Law data. Each dataset is independently controlled.                                                             |
| **Country-level scoping**   | A regional partner can be restricted to only their countries. They cannot see or query data outside their assigned geography.                                    |
| **Action-level control**    | View, edit, approve, and export are separate permissions. An annotator can edit but not export. A viewer can see but not change.                                 |
| **Partner API access**      | External consumers receive API keys scoped to specific datasets, countries, and usage limits. WageIndicator issues, scopes, and revokes these keys at will.      |

---

#### Data Distribution — What Goes Out, To Whom, How Much

| Mechanism               | What It Means                                                                                                                                                     |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Tiered data access**  | WageIndicator defines tiers: e.g., public tier gets country-level summaries; premium partners get city-level detail. The platform enforces the tier per consumer. |
| **Field-level control** | Specific data fields can be shown or hidden per partner. A government client might see full detail; a commercial consumer sees only aggregates.                   |
| **Usage quotas**        | Each external consumer has defined rate limits and monthly quotas. Prevents bulk extraction or over-use.                                                          |
| **Export approvals**    | For large data exports, a second person must approve before the system generates the file. No single user can extract data unilaterally.                          |
| **Traceability**        | Every export is tagged. If data surfaces where it shouldn't, WageIndicator can trace it back to the exact consumer and export event.                              |

---

#### How WageIndicator Stays in Control

| Feature                      | What It Provides                                                                                                                   |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **Admin dashboard**          | Real-time view of active users, recent access, export activity, and permission changes.                                            |
| **Searchable audit trail**   | Look up any data access event by user, date, module, country, or action type.                                                      |
| **Automated alerts**         | System flags unusual activity: bulk export attempts, access from unexpected locations, repeated failed logins, permission changes. |
| **Quarterly access reviews** | Built-in workflow to review and clean up permissions — ensures no stale or over-provisioned accounts.                              |

---

> **Bottom line:** WageIndicator decides who can access what, what actions they can take, and what data leaves the platform. Every decision is enforced by the system and every action is logged. The platform is built for WageIndicator to be the gatekeeper — not just a user of the system.
