# Capstone Project Checklist

## 1. Assignment Setup
- [X] Confirm group ownership across architecture, governance, cyber, lifecycle risk, and board-pack workstreams.
- [ ] Confirm the final submission format for Deliverable A and Deliverable B.
- [ ] Confirm whether the one-page HLDs are an internal working asset or part of the submitted appendix.
- [ ] Confirm any deck design or file-format expectations for Teams or OneDrive sharing.
- [ ] Align terminology to the course glossary and taxonomy before drafting.

## 2. Scenario And Deal Baseline
- [ ] Document the acquisition baseline: `Nordhaven` acquires `80%` of `LumaPay`.
- [ ] Capture the `12–18 month` parallel operations window.
- [ ] Document the `EU`, `UK`, and `US-hosted cloud` cross-border data-flow context.
- [ ] Capture mixed infrastructure, mixed suppliers, and transitional accountability gaps.
- [ ] Define the combined-entity operating assumptions needed for the roadmap.

## 3. LumaPay Company Profile
- [ ] Finalize the LumaPay profile as a `UK-regulated fintech`.
- [ ] Document the products: embedded `BNPL` and `SME lending`.
- [ ] Flesh out the fictional operating model for a `200-person` startup.
- [ ] Define legal entities, leadership, control functions, and board oversight model.
- [ ] Document the governance immaturity issues called out in the scenario.
- [ ] Capture the AWS baseline with `test` and `production` accounts.
- [ ] Document the key vendors, AI providers, data suppliers, and third-party APIs.

## 4. AI System Inventory
- [ ] Create a master inventory for the four in-scope systems.
- [ ] `LumaCredit-EU`: define high-risk credit-decision use case and lifecycle controls.
- [ ] `LumaAssist Chat`: define LLM assistant workflow, exposure points, and guardrails.
- [ ] `AutoUnderwriter Agent`: define agentic orchestration, tools, and approval points.
- [ ] `FraudShield`: define third-party model dependency and supply-chain controls.
- [ ] Tag each system by substrate properties:
- [ ] opacity
- [ ] autonomy
- [ ] dependency
- [ ] drift
- [ ] scale asymmetry

## 5. One-Page HLDs
- [ ] Produce a one-page HLD for `LumaCredit-EU`.
- [ ] Produce a one-page HLD for `LumaAssist Chat`.
- [ ] Produce a one-page HLD for `AutoUnderwriter Agent`.
- [ ] Produce a one-page HLD for `FraudShield`.
- [ ] Ensure each HLD includes:
- [ ] business purpose and decision criticality
- [ ] users, owners, and human oversight
- [ ] design, data, develop, deploy, and monitor touchpoints
- [ ] `test` versus `production` AWS hosting assumptions
- [ ] key integrations, APIs, and vendors
- [ ] governance, operational, and cyber controls
- [ ] top risks and due-diligence evidence requests

## 6. Risk Taxonomy And Lens Mapping
- [ ] Create a shared taxonomy covering categories such as alignment, autonomy, data, dependency, security, and explainability.
- [ ] Tag each risk to one or more enterprise lenses:
- [ ] governance lens
- [ ] operational lens
- [ ] cyber lens
- [ ] Tag each risk to one lifecycle stage:
- [ ] design
- [ ] data
- [ ] develop
- [ ] deploy
- [ ] monitor

## 7. Standards And Clause Mapping
- [ ] Create the standards inventory for the assignment.
- [ ] Map `NIST AI RMF` to `Govern`, `Map`, `Measure`, `Manage`.
- [ ] Map `NIST CSF` functions to cyber controls and monitoring enhancements.
- [ ] Map relevant `EU AI Act` obligations, including high-risk credit-decision concerns.
- [ ] Map `GDPR`, `UK GDPR`, and `UK DPA 2018` to data-flow and privacy risks.
- [ ] Map `ISO/IEC 42001`, `27001`, `23894`, `5259`, `27036`, and `DORA`.
- [ ] Add at least a starter set of clause or article references for each major recommendation.

## 8. Deliverable B1: Risk Register Extract
- [ ] Draft `10–12` realistic AI risks.
- [ ] Include M&A-specific themes such as:
- [ ] shadow AI and undocumented tools
- [ ] change-of-control and non-assignable licences
- [ ] talent flight and orphaned models
- [ ] governance misalignment
- [ ] IP and data provenance
- [ ] expanded cyber attack surface
- [ ] For each risk include:
- [ ] taxonomy category
- [ ] lifecycle stage
- [ ] standards mapping
- [ ] likelihood and impact
- [ ] designated owner
- [ ] at least one measurable `KRI`

## 9. Deliverable B2: AI Due-Diligence Checklist
- [ ] Organize the checklist across the five required domains:
- [ ] data and IP
- [ ] model risk
- [ ] cyber
- [ ] regulation and ethics
- [ ] vendor and supply chain
- [ ] For each checklist item include:
- [ ] artefact to request
- [ ] risk addressed
- [ ] standard or regulatory mapping
- [ ] clause or article reference where possible
- [ ] Flag which items are `pre-close critical`.
- [ ] Flag which items can be handled in the `100-day` post-close plan.

## 10. Deliverable A: Executive Summary And Board Pack
- [ ] Draft the `8–12` slide board-level pack.
- [ ] Write the executive summary for the top `5–7` risks.
- [ ] Make every risk statement precise and non-generic.
- [ ] Tag each top risk with lifecycle stage and primary framework reference.
- [ ] Build the due-diligence view for `pre-close` AI risks and evidence requests.
- [ ] Keep the writing decision-oriented for a senior risk audience with limited technical patience.

## 11. 100-Day Plan
- [ ] Build the phased roadmap from day `0–30`, `31–60`, and `61–100`.
- [ ] Define unified AI registry ownership.
- [ ] Define stage-gate review milestones.
- [ ] Define deployment approval rights and escalation paths.
- [ ] Map each initiative to `NIST AI RMF` or `NIST CSF` functions.
- [ ] Include dependencies, milestones, and maturity progression from initial to optimised.

## 12. Cyber And Monitoring Enhancements
- [ ] Prioritize enhancements for `LumaAssist Chat`.
- [ ] Prioritize enhancements for `AutoUnderwriter Agent`.
- [ ] Include `OWASP LLM Top 10` controls for LLM exposure.
- [ ] Include `MITRE ATLAS` mitigations for adversarial ML threats.
- [ ] Include `NIST CSF` measures for protection, detection, response, and recovery.
- [ ] Address monitoring gaps, model drift, API exposure, and access-control seams.

## 13. Risk Appetite And Tolerance Statements
- [ ] Draft quantifiable appetite and tolerance statements for:
- [ ] opacity
- [ ] autonomy
- [ ] dependency
- [ ] drift
- [ ] scale asymmetry
- [ ] Make them defensible to regulators and aligned to Nordhaven’s ERM model.

## 14. Final Quality Review
- [ ] Check that every recommendation is traceable to a framework or standard.
- [ ] Check that all deliverables use the same taxonomy and glossary.
- [ ] Check that each HLD, risk, and roadmap item fits the scenario facts.
- [ ] Check that the work protects enterprise value, not just compliance posture.
- [ ] Prepare the final share pack for Teams or OneDrive.
