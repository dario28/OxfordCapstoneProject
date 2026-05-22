# 100-Day AI Integration Roadmap

## Purpose
This roadmap is the `B3` technical appendix component for the Nordhaven-LumaPay capstone. It translates the inherited AI risks into a practical `100-day` integration plan that can be defended to the Board, the Group Risk Committee, and regulators.

## Planning Assumptions
- Nordhaven acquires `80%` of LumaPay and inherits four in-scope AI systems.
- The combined entity will operate in an interim state for `12–18 months`.
- LumaPay currently has no dedicated security team, no formal `CSPM` or `DSPM`, immature AI lifecycle governance, and copied live `PII` into `test`.
- Nordhaven has a stronger control baseline and must reduce inherited AI risk before full platform harmonisation is complete.

## Roadmap Design Principles
- Prioritize inherited-state risk reduction before target-state optimization.
- Treat lower-environment `PII`, high-risk decision systems, and agent tool overreach as day-1 issues.
- Use interim controls where full platform migration is not yet possible.
- Map each initiative to `NIST AI RMF` and `NIST CSF` so the roadmap supports both Deliverable A and Deliverable B.

## Maturity Scale
| Maturity Level | Meaning In This Scenario |
| --- | --- |
| Initial | Control is ad hoc, undocumented, or dependent on individuals. |
| Repeatable | Control exists in limited form but is inconsistent across systems or environments. |
| Defined | Control is documented, assigned, and consistently applied to in-scope systems. |
| Managed | Control is measured through KRIs, dashboards, or review forums. |
| Optimised | Control is continuously improved, tested, and integrated into the wider Nordhaven operating model. |

## Roadmap Summary

| Phase | Primary Objective | Maturity Shift | Board Message |
| --- | --- | --- | --- |
| Day `0–30` | Stabilize inherited risk and stop obvious exposure | Initial -> Repeatable | Nordhaven has identified the highest inherited AI control failures and applied emergency guardrails. |
| Day `31–60` | Formalize governance, evidence, and monitoring | Repeatable -> Defined / Managed | The combined entity has a working interim AI control model with named owners and measurable indicators. |
| Day `61–100` | Strengthen resilience and prepare for regulator-grade oversight | Defined / Managed -> Optimised for highest-priority controls | The most material AI risks now have sustainable controls, escalation paths, and Board reporting. |

## Detailed Roadmap

