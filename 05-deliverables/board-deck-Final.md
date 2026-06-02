---
marp: true
theme: default
paginate: true
---
# Board Deck Final


## Cover Slide
**Title**
`Nordhaven–LumaPay AI Risk Review`

**Subtitle**
Board-level view of acquisition-related AI governance, operational, and cyber risk

**Prepared By**
`Nordhaven–LumaPay AI Risk Taskforce`

---

## Slide 1: Executive Summary
**Headline**
Nordhaven is acquiring a high-growth AI-intensive fintech whose control maturity is materially below Nordhaven’s existing risk baseline.

**Key Message**
The transaction creates immediate AI risk not because LumaPay lacks value, but because Nordhaven inherits regulated credit models, customer-facing LLM workflows, agentic tooling, third-party AI dependence, and copied live `PII` in `test` before governance and security controls are aligned.

**Top Board Risks**
- No named Day 1 owner, RACI, or board-approved AI appetite exists for the combined AI estate, creating an accountability gap before control uplift is complete.
- Unknown shadow AI and undocumented tools may still affect customers while remaining invisible to Nordhaven, auditors, and the Group Risk Committee.
- `LumaCredit-EU` appears to operate as a high-risk credit-decision system with incomplete EU AI Act evidence, weak explanation capability, and unproven fairness monitoring.
- `LumaAssist Chat` and `AutoUnderwriter Agent` rely on `MCP` tool access that could turn prompt failure or over-broad permissions into direct data or workflow misuse.
- `FraudShield` introduces third-party opacity, continuity, and change-of-control risk during the transaction window.
- Live customer `PII` has been copied into lower environments without masking, creating immediate privacy, confidentiality, and regulatory exposure.

**Board Decisions Requested**
- Approve an interim AI governance model for the integration period.
- Approve urgent remediation for copied live `PII` in `test`.
- Endorse the `100-day` AI integration plan and interim AI risk-appetite statements.

---

## Slide 2: Why This Deal Is An AI Risk Stress Test
**Headline**
This is not a standard technology integration; it is the acquisition of an AI estate with regulatory, operational, and cyber exposure embedded in the business model.

**Core Points**
- LumaPay’s AI assets are central to product delivery in `BNPL`, SME lending, customer servicing, and fraud controls.
- Traditional diligence would not fully surface model lineage, prompt flows, MCP-connected tool risk, drift exposure, or incomplete governance evidence.
- The interim integration state increases attack surface, duplicates control boundaries, and introduces uncertainty over ownership, approval rights, and escalation paths.
- Cross-border data flows into `US-hosted` environments increase scrutiny under `GDPR`, `UK GDPR`, and related transfer obligations.

**Framework Anchors**
- `NIST AI RMF`
- `ISO/IEC 42001`
- `GDPR`
- `EU AI Act`

---

## Slide 3: LumaPay At A Glance
**Headline**
LumaPay is small, developer-heavy, and product-led, with strong AI exposure but thin control capacity.

**Current-State Profile**
- `200` employees
- `100` developers
- `5` platform engineers
- no dedicated security team
- no dedicated `GRC` team
- two AWS accounts: `test` and `production`
- no `CSPM`, `DSPM`, or modern AI security tooling
- copied live `PII` into `test`

**Comparison To Nordhaven**
- Nordhaven operates at enterprise scale with `10,000` employees, dedicated security and `GRC`, formal risk processes, and mature cloud and AI security tooling.
- The acquisition therefore transfers risk faster than it transfers control.

**Board Implication**
Nordhaven is not only acquiring systems; it is acquiring a materially different control culture and operating tempo.

---

## Slide 4: AI Systems In Scope
**Headline**
The inherited AI estate contains four distinct systems, each with a different risk profile and regulatory significance.

**Systems**
- `LumaCredit-EU`
  Credit-decision model stack for lending outcomes. Most exposed to high-risk AI governance, explainability, drift, and data quality requirements.
- `LumaAssist Chat`
  Customer-facing LLM assistant. Most exposed to prompt injection, data leakage, and over-broad MCP-connected access.
- `AutoUnderwriter Agent`
  Agentic internal workflow combining model reasoning with underwriting tool access. Most exposed to autonomy, traceability, and unsafe tool use.
- `FraudShield`
  Third-party fraud model. Most exposed to supplier opacity, contract dependence, and continuity risk.

**Visual**
Insert the four architecture diagrams from the share pack.

---

## Slide 5: Top 6 AI Risks
**Headline**
The most material risks are inherited-state control failures that can create customer harm, regulatory breach, or operational disruption before target-state integration is complete.

