# NIST AI RMF: Govern, Map, Measure, Manage

## Purpose
This note is designed to support the appendix deck and the board pack narrative. It translates the Nordhaven-LumaPay scenario into the `NIST AI RMF` operating model.

## Scenario Context
- Nordhaven acquires `80%` of LumaPay
- LumaPay operates four in-scope AI systems
- The combined entity will spend `12–18 months` in a transitional operating state
- LumaPay has weak documentation, copied live `PII` in `test`, no dedicated security team, and immature AI lifecycle controls

---

## Govern

### Objective
Create the accountability, policy, and oversight structure that lets Nordhaven take ownership of inherited AI risk without disrupting business value.

### What Govern Means In This Scenario
- Define who owns each AI system, model, MCP server, dataset, and third-party dependency
- Align Nordhaven and LumaPay on risk appetite for:
- opacity
- autonomy
- dependency
- drift
- scale asymmetry
- Establish board-level and Group Risk Committee reporting for inherited AI risk
- Create interim decision rights for deployments, exceptions, and incident escalation

### Govern Actions
- Stand up a unified AI registry across the combined entity
- Assign accountable executives and technical owners for all four AI applications
- Approve interim AI operating rules for the integration period
- Define how shadow AI, MCP tools, and lower-environment data use must be disclosed
- Create a single AI risk forum for governance, cyber, and operational review

### Govern Questions For The Appendix
- Who owns `LumaCredit-EU` as a high-risk credit-decision system?
- Who approves prompt, model, and MCP tool changes?
- Which body owns exceptions like copied `PII` in `test`?

---

## Map

### Objective
Understand the inherited AI estate, the data flows, the actors, and the business context well enough to classify real risk.

### What Map Means In This Scenario
- Inventory the four AI systems and their dependencies
- Identify cross-border data flows into `US-hosted` services
- Identify internal and third-party MCP-connected tools
- Tag each system by substrate properties and lifecycle stages
- Make the transition-state architecture visible, not just the target-state design

### Map Actions
- Build the combined inventory for models, prompts, datasets, MCP services, APIs, vendors, and environments
- Map `test` versus `production` data handling for each system
- Record where live `PII` exists outside intended boundaries
- Identify human approval points and override paths
- Map each system to governance, operational, and cyber lenses

### Map Questions For The Appendix
- Which systems are high-risk, customer-facing, internal agentic, or third-party?
- Which MCP tools can act on customer, case, or document data?
- Where are the largest interim gaps between LumaPay’s and Nordhaven’s control assumptions?

---

## Measure

### Objective
Assess the severity, likelihood, and current control posture of inherited AI risk using evidence rather than intuition.

### What Measure Means In This Scenario
- Evaluate drift, data quality, prompt abuse, tool misuse, third-party dependence, and governance maturity
- Tie findings to named standards and clauses
- Use KRIs and evidence expectations rather than broad statements like “AI risk is high”

### Measure Actions
- Create the `10–12` risk register extract with owners, impacts, and KRIs
- Assess each system against key framework expectations:
- `EU AI Act`
- `GDPR` / `UK GDPR`
- `ISO/IEC 42001`
- `ISO/IEC 27001`
- `NIST CSF`
- `OWASP LLM Top 10`
- Define measurable indicators such as:
- percentage of AI assets in the unified registry
- number of lower-environment datasets containing live `PII`
- drift threshold breaches
- manual override rate
- MCP permission exceptions
- vendor SLA or outage breaches

### Measure Questions For The Appendix
- What are the top `5–7` board-level risks?
- What evidence is missing pre-close?
- Which interim controls reduce exposure fastest?

---

## Manage

### Objective
Treat the highest risks through practical, prioritized action while the combined entity is still in transition.

### What Manage Means In This Scenario
- Reduce inherited risk without waiting for full platform harmonization
- Prioritize the highest-impact issues for the first `100 days`
- Focus on realistic actions Nordhaven can actually enforce

### Manage Actions
- Stop further copying of unredacted `PII` into `test`
- Constrain or review MCP tool permissions for `LumaAssist Chat` and `AutoUnderwriter Agent`
- Put manual fallback and incident playbooks around `FraudShield`
- Introduce stage-gate approvals for model and prompt changes
- Centralize key logging, trace review, and Datadog monitoring
- Build the maturity roadmap from initial to optimised

### Manage Questions For The Appendix
- Which actions are `pre-close critical`?
- Which actions belong in day `0–30`, `31–60`, and `61–100`?
- Which residual risks should remain explicitly accepted by leadership during the interim period?

---

## Quick Mapping By Application

| Application | Govern | Map | Measure | Manage |
| --- | --- | --- | --- | --- |
| `LumaCredit-EU` | Confirm high-risk AI ownership and accountability | Map data lineage, approval flow, and cross-border storage | Measure drift, approval bias, and evidence gaps | Prioritize data masking, logging, and model governance uplift |
| `LumaAssist Chat` | Define prompt and escalation authority | Map MCP tools, prompt flows, and trace locations | Measure leakage, hallucination, and prompt abuse rates | Tighten tool permissions, trace controls, and response guardrails |
| `AutoUnderwriter Agent` | Define manual-approval authority and agent scope | Map agent tools, document flows, and permissions | Measure unsafe tool use, overrides, and traceability gaps | Restrict MCP authority, improve approvals, and monitor agent behavior |
| `FraudShield` | Assign vendor-risk ownership | Map external dependencies, contracts, and fallback paths | Measure outage exposure, score drift, and vendor assurance gaps | Strengthen fallback design, contract review, and supplier oversight |