| Initiative ID | Initiative | Primary Risks Addressed | AI Systems | Phase | Owner | Dependencies | NIST AI RMF / NIST CSF Mapping | Maturity Shift | Success Measure |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `I-01` | Freeze further copying of live `PII` into `test` and start purge / masking actions for known lower-environment datasets | `R-01`, `R-06` | LumaCredit-EU, LumaAssist Chat, AutoUnderwriter Agent | Day `0–30` | Head of Platform | Executive mandate, environment inventory | `Manage`; `Protect` | Initial -> Repeatable | No new live `PII` copies created after day `7`; purge or masking plan approved for all known datasets |
| `I-02` | Produce an emergency inventory of all four AI systems, their environments, MCP servers, core datasets, and third-party dependencies | `R-02`, `R-05`, `R-08`, `R-10`, `R-12` | All | Day `0–30` | Integration Lead | Access to app owners and architecture notes | `Map`; `Identify` | Initial -> Repeatable | Combined inventory completed for `100%` of in-scope systems and dependencies |
| `I-03` | Stand up an interim AI governance forum with weekly review of inherited risks, exceptions, and deployment decisions | `R-02`, `R-07`, `R-12` | All | Day `0–30` | Group Risk Committee Delegate / Integration Lead | Named attendees, initial terms of reference | `Govern`; `Identify` | Initial -> Repeatable | Weekly governance cadence established with decision log and action tracker |
| `I-04` | Apply immediate least-privilege restrictions to `MCP` tools used by `LumaAssist Chat` and `AutoUnderwriter Agent` | `R-05`, `R-08` | LumaAssist Chat, AutoUnderwriter Agent | Day `0–30` | AI Workflow Engineering Lead | MCP inventory, tool permission matrix | `Manage`; `Protect` | Initial -> Repeatable | Reduction in callable high-risk tools; all sensitive tool calls require explicit approval or scoped read-only access |
| `I-05` | Create a Board and Group Risk Committee inherited-risk reporting pack separating current-state exposure from target-state design | `R-12` | All | Day `0–30` | Group Risk Committee / Integration Lead | Interim governance forum | `Govern`; `Measure` | Initial -> Repeatable | First inherited-state report delivered with top `5–7` AI risks and decisions required |
| `I-06` | Classify `LumaCredit-EU` formally as a high-risk credit-decision system and assign accountable executive and technical owners | `R-02`, `R-03` | LumaCredit-EU | Day `31–60` | Chief Credit Officer | AI asset inventory, legal input | `Govern`; `Map` | Repeatable -> Defined | Ownership, classification, and mandatory documentation requirements approved |
| `I-07` | Build the minimum compliance and evidence pack for `LumaCredit-EU` covering model purpose, validation, oversight, logging, and review history | `R-02`, `R-03` | LumaCredit-EU | Day `31–60` | Head of Lending | `I-06`, validation artefacts | `Measure`; `Detect` | Repeatable -> Defined / Managed | Core high-risk AI evidence bundle completed and reviewable |
| `I-08` | Implement trace redaction, retention limits, and access controls for prompts, responses, and LangSmith traces | `R-06`, `R-09` | LumaAssist Chat, AutoUnderwriter Agent | Day `31–60` | Head of Platform | Logging architecture, privacy review | `Manage`; `Protect` / `Detect` | Repeatable -> Defined | Trace retention standard approved; sampled traces show materially reduced `PII` presence |
| `I-09` | Establish minimum drift, quality, and performance monitoring thresholds for `LumaCredit-EU` and `FraudShield` integrations | `R-03`, `R-11` | LumaCredit-EU, FraudShield | Day `31–60` | Credit Platform Engineering Manager / Head of Fraud | Dashboard setup, baseline metrics | `Measure`; `Detect` | Repeatable -> Managed | Thresholds approved; alerts routed to named owners; monthly review starts |
| `I-10` | Introduce documented no-auto-decision boundaries and approval gates for `AutoUnderwriter Agent` recommendations | `R-07`, `R-09` | AutoUnderwriter Agent | Day `31–60` | Chief Credit Officer | Underwriting workflow review, agent inventory | `Govern`; `Protect` | Repeatable -> Defined | Human approval checkpoints documented and enforced for all in-scope underwriting actions |
| `I-11` | Complete pre-close review of `FraudShield` and other critical AI vendor contracts for assignment, change-of-control, and fallback obligations | `R-10`, `R-11` | FraudShield | Day `31–60` | Head of Fraud / Legal | Vendor contracts, supplier list | `Map`; `Recover` | Repeatable -> Defined | Critical vendor legal review completed with remediation actions and fallback assumptions recorded |
| `I-12` | Run focused red-team and abuse-case testing for prompt injection, unsafe tool use, and sensitive-data leakage | `R-04`, `R-05`, `R-08` | LumaAssist Chat, AutoUnderwriter Agent | Day `61–100` | Conversational AI Product Lead / AI Workflow Engineering Lead | Guardrails in place, test scenarios | `Measure`; `Protect` / `Detect` | Defined -> Managed | Test cycle completed with tracked findings and closure dates |
| `I-13` | Create AI-specific incident playbooks for prompt abuse, model drift, vendor outage, and unauthorized lower-environment data exposure | `R-03`, `R-04`, `R-10`, `R-12` | All | Day `61–100` | Nordhaven Security Incident Lead | Governance forum, monitoring setup | `Manage`; `Respond` / `Recover` | Defined -> Managed | Playbooks approved, contacts assigned, and at least one tabletop completed |
| `I-14` | Publish interim AI risk-appetite and tolerance statements for opacity, autonomy, dependency, drift, and scale asymmetry | `R-02`, `R-07`, `R-11`, `R-12` | All | Day `61–100` | Group Risk Committee | Governance forum outputs, KRIs | `Govern`; `Identify` | Defined -> Managed | Appetite statements approved with linked KRIs and escalation thresholds |
| `I-15` | Formalize the unified AI registry, stage-gate process, and change approval model for prompts, models, MCP tools, and third-party AI services | `R-02`, `R-05`, `R-08`, `R-12` | All | Day `61–100` | Integration Lead / Head of Platform | Inventory, governance charter | `Govern`; `Protect` | Defined -> Managed / Optimised | Unified registry becomes the required source of truth for changes and exceptions |
| `I-16` | Define target-state migration priorities for control uplift, including Nordhaven security tooling adoption and environment separation improvements | `R-01`, `R-06`, `R-12` | All | Day `61–100` | CISO Delegate / Head of Platform | Roadmap outputs, budget decision | `Manage`; `Identify` / `Protect` | Managed -> Optimised for priority controls | Post-100-day target-state backlog approved with owners, budget asks, and sequencing |