| Risk | Why It Matters | Lifecycle Stage | Primary Reference |
| --- | --- | --- | --- |
| `R-12` Governance misalignment during parallel operations | No single combined-entity accountability model means inherited risk may be accepted accidentally rather than by Board decision. | Design / Deploy / Monitor | `NIST AI RMF` Govern; `ISO/IEC 42001` Cl.5 |
| `R-13` Shadow AI and undocumented tools | Undiscovered LumaPay AI can create customer, regulatory, and evidence risk from Day 1 while remaining outside the registry. | Design / Deploy | `NIST AI RMF` Map; `EU AI Act` Art. 6-7 |
| `R-02` High-risk AI governance gap in `LumaCredit-EU` | Nordhaven may inherit an Annex III credit-decision system without complete model cards, conformity evidence, accountability, validation, or oversight records. | Full lifecycle | `EU AI Act` Annex III 5(b), Art. 9-17; `ISO/IEC 42001` |
| `R-08` MCP tool overreach in `AutoUnderwriter Agent` | Excessive tool permissions could turn reasoning failure into direct misuse of underwriting, identity, affordability, or document systems. | Develop / Deploy | `ISO/IEC 27001`; `OWASP Agentic`; `OWASP MCP`; `NIST CSF` |
| `R-10` Fraud vendor change-of-control disruption | Critical third-party fraud services may become unstable, contested, or unavailable during the transaction. | Deploy | `DORA` Art. 28, 30; `ISO/IEC 27036` |
| `R-01` Unredacted `PII` in `test` | Live personal data is already outside intended production boundaries, creating immediate privacy and security exposure. | Data / Develop | `GDPR` Art. 5, 25, 32; `ISO/IEC 27001` A.8.31 |

**Takeaway**
These are not isolated issues. They compound each other during the interim operating phase.

---

## Slide 6: Pre-Close Due-Diligence Priorities
**Headline**
Pre-close diligence should focus on the evidence gaps most likely to affect legal exposure, service continuity, and regulator defensibility.

**Priority Evidence Requests**
- Environment inventory and proof of whether live `PII` exists in `test` or other lower environments
- Complete AI asset inventory, including shadow tools, departmental scripts, informal assistants, and registry gaps
- `LumaCredit-EU` model documentation, validation evidence, and ownership records
- Model cards or system cards for all four in-scope systems
- Board-level AI governance policy, RACI, decision-rights matrix, and risk-appetite statement
- `MCP` inventory, tool permission matrix, and approval model for LLM and agent workflows
- Logging, trace-retention, and redaction controls for prompts and AI observability data
- Vendor contracts, assignment rights, SLAs, audit rights, incident rights, and fallback assumptions for `FraudShield`, foundation models, and critical suppliers
- Human-in-the-loop evidence, reviewer rationale samples, and override-rate dashboards for credit and underwriting decisions

**Board Message**
If these artefacts cannot be produced quickly, Nordhaven should assume higher inherited risk and govern accordingly.

---

## Slide 7: Governance, Operational, And Cyber Stress Test
**Headline**
The transaction should be viewed through three lenses simultaneously because failures in one area cascade into the others.

**Governance Lens**
- Day 1 accountability owner not named
- shadow AI inventory incomplete
- RACI and decision rights not documented across lifecycle stages
- AI risk appetite and escalation triggers not approved
- model cards, conformity evidence, and documentation incomplete

**Operational Lens**
- drift risk in credit and fraud systems
- orphaned knowledge in a small engineering team
- weak lower-environment controls
- insufficient fallback and monitoring maturity

**Cyber Lens**
- prompt injection
- over-broad `MCP` access
- copied live `PII`
- exposure in logs, traces, APIs, and duplicated interim environments

**Takeaway**
The interim phase amplifies all three lenses at once.

**Five Governance Choices**
- Name the combined-estate accountability owner.
- Approve interim risk appetite and breach triggers.
- Require a unified AI registry and shadow AI discovery.
- Establish RACI and stage-gates across all lifecycle stages.
- Set escalation authority to halt or constrain high-risk systems.

---

## Slide 8: Interim AI Risk Appetite And Tolerance
**Headline**
Nordhaven should operate with low or very low appetite for inherited AI risks that affect regulated decisions, customer treatment, or unbounded third-party dependence.

