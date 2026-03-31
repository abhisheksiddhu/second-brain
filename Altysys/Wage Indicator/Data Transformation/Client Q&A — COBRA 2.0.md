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

---

**4. The LLM will need an API where visitors can query. The scope of what the LLM is allowed to answer needs to be strictly guided.**

Agreed — this is a core design principle. We enforce strict boundaries on what the LLM can access and respond to:

- The LLM connects to the database through **restricted database users** that only have access to approved tables
- This prevents the model from accessing, referencing, or exposing data outside its permitted scope — even if a user tries to manipulate the query (a technique called prompt injection)
- Additional guardrails at the application layer ensure responses stay within defined topic boundaries

The result: the LLM answers only what WageIndicator wants it to answer, using only the data WageIndicator has approved for public or subscriber access.

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

Absolutely — we just need access. One question for your side: should we host the repository on WageIndicator's infrastructure, or are you open to using GitHub?

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
