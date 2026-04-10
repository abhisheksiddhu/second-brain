# Client Q&A — COBRA 2.0

---

**1. Automated law change detection — what do you have in mind?**

Our approach is a monitored pipeline:

- We register the official legal sources WageIndicator tracks today (government gazettes, regulatory portals, etc.)
- A scheduled monitor checks those sources periodically and detects changes
- When a change is found, our AI pipeline extracts the relevant updates and scores them for significance
- The changes appear in a **review queue** — a human reviewer always approves before anything enters the Labour Law database

Nothing goes into the system without human sign-off. The automation handles the tedious part (watching hundreds of sources) while your team retains full editorial control.

---

**2. What will the estimated monthly costs be for the LLM?**

LLM costs are usage-based — they depend on the volume of documents processed (OCR pages) and the number of chat interactions. We cannot give a reliable monthly figure at this stage without knowing actual usage patterns.

During the **Discovery phase**, we'll profile your real document volumes and query patterns and provide a concrete cost estimate with low/medium/high usage scenarios.

---

**3. Will Altysys connect the LLM to use and learn from the connected databases?**

The LLM will have access to database metadata (table structures, field descriptions, data dictionaries) so it can answer questions intelligently and generate accurate queries. However, **fine-tuning the LLM on your data is not in scope** — the model works with your data at query time, it doesn't permanently absorb or "learn" from it. This keeps the system predictable, auditable, and avoids the risks of model drift.

To clarify what happens when data or schema changes:

- **Data changes** (new CBAs added, labour law records updated): The system picks these up automatically. When a user asks a question, the system queries the current database — so new or updated records are immediately available. The only background task is regenerating search embeddings for new/changed documents, which runs automatically.
- **Schema changes** (new fields, new tables, restructured data models): These require a configuration update — the LLM's knowledge of available tables and fields needs to be refreshed. This is a managed change, not a retraining exercise. We update the metadata definitions and field mappings; the model itself doesn't change.

In neither case is the model "retrained." Your data stays in your database — the LLM reads it on demand, it doesn't memorize it.

---

**4. The LLM will need an API where visitors can query. The scope of what the LLM is allowed to answer needs to be strictly guided.**

Agreed — this is a core design principle. We enforce strict boundaries on what the LLM can access and respond to:

- The LLM connects to the database through **restricted database users** that only have access to approved tables
- This prevents the model from accessing, referencing, or exposing data outside its permitted scope — even if a user tries to manipulate the query (a technique called prompt injection)
- Additional guardrails at the application layer ensure responses stay within defined topic boundaries

The result: the LLM answers only what WageIndicator wants it to answer, using only the data WageIndicator has approved for public or subscriber access.

**A note on infrastructure:** The pricing we've shared (Mistral Document AI at ~£8–20/month for OCR, Mistral Large at ~£1.26/month for chat) is based on Mistral's **public API**. Mistral does not currently offer private/dedicated endpoints for their Document AI product. For document processing, data is sent to Mistral's EU-hosted API — it is processed in the EU and not used for training, but it does leave your network.

