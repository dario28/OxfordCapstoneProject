# Monday Task Assignment Table

## Purpose
This table is designed for the Monday team meeting so each person can assign themselves a clear workstream, deliverable, and output. It is based on:
- the capstone slide requirements
- the suggested team structure image
- the `Oxford Capstone - Group 4 Approach` notes from the Onur session

## Working Assumptions
- Team lead / coordinator owns overall narrative, architecture integration, and final packaging.
- Governance and regulatory work should cover `EU AI Act`, `GDPR`, `UK GDPR`, `ISO/IEC 42001`, and clause-linked read-across.
- Cyber work should cover `NIST CSF`, `OWASP LLM Top 10`, `MITRE ATLAS`, `MCP`-related risk, and monitoring enhancements.
- Operational and lifecycle work should cover design, data, develop, deploy, and monitor, with focus on drift, monitoring, orphaned models, and the `100-day` roadmap.
- Technical design work should own the AI system realism, AWS architecture, integrations, and HLD quality.

## Suggested Workstream Allocation

| Workstream | Core Scope | Main Deliverables | Suggested Owner Based On Notes | Monday Assignee | Support / Backup | Status | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Overall Lead / Integration | Own final storyline, working plan, integration across all sections, and submission quality | final narrative, consistency pass, final deck merge, final appendix merge | You / Lead Architect |  |  | Not assigned | This role should also chair the Monday check-in and track dependencies. |
| Governance And Regulatory | Map risks and recommendations to `EU AI Act`, `GDPR`, `UK GDPR`, `ISO/IEC 42001`, `ISO/IEC 27001`, `DORA`; ensure clause-linked references | standards mapping, governance sections, compliance wording, board defensibility | Suggested Team Structure `Person 2` |  |  | Not assigned | Should review `LumaCredit-EU` high-risk AI treatment and cross-border data flow controls. |
| AI Cybersecurity | Cover `NIST CSF`, `OWASP LLM Top 10`, `MITRE ATLAS`, prompt injection, `MCP` security, trace/log exposure, access control, and monitoring uplift | cyber risk content, control recommendations, LumaAssist / AutoUnderwriter cyber slide content | Suggested Team Structure `Person 3`; notes mention `Amrik Randhawa` for AI cyber and monitoring |  |  | Not assigned | Best fit for `LumaAssist Chat` and `AutoUnderwriter Agent` deep dive. |
| Operational And Lifecycle Risk | Cover lifecycle ownership, drift, monitoring, resilience, orphaned models, and transition-state operating risk | lifecycle lens content, operational risk analysis, roadmap dependencies, KRIs | Suggested Team Structure `Person 4` |  |  | Not assigned | Should own design/data/develop/deploy/monitor read-across in the appendix. |
| AI Systems And Technical Design | Own realism of the four AI applications, AWS architecture, data flows, environments, vendors, and diagrams | one-page HLDs, architecture assumptions, AI system inventory, technical appendix support | Suggested Team Structure `Person 5` |  |  | Not assigned | This workstream should support every other owner with system detail. |
| 100-Day Plan And Board Pack | Turn the risks into a decision-quality pack for the Group Risk Committee; shape the roadmap and executive storyline | board deck structure, executive wording, `100-day` plan summary, board asks | Suggested Team Structure `Person 6` |  |  | Not assigned | This role can work closely with the overall lead on slide flow and final tone. |

## Deliverable-Level Assignment Table

| Deliverable Section | What Needs To Be Produced | Key Source Material | Recommended Primary Owner | Monday Assignee | Due / Checkpoint | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| Deliverable A: Executive Summary | Top `5–7` risks with lifecycle stage and main framework tags | board draft, risk register, capstone slides | Overall Lead / Board Pack Owner |  |  | Must stay concise and board-oriented. |
| Deliverable A: Due-Diligence View | Pre-close AI risks and the artefacts Nordhaven needs before close | due-diligence checklist, risk register, Onur notes | `E Michael Leverock` was noted against this area |  |  | Strong place for governance + legal + data collaboration. |
| Deliverable A: 100-Day Plan | Ownership of AI registry, stage-gates, deployment approval, escalation, phased roadmap | roadmap draft, NIST note, risk register | Board Pack Owner with Operational support |  |  | Should be practical rather than aspirational. |
| Deliverable A: AI Cyber And Monitoring Enhancements | Targeted cyber uplift for `LumaAssist Chat` and `AutoUnderwriter Agent` | HLDs, framework matrix, cyber notes | `Amrik Randhawa` was noted against this area |  |  | Should tie clearly to `NIST CSF`, `OWASP`, and `MITRE ATLAS`. |
| Deliverable A: Risk Appetite And Tolerance | Statements for `opacity`, `autonomy`, `dependency`, `drift`, `scale asymmetry` | appetite draft, risk register, NIST Govern | `Akanksha Mohan` was noted against this area |  |  | Needs regulator-defensible rationale and measurable tolerances. |
| Deliverable B1: Risk Register Extract | `10–12` risks with taxonomy, lifecycle stage, standards, owner, impact, KRI | populated risk register | `Akanksha Mohan` was noted against this area |  |  | Should preserve consistent taxonomy wording across the whole project. |
| Deliverable B2: Due-Diligence Checklist | Five-domain checklist with artefact, risk, and standard mapping | populated checklist | `E Michael Leverock` was noted against this area |  |  | Should stay practitioner-level and realistic. |
| Deliverable B3: 100-Day AI Integration Roadmap | Phased plan with dependencies, maturity, and `NIST AI RMF` / `NIST CSF` mapping | roadmap draft | Operational / Board Pack shared ownership |  |  | Good candidate for one owner plus one reviewer. |

## AI Application Ownership Table

| AI Application | Primary Focus Areas | Recommended Owner Type | Monday Assignee | Reviewer | Notes |
| --- | --- | --- | --- | --- | --- |
| `LumaCredit-EU` | high-risk AI governance, drift, explainability, data quality, credit-decision controls | Governance / Operational |  |  | Most regulator-sensitive application in the scenario. |
| `LumaAssist Chat` | prompt injection, data leakage, trace retention, customer harm, `MCP` access | Cyber / Technical Design |  |  | Good fit for the cyber owner plus technical design support. |
| `AutoUnderwriter Agent` | autonomy, human oversight, traceability, unsafe tool use, `MCP` permission scope | Cyber / Operational / Technical Design |  |  | Good place for joint ownership if the team wants one lead and one support. |
| `FraudShield` | supplier risk, change-of-control, continuity, opacity, fallback mode | Governance / Operational |  |  | Good fit for vendor-risk and resilience themes. |

## Monday Meeting Agenda Prompts
- Confirm whether the team wants one owner per section or one owner plus one reviewer.
- Confirm whether each AI application should have a named lead as well as a workstream lead.
- Confirm who owns final slide drafting versus content contributions in markdown.
- Confirm whether legal and regulatory mapping stays centralized under one person or is split by framework.
- Confirm the first checkpoint date for draft completion before the final integration pass.

## Recommended Minimum Monday Decisions
- Assign one person as overall lead and final integrator.
- Assign one primary owner to each Deliverable A section.
- Assign one primary owner to each Deliverable B section.
- Assign one named lead to each of the four AI applications.
- Set one checkpoint for first drafts and one checkpoint for final integration.
