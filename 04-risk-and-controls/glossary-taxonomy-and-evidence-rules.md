# Glossary, Taxonomy, And Evidence Rules

## Purpose
Use this document as the quality gate for Deliverable A and Deliverable B. It keeps the board pack, technical appendix, risk register, due-diligence checklist, and `100-day` roadmap aligned to the same glossary, taxonomy, lifecycle model, and evidence standard.

## Scenario Terms

| Term | Working Definition For This Capstone | Use In Deliverables |
| --- | --- | --- |
| `Nordhaven` | Acquiring institution and control-oriented parent entity. | Use when referring to inherited accountability, Group Risk Committee reporting, and target-state control uplift. |
| `LumaPay` | Acquired `UK-regulated fintech` focused on embedded `BNPL` and `SME lending`. | Use when referring to inherited AI systems, existing operating weaknesses, and current-state evidence gaps. |
| `Combined entity` | Nordhaven and LumaPay during the acquisition and integration period. | Use when describing interim accountability, shared control ownership, and `100-day` integration actions. |
| `Parallel operations window` | The `12-18 month` period where Nordhaven and LumaPay operate with mixed infrastructure, suppliers, policies, and controls. | Use to explain governance misalignment, transitional accountability gaps, and inherited-state risk. |
| `Inherited-state risk` | Risk that exists at or before close because of LumaPay's current AI estate and control maturity. | Use separately from target-state risk so the board does not confuse plans with achieved control. |
| `Target-state uplift` | The future Nordhaven-aligned operating model after interim controls and platform harmonisation mature. | Use for post-`100-day` actions, not for claims about current control effectiveness. |

## AI System Terms

| Term | Working Definition For This Capstone | Examples |
| --- | --- | --- |
| `AI system` | A system that uses model, LLM, rules, agentic, or vendor-hosted AI capability to support or influence business decisions or operations. | `LumaCredit-EU`, `LumaAssist Chat`, `AutoUnderwriter Agent`, `FraudShield` |
| `High-risk AI` | An AI use case that affects credit access, underwriting, customer outcomes, legal rights, or material financial decisions and therefore requires stronger governance, evidence, oversight, and monitoring. | `LumaCredit-EU`; parts of `AutoUnderwriter Agent` |
| `LLM assistant` | A customer-facing or employee-facing interface that generates natural-language responses and may retrieve or process customer data. | `LumaAssist Chat` |
| `Agentic workflow` | A workflow where an AI component can chain reasoning, retrieval, and tool calls to produce recommendations or actions. | `AutoUnderwriter Agent` |
| `MCP tool` | A callable tool or service exposed to an AI workflow for retrieving data, invoking business logic, or interacting with internal systems. | CRM lookup, affordability API, identity check, document retrieval |
| `Vendor-hosted model` | AI capability operated by a third party where LumaPay has limited visibility into model design, assurance, resilience, or change control. | `FraudShield` |

## Risk And Control Terms

| Term | Working Definition For This Capstone | Required Use |
| --- | --- | --- |
| `Risk` | A plausible event, weakness, or condition that could harm customers, operations, compliance, resilience, or enterprise value. | Write as a scenario-specific statement, not as a generic theme. |
| `Control` | A preventive, detective, corrective, or governance measure that reduces likelihood, impact, or uncertainty. | Tie each material control to a risk and framework clause or function. |
| `Treatment` | The action selected to reduce, transfer, accept, or avoid a risk. | Use in the risk register and roadmap. |
| `KRI` | A measurable indicator that shows whether risk is increasing, stable, or reducing. | Include at least one KRI for every risk register row. |
| `Evidence artefact` | A document, log, system export, dashboard, contract, decision record, or approval record that proves whether a control exists and operates. | Use in due-diligence requests and appendix traceability. |
| `Pre-close critical` | Evidence or control decision needed before or at transaction close because it affects value, liability, continuity, or go/no-go risk acceptance. | Use in the due-diligence checklist. |
| `Post-close urgent` | Evidence or control action that can be handled in the `100-day` plan but must not drift into normal backlog. | Use in the due-diligence checklist and roadmap. |

## Enterprise Lenses

Use these lenses exactly. A risk may have more than one lens, but one should be dominant in the board narrative.

| Lens | Definition | Typical Risk Signals |
| --- | --- | --- |
| `Governance` | Accountability, policy, oversight, approval, risk appetite, ethics, legal defensibility, and board reporting. | Missing owner, weak evidence, no approval route, unclear escalation, poor traceability. |
| `Operational` | Continuity, process performance, customer outcomes, model performance, resilience, and business execution. | Drift, outages, vendor failure, inconsistent workflow, manual fallback weakness. |
| `Cyber` | Confidentiality, integrity, availability, identity, access, logging, incident response, and adversarial AI exposure. | Prompt injection, over-broad tool access, leaked `PII`, weak logging, API misuse. |