If full data isolation is a requirement, the alternative is **self-hosting open-source models on OVH GPU instances**. This keeps everything on WageIndicator infrastructure, but comes with different cost and quality trade-offs (see Q&A #5 in the follow-up batch below). We'll evaluate both paths during Discovery and recommend based on your cost tolerance and privacy requirements.

---

**5. We will connect to this API via the public website. We already have an access layer for Living Wages. But if Altysys has a better option, let us know.**

Your existing access layer (email + SMS registration, subscription tiers) can absolutely be reused — we'll expose the LLM as a standard API endpoint that your website integrates with, just as it would any other backend service.

If you'd like, we can review your current implementation during Discovery and recommend improvements (rate limiting, usage analytics, abuse prevention). But this is not a blocker — your existing approach works, and we'll design the API to be compatible with it.

---

**6. For the CBA database: We need a dynamic survey/form system — admins should be able to add questions, set data types, add relevance rules, etc.**

This is core scope for COBRA 2.0. What you're describing is a **dynamic form engine**, and we're building it as a first-class admin module:

- **Question management:** Admins add, edit, reorder, or archive questions from a UI — no developer involvement needed
- **Data types supported:** Text, number, date, dropdown (static list or API-fed), multi-select, boolean, free text
- **Required/optional flags:** Configurable per question by admins
- **Relevance rules (conditional visibility):** "If Question A = X, show Question B" — configured through a visual rule builder, not hard-coded. Supports nested logic (conditions within conditions)
- **External API dropdowns:** Same pattern you use today — admin specifies the API endpoint and field mapping, the dropdown populates dynamically

Your current survey workflow is preserved and improved — the difference is that everything is configurable through the admin interface instead of requiring technical changes.

---

**7. Can Altysys use their own git repository?**

Apologies for the confusion in the proposal — this has been discussed. We'll use a repository that both teams can access. Could you confirm your preference: should we host it on WageIndicator's infrastructure (e.g., self-hosted GitLab), or are you open to using GitHub?

---

**8. After converting a CBA document to HTML, we want clean, well-structured output (proper headings, ordered lists, etc.). Can we ensure quality before finalizing?**

Yes. Our document processing pipeline uses AI-based document conversion that preserves the original layout and structure — headings, lists, tables, and formatting come through cleanly.

That said, no automated conversion is perfect for every document. We'll build an **editor review step** where your team can inspect and correct the HTML before it's finalized in the system.

During Discovery, we'll test your actual documents against **multiple LLMs and document AI tools** and decide based on quality and cost. Candidates include Mistral Document AI, and options like **Dragon LLM** — a Paris-based model specifically built for regulated industries — along with other EU and open-source alternatives. The goal is to find the best fit for your document types while staying within European provider preferences.

---

**9. Does OVH have any vendor lock-in or minimum commitment?**

No. OVH operates on a **pay-as-you-go** model with billing as granular as hourly. There is no minimum contract period — you can scale up or down as needed without lock-in.

---

**10. Does OVH offer discounts for long-term commitments or NGO accounts?**

- **Long-term commitments:** Yes — OVH offers a Savings Plan for reserved capacity, with discounts **up to 54% on 3-year commitments**
- **NGO-specific pricing:** There is no formal NGO discount program. However, their sales team has indicated they are open to discussing volume-based or mission-based pricing depending on the contract size

We can facilitate an introduction to their sales team if WageIndicator wants to explore this further.

---

**11. Are cloud GPU instances available in the Netherlands?**

OVH GPU instances are currently available in **France, UK, Germany, and Poland** — not the Netherlands specifically. However, all of these are EU-region datacenters and comply with the same data sovereignty requirements. Germany or France would be the natural choice given proximity and latency considerations.

---

---

# Follow-Up Q&A — April 2026

---

**1. For UI translation strings, we have a centralized Weblate instance. Can we add COBRA, Labour Law, and Pensions as new projects?**

Yes — that's the right approach. We'll integrate with your self-hosted Weblate for all UI translation strings. COBRA 2.0, Labour Law, and Pensions each become separate Weblate projects, and we'll reuse your Universal project for shared generic strings (ok, cancel, next, etc.).

To be clear on the boundary: **Weblate handles UI strings only** — the labels, buttons, and system messages. Translatable _content_ (labour law texts, CBA clauses, pension descriptions) lives in COBRA 2.0's own content management layer with its own editorial and translation workflow, since that content requires versioning, review, and approval that goes beyond string translation.

---

**2. Will all AI features use RAG, or will some use prompt engineering or fine-tuning?**

Different features use different techniques — RAG is not the only approach:

| Feature                                              | Technique                           | Why                                                                                         |
| ---------------------------------------------------- | ----------------------------------- | ------------------------------------------------------------------------------------------- |
| **CBA querying** (user asks a question)              | RAG                                 | Retrieves relevant CBA passages, then generates an answer grounded in actual data           |
| **CBA structure detection** (parsing a new document) | Prompt engineering                  | Structured prompts with examples guide the model to identify headings, articles, clauses    |
| **Field prefill** (suggesting annotation values)     | Prompt engineering                  | The model is given document context and field definitions, asked to extract specific values |
| **Confidence scoring**                               | Pipeline logic + prompt engineering | Combines model confidence signals with rule-based validation                                |

**Fine-tuning is not in scope.** Fine-tuning means permanently modifying the model's weights with your data — it's expensive, requires ongoing maintenance, and introduces model drift risk. Our approach keeps the model generic and feeds it your data at query time, which is more maintainable, auditable, and significantly cheaper to operate.

---

**3. Does the AI layer need to be retrained or updated when the database changes?**

No retraining is needed — for either data changes or schema changes.

- **Data changes** (new CBAs, updated labour law records): The system picks these up automatically. Queries always run against the current database. The only background task is regenerating search embeddings for new/changed documents, which runs as an automated pipeline — no manual intervention.
- **Schema changes** (new fields, new tables, restructured models): These require a configuration update — we refresh the metadata definitions and field mappings that tell the LLM what's available. This is a managed change done during a release, not a retraining exercise.

In neither case does the model itself change. Your data stays in your database — the LLM reads it on demand, it doesn't memorize it.

---

**4. When you mention using Mistral, would this involve private endpoints or public API usage?**

The infrastructure costs we've shared are based on **Mistral's public API**. To be transparent:

- **Mistral Document AI** (for OCR/document conversion): This is only available as a public API. Mistral does not currently offer private/dedicated endpoints for this product. Your documents are sent to Mistral's EU-hosted servers for processing — they are not used for model training, but they do leave your network.
- **Mistral Large** (for chat/query/extraction): Private endpoints are available through Mistral's enterprise offering, but at higher cost.

If full data isolation is a hard requirement, the alternative is **self-hosting open-source models on OVH GPU instances** — which keeps everything on WageIndicator's infrastructure. The trade-offs are covered in the next question.

---

**5. Self-hosting vs. API — cost, performance, and privacy comparison?**

This is an important decision, especially given cost sensitivity. Here's the honest trade-off:

| Factor           | Self-Hosted (OVH GPU)                                                                                    | Public API (Mistral)                                                                                                  |
| ---------------- | -------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Model size**   | Limited to what fits on your GPU — typically 7B–70B parameter models                                     | Access to Mistral's largest models                                                                                    |
| **Performance**  | Very good for structured tasks (extraction, prefill). May be weaker on complex multi-document reasoning  | Best available quality across all task types                                                                          |
| **Cost**         | Higher fixed cost (~€1,500–3,000/month for GPU instance), but **unlimited usage** — predictable and flat | Very low entry cost (~£100/month at current volumes), but **scales with usage** — unpredictable if query volumes grow |
| **Data privacy** | Maximum — data never leaves your infrastructure                                                          | Data processed in EU, not used for training, but leaves your network                                                  |
| **Maintenance**  | Your team (or Altysys) manages model updates, GPU scaling, uptime                                        | Provider handles everything                                                                                           |

**Our recommendation given cost concerns:** Start with the public API during Phase 1 — it's the fastest path to delivery and the cheapest at your current volumes (~£30/month total for OCR + chat). During Discovery, we'll benchmark your actual workloads against self-hosted models. If volumes grow significantly or privacy requirements tighten, we can switch to self-hosted — the architecture is provider-agnostic, so this is a configuration change, not a rebuild.

---

**6. Cloud provisioning — WageIndicator wants Altysys to provision the infrastructure.**

Understood. We'll handle the cloud infrastructure provisioning using WageIndicator's payment account and credentials. This makes sense — our team knows the server requirements, sizing, and configuration needed for COBRA 2.0.

Based on our estimates, the **core production infrastructure costs approximately £100/month** on OVH:

| Service                | Specification              | Est. Monthly Cost |
| ---------------------- | -------------------------- | ----------------- |
| Compute                | 4 vCore / 16 GB RAM        | £45.40            |
| Object Storage         | 50 GB                      | £0.35             |
| PostgreSQL (Managed)   | 2 vCore / 4 GB RAM / 80 GB | £46.80            |
| Gateway                | Size M — 500 Mbps          | £7.00             |
| Bandwidth              | Up to 1 TB/month           | Free              |
| Kubernetes             | Up to 100 nodes            | Free              |
| **Total (core infra)** |                            | **~£100/month**   |

Adding dev/staging environments adds ~£50–80/month. LLM API costs (OCR + chat) add ~£10–30/month at current volumes.

We'll document the full infrastructure setup so your IT team has full visibility and can manage it independently going forward.

---

**7. The proposal mentions React. Is this going to be Vue.js?**

Yes — apologies for the outdated reference in the proposal. Based on our discussion, we'll be using **Vue.js** for the frontend. The proposal text should have been updated to reflect this; we'll correct it in the next revision.

---

**8. The recurring monthly LLM costs seem very low — €1.45/month. How does the LLM actually work?**

Good question — let's clarify both the architecture and the cost.

**How the LLM works for CBA queries:**

A question like _"give me the best clauses for long-time sickness in the garment industry"_ goes through multiple steps:

1. The LLM interprets the natural-language question and identifies the intent (topic: sickness, industry: garment)
2. The system searches the database using vector similarity + structured filters to retrieve relevant CBA clauses
3. The LLM **reads the retrieved clauses** and synthesizes an answer — ranking, comparing, and summarizing across multiple documents
4. The response is returned with source citations

So no — the LLM is not just decoding the question into a database query. It's doing real reasoning over retrieved content. That's what makes the answers useful, and that's also what drives token usage.

**On the £1.26 figure:**

That estimate is based on a specific usage assumption: **20 internal admin users, 30 conversations/month each, 10 messages per conversation.** At that volume, Mistral Large's token pricing really is that low — roughly £1.26/month for the chat component.

Here's the full picture including OCR:

| Component                     | Assumption                                | Est. Monthly Cost |
| ----------------------------- | ----------------------------------------- | ----------------- |
| OCR (document conversion)     | 50 documents/month × 100 pages avg        | £8–20             |
| Chat / Query (internal admin) | 20 users × 30 conversations × 10 messages | £1.26             |
| **Total LLM cost**            |                                           | **~£10–22/month** |

The costs are genuinely low at these volumes because Mistral's pricing is competitive and your usage is modest. **Where costs would increase:** if you open the chat API to public website visitors at scale (thousands of queries/month), or if documents grow significantly in size/volume. We'll model those scenarios during Discovery.

The key message: at your current scale, LLM costs are a rounding error compared to infrastructure (£100/month) and engineering effort. Cost only becomes a concern if public-facing query volumes grow substantially.
