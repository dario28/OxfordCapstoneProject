# AI Risk Appetite And Tolerance Statements

## Purpose
This note provides interim AI risk-appetite and tolerance statements for the Nordhaven-LumaPay combined entity. It is designed to support:
- Deliverable A slide `8`
- the `Govern` section of the appendix
- Board discussion of what risk may be accepted during the `12–18 month` integration period

## Scenario Context
- Nordhaven is inheriting four in-scope AI systems with uneven control maturity.
- LumaPay currently operates with weak AI governance, no dedicated security team, and copied live `PII` in `test`.
- These statements are therefore framed for an interim state, not an ideal target state.

## How To Read These Statements
- `Risk Appetite` describes the level of risk the Board is willing to accept during the transition.
- `Tolerance` describes the measurable boundary that triggers escalation, exception handling, or remediation.
- These thresholds should be used alongside the AI risk register, KRIs, and the `100-day` roadmap.

## Board-Level Position
Nordhaven has low appetite for unmanaged AI risk that can create customer harm, regulatory exposure, or uncontrolled third-party dependence. During the integration period, the Board may accept limited residual risk only where:
- the risk is visible and owned
- interim controls are operating
- a defined remediation path exists
- inherited-state reporting remains separate from target-state aspirations

## Risk-Appetite Statements By Substrate Property

| Property | Appetite Statement | Tolerance Statement | Example KRI | Escalation Trigger |
| --- | --- | --- | --- | --- |
| `Opacity` | Nordhaven has low appetite for opaque AI decisioning in any system that affects credit outcomes, fraud intervention, or customer treatment. | No high-impact AI system should operate without a named owner, documented purpose, model or workflow description, logging approach, and review evidence for more than `60` days post-close. | Percentage of mandatory artefacts completed for `LumaCredit-EU` and `AutoUnderwriter Agent` | High-impact system remains in service with missing core documentation or incomplete explanation evidence beyond approved tolerance |
| `Autonomy` | Nordhaven has very low appetite for autonomous AI behavior in underwriting, customer remediation, or any high-impact workflow without enforceable human oversight. | `0` production use cases are permitted to execute high-impact credit or account actions without documented human approval checkpoints. | Percentage of agent-assisted decisions completed without material human review | Any auto-decision path is discovered in underwriting or customer-sensitive operations |
| `Dependency` | Nordhaven has moderate but actively managed appetite for reliance on third-party AI, MCP tools, and cloud services where the dependency is commercially necessary, visible, owned, contractually controlled, and supported by fallback or continuity planning. | `100%` of critical AI vendors, MCP-connected tools, and high-risk dependencies must have a named owner, inventory entry, and fallback or continuity assumption within `60` days. | Percentage of critical dependencies recorded in the unified AI registry | Critical tool or vendor remains unregistered, unowned, or without fallback posture after the interim governance model is live |
| `Drift` | Nordhaven has low appetite for unmonitored drift in credit, fraud, or customer-facing AI systems. | `100%` of in-scope production models and high-impact workflows must have defined monitoring thresholds and review owners within `60` days; no unresolved critical drift breach should remain open beyond agreed SLA. | Number of unresolved drift-threshold breaches | Critical performance or data-quality drift persists without owner action or escalation |
| `Scale Asymmetry` | Nordhaven has very low appetite for inherited AI exposure that scales faster than oversight capacity, especially where LumaPay’s engineering footprint exceeds its control capacity. | No material expansion in AI functionality, environment footprint, or MCP tool access should occur until the affected system is recorded in the registry, assigned an owner, and covered by interim governance. | Number of new AI services or major changes introduced without interim approval | A major model, prompt, MCP, or environment change is deployed outside the interim stage-gate process |

## Interim Threshold Interpretation

## Appetite Crosswalk To Risk Register

| Substrate Property | Appetite | Breach Trigger | Linked Risk IDs | Primary Anchor |
| --- | --- | --- | --- | --- |
| `Opacity` | Low | Unexplained high-risk or customer-impacting AI decision in production | `R-02`, `R-09`, `R-13`, `R-16`, `R-18` | `EU AI Act` Articles `11-13`; `GDPR` Article `22`; `NIST AI RMF` Measure |
| `Autonomy` | Very low | Autonomous adverse decision, unsanctioned agent action, or ineffective human review | `R-07`, `R-08`, `R-17` | `EU AI Act` Article `14`; `NIST AI RMF` Manage |
| `Dependency` | Moderate, actively managed | Unresolved change-of-control clause, no exit plan, or unowned critical dependency | `R-05`, `R-08`, `R-10`, `R-11`, `R-15` | `DORA`; `ISO/IEC 27036`; `NIST AI RMF` Map |
| `Drift` | Low | Production model operates without monitoring thresholds or unresolved drift breach exceeds SLA | `R-03`, `R-14`, `R-16`, `R-18` | `EU AI Act` Articles `9`, `15`, `72`; `NIST AI RMF` Measure |
| `Scale Asymmetry` | Very low | Full-population deploy, broad MCP expansion, or customer-facing change occurs without staged validation and governance approval | `R-01`, `R-04`, `R-05`, `R-12`, `R-13`, `R-17` | `NIST CSF` Detect / Respond; `OWASP LLM Top 10`; `NIST AI RMF` Manage |

### Red-Line Conditions
The following should be treated as outside appetite and require immediate action:
- copied live `PII` into `test` or other lower environments
- unapproved autonomous high-impact decisions
- critical vendor or MCP dependency with no owner and no fallback position
- production AI change introduced outside the interim stage-gate
- prompt or trace stores containing large volumes of unmasked personal data without mitigation
- customer-affecting AI system operating outside the unified AI registry
- high-impact human review present only nominally, with no reviewer rationale or meaningful override evidence
- decision or recommendation that cannot be reconstructed to model, prompt, rule, and evidence version

### Temporary Exceptions The Board May Accept
The Board may accept short-term inherited gaps where all of the following are true:
- the issue is explicitly documented in the risk register
- an accountable owner is assigned
- there is a dated remediation milestone in the `100-day` plan
- the issue does not create immediate unlawful processing or unbounded customer harm

## Mapping To In-Scope Applications

| AI Application | Most Relevant Appetite Themes | Why |
| --- | --- | --- |
| `LumaCredit-EU` | `Opacity`, `Drift`, `Scale Asymmetry` | High-risk credit decisioning requires evidence, explanation, and stable performance. |
| `LumaAssist Chat` | `Dependency`, `Scale Asymmetry` | Customer-facing LLM behavior and MCP-connected tools can scale errors quickly. |
| `AutoUnderwriter Agent` | `Autonomy`, `Opacity`, `Dependency` | Agentic orchestration creates the sharpest challenge around human oversight and tool misuse. |
| `FraudShield` | `Dependency`, `Drift` | Third-party service continuity and performance assurance matter more than direct model ownership. |

## Appendix / Slide Language

### Concise Board Version
- Low appetite for opaque or unowned AI in regulated decisions
- Very low appetite for autonomous high-impact decisions without human approval
- Low appetite for undocumented third-party and MCP dependency
- Low appetite for unmonitored model drift
- Very low appetite for AI scale that outpaces oversight and governance capacity

### Suggested Board Ask
Approve these interim AI risk-appetite statements for use during the first `100 days`, with monthly reporting on exceptions, KRIs, and residual inherited-state risk.