## Taxonomy Categories

Use these categories consistently across Deliverable A and Deliverable B.

| Category | Definition | Best-Fit Risks |
| --- | --- | --- |
| `Accountability` | Ownership, decision rights, board oversight, and responsible escalation are unclear or incomplete. | `R-02`, `R-09`, `R-12` |
| `Access Control` | AI workflows, users, services, or tools have excessive or poorly governed access. | `R-05`, `R-08` |
| `Alignment` | AI behavior may diverge from business intent, policy, or safe operating boundaries. | `R-04` |
| `Autonomy` | AI can influence or chain decisions beyond intended human oversight or authority. | `R-07` |
| `Compliance` | The system may fail legal, regulatory, or governance requirements. | `R-02` |
| `Data` | Data quality, lineage, retention, provenance, or environment handling is incomplete or unsafe. | `R-01`, `R-03`, `R-06` |
| `Decision Risk` | AI output can materially affect credit, fraud, customer, or underwriting outcomes. | `R-02`, `R-07`, `R-09` |
| `Dependency` | The entity relies on vendors, tools, cloud services, data providers, or inherited systems that it cannot fully control. | `R-05`, `R-08`, `R-10`, `R-11` |
| `Explainability` | The system cannot provide an audit-ready reason, trace, or explanation for relevant outputs. | `R-02`, `R-09`, `R-11` |
| `Model Risk` | Model performance, validation, drift, robustness, or monitoring is insufficient. | `R-03`, `R-11` |
| `Operating Model` | Policies, forums, evidence standards, or roles do not work coherently across the combined entity. | `R-12` |
| `Privacy` | Personal data may be processed, transferred, retained, or exposed beyond lawful and controlled bounds. | `R-01`, `R-06` |
| `Security` | AI systems, prompts, APIs, logs, environments, or tools may be exploited or misused. | `R-01`, `R-04`, `R-05`, `R-06`, `R-08` |
| `Third-Party Risk` | Supplier contracts, assurance, resilience, transparency, or continuity are insufficient. | `R-10`, `R-11` |

## Substrate Properties

These are the AI-specific properties from the project checklist. Use them to explain why AI changes the M&A risk profile.

| Property | Definition | Example In Scenario |
| --- | --- | --- |
| `Opacity` | The system's reasoning, model internals, or decision path is hard to inspect or explain. | Credit decision explanations and agent traceability. |
| `Autonomy` | The system can perform multi-step reasoning, recommendations, or tool actions without direct human selection of every step. | AutoUnderwriter tool chaining and recommendation workflow. |
| `Dependency` | The system depends on external models, APIs, tools, suppliers, or data sources. | FraudShield vendor model and MCP tools. |
| `Drift` | Model performance, data distributions, behavior, or outcomes change over time. | LumaCredit-EU approval-rate or bad-debt changes. |
| `Scale Asymmetry` | A small model, prompt, data, or permission failure can affect many customers or workflows quickly. | Unredacted `PII` copied into `test`; broad assistant access to CRM data. |

## Lifecycle Stages

Use one primary lifecycle stage per risk where possible. Use multiple stages only when the risk clearly spans both control design and operation.

| Stage | Definition | Evidence Examples |
| --- | --- | --- |
| `Design` | Purpose, classification, oversight, architecture, risk appetite, and control requirements are defined. | HLDs, classification memo, governance charter, risk assessment. |
| `Data` | Data sources, lineage, quality, privacy, retention, transfer, and environment use are governed. | Data lineage, masking standard, DPIA, transfer map. |
| `Develop` | Prompts, models, integrations, tools, and software are built, tested, versioned, and approved. | Repositories, test results, prompt approvals, secure development evidence. |
| `Deploy` | The system is released, permissioned, integrated, and operated in production or lower environments. | Deployment approvals, IAM roles, MCP permission matrix, change records. |
| `Monitor` | The system is measured, reviewed, logged, challenged, and escalated during operation. | KRIs, dashboards, drift alerts, audit logs, incident records. |

## Evidence Quality Rules

- Every board-level risk must include a risk ID, enterprise lens, taxonomy category, substrate property, lifecycle stage, owner, KRI, treatment, and framework mapping.
- Every due-diligence question must state the evidence artefact requested and link back to at least one risk ID or scenario theme.
- Every roadmap initiative must link to one or more risks and at least one `NIST AI RMF` or `NIST CSF` function.
- Every recommendation in Deliverable A should be traceable to a more detailed row in Deliverable B.
- Clause references should be specific where available. Where a source is used at function level only, label it as a function or theme rather than a clause.
- Separate inherited-state exposure, interim treatment, and target-state uplift in all board-facing materials.
