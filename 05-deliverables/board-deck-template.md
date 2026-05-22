# Board Deck Template

## Purpose
This template is designed to be copied into PowerPoint, Google Slides, Teams, or a Word-based board pack. It follows the assignment structure and keeps the language concise enough for a `Group Risk Committee` audience.

## Cover Slide
**Title**
`Nordhaven–LumaPay AI Risk Review`

**Subtitle**
Board-level pack for acquisition-related AI governance, operational, and cyber risk

**Footer**
- Prepared by: `Nordhaven–LumaPay AI Risk Taskforce`
- Date:
- Audience: `Group Risk Committee / Board`

## Slide 1: Executive Summary
**Slide Objective**
Summarize the `5–7` most important AI risks and the Board decisions required.

**Suggested Layout**
- Left: transaction summary
- Right: top risk bullets

**Content Placeholder**
- Nordhaven is acquiring `80%` of LumaPay, a `UK-regulated` fintech using four material AI systems.
- The transaction creates a `12–18 month` interim control gap across governance, operations, and cyber.
- Highest current concerns include:
- copied live `PII` in `test`
- high-risk AI governance gaps in `LumaCredit-EU`
- over-broad `MCP` permissions in LLM and agent workflows
- third-party continuity and opacity risk in `FraudShield`
- Board decisions requested include:
- approve interim AI governance model
- approve `100-day` remediation priorities
- approve interim AI risk-appetite statements

## Slide 2: Deal Context And Why AI Changes The Risk Profile
**Slide Objective**
Explain why this acquisition is an AI-risk stress test rather than a standard technology integration.

**Content Placeholder**
- AI assets are central to LumaPay’s value and risk profile.
- Documentation, lineage, and governance maturity are incomplete.
- Parallel operations create duplicated attack surface and accountability gaps.
- Cross-border data flows and high-risk credit use cases elevate regulatory exposure.

**Reference Tags**
- `NIST AI RMF`
- `ISO/IEC 42001`
- `GDPR`
- `EU AI Act`

## Slide 3: LumaPay At A Glance
**Slide Objective**
Ground the audience in the fictional company and inherited maturity gap.

**Content Placeholder**
- `200` employees
- `100` developers
- `5` platform engineers
- no dedicated security team
- no `CSPM`, `DSPM`, or modern AI security tooling
- two AWS accounts: `test` and `production`
- copied live `PII` into `test`

**Compare To Nordhaven**
- `10,000` employees
- dedicated security and `GRC`
- established risk process
- existing `CSPM`, `DSPM`, and modern AI security tooling

## Slide 4: AI Systems In Scope
**Slide Objective**
Show the four systems and their distinct risk profiles.

**Suggested Layout**
- `2 x 2` grid

**Systems**
- `LumaCredit-EU`: high-risk credit decisioning
- `LumaAssist Chat`: customer-facing LLM with MCP access
- `AutoUnderwriter Agent`: agentic internal underwriting workflow
- `FraudShield`: third-party fraud model and supplier dependency

**Visual Option**
Insert the PNG diagrams from:
- [lumaassist-chat-architecture.png](/Users/dquigley/Documents/Codex/projects/capstone/06-collaboration/teams-share-pack/lumaassist-chat-architecture.png)
- [autounderwriter-agent-architecture.png](/Users/dquigley/Documents/Codex/projects/capstone/06-collaboration/teams-share-pack/autounderwriter-agent-architecture.png)
- [lumacredit-eu-architecture.png](/Users/dquigley/Documents/Codex/projects/capstone/06-collaboration/teams-share-pack/lumacredit-eu-architecture.png)
- [fraudshield-architecture.png](/Users/dquigley/Documents/Codex/projects/capstone/06-collaboration/teams-share-pack/fraudshield-architecture.png)

## Slide 5: Top 5-7 AI Risks
**Slide Objective**
Present the highest-priority risks with precise statements.

**Suggested Columns**
- Risk
- AI system
- lifecycle stage
- primary framework tag

**Candidate Risks**
- `R-01` Unredacted `PII` in `test`
- `R-02` High-risk AI governance gap in credit decisioning
- `R-04` Prompt injection against customer assistant
- `R-08` MCP tool permission overreach in underwriting
- `R-10` Fraud vendor change-of-control disruption
- `R-12` Governance misalignment during parallel operations

## Slide 6: Pre-Close Due-Diligence View
**Slide Objective**
Show what evidence Nordhaven needs before close.

**Suggested Layout**
- left: critical diligence themes
- right: artefacts to request

**Critical Themes**
- data and `PII` handling
- high-risk model governance
- MCP inventory and permissions
- prompt and trace logging
- vendor contracts and assignment rights

**Key Artefacts**
- masking standards and dataset inventories
- model documentation
- validation reports
- contract clauses
- transfer-impact and privacy assessments

## Slide 7: Governance, Operational, And Cyber Stress Test
**Slide Objective**
Show that failures in one lens cascade into the others.

**Suggested Layout**
- three columns:
- governance
- operational
- cyber

**Content Placeholder**
- Governance: fragmented ownership, weak documentation, no unified AI registry
- Operational: drift, orphaned models, inconsistent monitoring, vendor fallback gaps
- Cyber: prompt injection, MCP overreach, copied `PII`, broad access in interim environments

## Slide 8: AI Risk Appetite And Tolerance Statements
**Slide Objective**
Give the Board a defensible position on the five substrate properties.

**Suggested Layout**
- five-row table with:
- property
- appetite
- tolerance
- KRI

**Properties**
- `Opacity`
- `Autonomy`
- `Dependency`
- `Drift`
- `Scale Asymmetry`

**Source File**
- [ai-risk-appetite-and-tolerance-statements.md](/Users/dquigley/Documents/Codex/projects/capstone/04-risk-and-controls/ai-risk-appetite-and-tolerance-statements.md)

## Slide 9: 100-Day AI Integration Plan
**Slide Objective**
Show how Nordhaven reduces inherited risk quickly and practically.

**Suggested Layout**
- timeline by phase:
- day `0–30`
- day `31–60`
- day `61–100`

**Must Highlight**
- `PII` containment in `test`
- `LumaCredit-EU` high-risk governance uplift
- `MCP` permission reduction
- `FraudShield` contract and fallback review
- inherited-state versus target-state reporting

**Source File**
- [100-day-ai-integration-roadmap.md](/Users/dquigley/Documents/Codex/projects/capstone/04-risk-and-controls/100-day-ai-integration-roadmap.md)

## Slide 10: Board Decisions And Escalation Asks
**Slide Objective**
End with concrete decisions rather than a passive summary.

**Suggested Decisions**
- Approve interim AI governance forum and decision rights
- Approve funding and executive backing for urgent `PII` remediation
- Endorse the interim AI risk-appetite statements
- Require monthly inherited-state AI risk reporting until material gaps are closed
- Approve vendor continuity review for critical third-party AI dependencies

## Optional Appendix Slides
- Detailed risk register extract
- Due-diligence checklist by domain
- NIST `Govern / Map / Measure / Manage`
- one-page HLD per AI system
- standards and clause cross-reference

## Speaker Notes Guidance
- Keep risk statements short and explicit.
- Separate `current inherited exposure` from `target-state ambition`.
- Use standards as anchors, not as the entire story.
- When possible, connect each risk to:
- customer harm
- regulatory exposure
- operational disruption
- Board accountability