## Phase View

### Day 0-30: Stabilize The Inherited Estate
- Stop known bad practices from spreading:
- copied live `PII` into `test`
- over-broad `MCP` permissions
- undocumented deployment or prompt changes
- Build enough visibility for Nordhaven to govern what it has inherited:
- AI asset inventory
- dependency inventory
- named owners
- inherited-state reporting

### Day 31-60: Establish The Interim Operating Model
- Convert emergency containment into documented controls.
- Raise the maturity of the highest-risk systems first:
- `LumaCredit-EU`
- `LumaAssist Chat`
- `AutoUnderwriter Agent`
- Complete the minimum viable evidence pack for high-risk and customer-impacting systems.

### Day 61-100: Prove Control And Prepare For Scrutiny
- Validate controls through testing, playbooks, and KRIs.
- Put interim appetite, escalation, and Board reporting on a sustainable footing.
- Define what stays interim and what moves into Nordhaven’s target-state operating model next.

## Critical Dependencies

| Dependency | Why It Matters | Blocked Initiatives |
| --- | --- | --- |
| Access to complete environment and data inventories | Required to identify copied `PII`, MCP scope, and vendor reliance | `I-01`, `I-02`, `I-08` |
| Named executive ownership across credit, fraud, platform, and customer operations | Needed to turn inherited issues into accountable remediation | `I-03`, `I-06`, `I-10`, `I-14` |
| Legal review of contracts, DPAs, and transfer arrangements | Required for third-party and cross-border diligence | `I-11`, `I-16` |
| Logging and observability baseline across AWS, Datadog, and LangSmith | Needed for measurable monitoring and defensible incident response | `I-08`, `I-09`, `I-12`, `I-13` |
| Governance decision on interim versus target-state standards | Prevents ambiguity during the `12–18 month` dual-operating phase | `I-05`, `I-14`, `I-15`, `I-16` |

## Appendix-Ready KPI / KRI Candidates
- Number of lower-environment datasets containing live `PII`
- Percentage of in-scope AI systems entered in the unified AI registry
- Percentage of critical MCP tools reviewed and permission-scoped
- Percentage of `LumaCredit-EU` required evidence artefacts completed
- Number of unresolved drift-threshold breaches
- Percentage of sampled traces containing unmasked personal data
- Percentage of critical AI vendors with confirmed assignment or fallback position
- Number of AI incidents or abuse cases without approved playbooks

## Board Decisions Supported By This Roadmap
- Confirm whether copied live `PII` in `test` is treated as a red-line integration issue requiring immediate remediation funding.
- Approve the interim AI governance forum and decision-rights model.
- Endorse the high-risk treatment priority for `LumaCredit-EU`, `LumaAssist Chat`, and `AutoUnderwriter Agent`.
- Require inherited-state reporting to remain separate from target-state reporting until key control gaps are materially closed.