| Property | Interim Appetite | Tolerance Direction |
| --- | --- | --- |
| `Opacity` | Low | No high-impact system should remain materially undocumented beyond `60` days post-close. |
| `Autonomy` | Very low | `0` autonomous high-impact credit or customer actions without human approval. |
| `Dependency` | Moderate, actively managed | All critical AI vendors and MCP-connected tools must have owners, inventory entries, and fallback assumptions within `60` days. |
| `Drift` | Low | All in-scope production models need thresholds, review owners, and escalation routes within `60` days. |
| `Scale Asymmetry` | Very low | No material AI expansion without registry entry, owner assignment, and interim governance coverage. |

**Red-Line Conditions**
- copied live `PII` in lower environments
- unapproved autonomous high-impact decisions
- critical AI dependencies with no owner or fallback
- production AI changes outside the interim stage-gate
- unexplained high-risk credit or underwriting decision in production
- customer-affecting AI system operating outside the unified AI registry
- human review that lacks rationale, challenge evidence, or meaningful override monitoring

---

## Slide 9: 100-Day AI Integration Plan
**Headline**
Nordhaven can materially reduce inherited AI risk in the first `100 days` without waiting for full platform harmonization.

**Day `0–30`**
- stop further copying of live `PII`
- appoint a named Day 1 AI accountability owner
- inventory AI systems, dependencies, MCP tools, and shadow AI
- establish interim AI governance forum, RACI, and risk appetite
- reduce high-risk MCP permissions

**Day `31–60`**
- classify all four AI systems under `EU AI Act` risk tiers
- complete `ISO/IEC 42001` gap analysis and model / system cards
- build minimum evidence pack for credit decisioning
- introduce drift thresholds and trace controls
- complete critical vendor change-of-control review

**Day `61–100`**
- run targeted red-team and abuse-case testing
- publish AI-specific incident playbooks
- deploy Board AI Risk Dashboard and first monthly KRI review
- formalize unified AI registry and stage-gate model

**Board Message**
The objective is not perfection in `100` days; it is to move the combined entity from opaque inherited risk to governed, measurable, and Board-visible risk.

---

## Slide 10: Standards Traceability

**Headline**
The proposed controls are clause-traceable across AI governance, privacy, operational resilience, cyber, and supplier-risk frameworks.

| Standard | Where It Applies | Primary Capstone Use |
| --- | --- | --- |
| `NIST AI RMF` | All four systems | Board structure across `Govern`, `Map`, `Measure`, `Manage` |
| `EU AI Act` | `LumaCredit-EU`; classification review for AutoUnderwriter | Annex III high-risk classification, Art. `9-17`, Art. `72` |
| `GDPR` / `UK GDPR` | Personal data, traces, lower environments, cross-border flows | Data minimisation, security, DPIA, transfer evidence |
| `ISO/IEC 42001` | AI management system | Roles, risk assessment, treatment, lifecycle controls, monitoring |
| `ISO/IEC 27001` | MCP tools, logging, access, environments | Access control, supplier controls, logging, secure development, test-production segregation |
| `DORA` / `ISO/IEC 27036` | FraudShield and critical suppliers | Vendor continuity, change-of-control, audit rights, fallback planning |
| `OWASP LLM`, `OWASP Agentic`, `OWASP MCP`, `MITRE ATLAS` | LumaAssist and AutoUnderwriter | Prompt injection, excessive agency, MCP authorization, adversarial testing |

**Board Message**
Every top risk and material control should trace back to the technical appendix, not stand alone as an assertion.

---

## Slide 11: Board Decisions And Escalation Asks
**Headline**
The Board should leave this review with explicit ownership, funding, and escalation decisions.

**Requested Decisions**
- Approve the interim AI governance forum and decision-rights model.
- Approve urgent remediation funding for copied live `PII` in `test`.
- Endorse high-priority control uplift for `LumaCredit-EU`, `LumaAssist Chat`, and `AutoUnderwriter Agent`.
- Require monthly inherited-state AI risk reporting until material gaps are closed.
- Require pre-close legal review of critical AI vendor contracts and fallback assumptions.

**Escalation Ask**
If material evidence gaps remain unresolved pre-close, the Group Risk Committee should require explicit acceptance of residual inherited AI risk rather than assuming it will be absorbed by general post-merger integration.

---

## Editing Notes For The Team
- Replace placeholder phrasing with workstream-specific detail as governance, cyber, and regulatory inputs arrive.
- Keep slide `1`, slide `5`, slide `8`, and slide `9` tightly aligned; those are the backbone of the board story.
- If the deck needs to be shortened, preserve slides `1`, `5`, `8`, `9`, and `10` first.
