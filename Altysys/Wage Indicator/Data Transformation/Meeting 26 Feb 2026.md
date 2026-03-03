**COBRA – Current State & COBRA 2.0**

- COBRA is a 25+ year old system built on PostgreSQL + CSV files, with data spread across Dropbox and Airflow tables
- Covers 180 countries, 26 years of data, granular city-block level, quarterly cadence — very large scale
- Have mostly consistent forma of questions and data allowing a language service layer serving content in 70 languages
- System has become slow and inflexible due to incremental additions over the years
- Immediate priority is the **CBA & Labour Law database** — other databases may follow in later phases
- Agreed to proceed with **COBRA 2.0** focused on scalability, flexibility, and future-proof architecture

---

**Cloud Infrastructure**

- Single region (Europe) deployment confirmed — no multi-region or multi-cloud needed
- Data is non-PII / summary in nature, so no compliance-sensitive storage concerns
- Client has a strict **no US vendor** policy — leaning toward a hybrid of self-hosted open source and European cloud providers
- Self-hosted options: Kubernetes, MinIO, GitLab, Nextcloud, Airflow on bare-metal (Hetzner, OVHcloud)
- European managed cloud options being considered: Hetzner Cloud, Scaleway, OVHcloud, Exoscale, Open Telekom Cloud, IONOS
- Existing Dropbox to be retained during transition period
- Phased, project-by-project migration preferred over a big-bang cutover
- Key principle: a deliberate, governed migration strategy rather than each project deciding independently

---

**Tech Stack & Project Walkthrough**

- Agreed first step: walk through the project map to understand existing functionality and workflows
- Can connect with their IT person if specific clarifications are required during proposal prep
- Client agreed to share web portal URL and login credentials
- Team to explore the application firsthand and document observations on processes, workflows, and UX
