# Framework Risk And Control Matrix

## Purpose
This document maps realistic risks from the LumaPay scenario to the main frameworks and regulations referenced in the capstone. It is deliberately broader than the final `10–12` risk register so the team can select the strongest board-level risks later.

## How To Read This File
- Each framework section contains `5` risk-and-control mappings.
- `AI Apps` shows which of the four systems are most affected.
- `Interim Parent Risk` makes the Nordhaven post-acquisition exposure explicit.
- `Suggested Controls` are intentionally high-level so they can be traced to the HLDs, due-diligence checklist, and roadmap.

## In-Scope Applications
- `LumaCredit-EU`
- `LumaAssist Chat`
- `AutoUnderwriter Agent`
- `FraudShield`

---

## 1. NIST AI RMF

| ID | AI Apps | Interim Parent Risk | NIST AI RMF Function | Risk | Suggested Controls |
| --- | --- | --- | --- | --- | --- |
| `AIRMF-01` | LumaCredit-EU, AutoUnderwriter Agent | Nordhaven inherits AI systems without a unified accountability model on day one. | `Govern` | AI ownership, approval rights, and escalation paths are fragmented across LumaPay and Nordhaven. | Establish a unified AI registry, define model owners, and formalize board-level decision rights. |
| `AIRMF-02` | All | During parallel operations, the combined entity lacks a single, current inventory of AI assets and MCP-connected tools. | `Map` | Shadow AI, undocumented models, and untracked MCP servers create hidden exposure. | Create a combined AI asset inventory covering models, prompts, datasets, MCP tools, and third-party dependencies. |
| `AIRMF-03` | LumaCredit-EU, LumaAssist Chat, AutoUnderwriter Agent | Nordhaven may not understand the real performance and abuse profile of inherited systems before close. | `Measure` | Drift, prompt abuse, data leakage, and quality failures are insufficiently measured. | Define KRIs, evaluation suites, drift thresholds, and misuse testing for each system. |
| `AIRMF-04` | FraudShield, AutoUnderwriter Agent | Treatment decisions may be inconsistent while the parent and target operate different governance standards. | `Manage` | Known risks remain open because no single body owns prioritization and remediation. | Implement a unified AI risk register and a 100-day remediation governance forum. |
| `AIRMF-05` | All | The parent company may report control confidence that does not match the real state of LumaPay’s estate. | `Govern`, `Measure` | Board reporting can overstate maturity because inherited evidence is incomplete or not comparable. | Use a maturity-based assurance model and explicitly flag inherited evidence gaps in board reporting. |

---

## 2. EU AI Act

| ID | AI Apps | Interim Parent Risk | Article / Theme | Risk | Suggested Controls |
| --- | --- | --- | --- | --- | --- |
| `EUAIA-01` | LumaCredit-EU | Nordhaven acquires a high-risk credit-decision system that may not meet required governance and technical controls. | High-risk AI, Annex III | `LumaCredit-EU` may not satisfy high-risk AI obligations for credit decisioning. | Confirm high-risk classification, perform gap assessment, and define conformity remediation steps. |
| `EUAIA-02` | LumaCredit-EU | The parent may inherit poor documentation that weakens defensibility with regulators. | Risk management and record keeping | Model documentation, logs, and approval evidence may be incomplete. | Build a minimum compliance pack: model docs, validation records, data lineage, and human-oversight evidence. |
| `EUAIA-03` | AutoUnderwriter Agent | Agent-assisted underwriting may expand decision influence without clear governance categorization. | Human oversight, robustness | Human-in-the-loop controls may be nominal rather than effective. | Enforce mandatory approval gates, override tracking, and clear no-auto-decision boundaries. |
| `EUAIA-04` | LumaCredit-EU | Poor-quality inherited data may invalidate compliance assumptions. | Data governance | Training or scoring data may be low quality, weakly governed, or not fit for purpose. | Strengthen lineage, quality checks, retention rules, and lower-environment masking controls. |
| `EUAIA-05` | All, especially LumaCredit-EU | During the interim phase, Nordhaven may be accountable for inherited AI harms before control uplift is complete. | Provider / deployer accountability | Liability attaches faster than integration controls can be implemented. | Define day-1 risk acceptance, immediate restrictions, and board-approved remediation priorities. |

---

## 3. GDPR And UK GDPR

| ID | AI Apps | Interim Parent Risk | Article / Theme | Risk | Suggested Controls |
| --- | --- | --- | --- | --- | --- |
| `GDPR-01` | LumaCredit-EU, LumaAssist Chat, AutoUnderwriter Agent | Nordhaven inherits unlawful lower-environment handling of personal data. | Security of processing | Unredacted customer `PII` has been copied into `test` without masking. | Freeze further copying, identify datasets in `test`, mask or purge where feasible, and raise as a due-diligence red flag. |
| `GDPR-02` | LumaAssist Chat, AutoUnderwriter Agent | Prompt traces and tool logs may move personal data into external or US-hosted services. | International transfers, minimization | Prompts, traces, and MCP logs may contain more personal data than necessary. | Apply prompt minimization, trace scrubbing, retention limits, and transfer-impact review. |
| `GDPR-03` | FraudShield, LumaCredit-EU | Third-party data-sharing arrangements may be poorly evidenced or contractually incomplete. | Controller / processor governance | Vendor and data-provider DPAs may not cover current or post-acquisition processing realities. | Review DPAs, subprocessors, transfer terms, and inherited processor obligations. |
| `GDPR-04` | LumaAssist Chat | Customer-service AI may surface or retain sensitive account context in ways not aligned to purpose. | Purpose limitation, data minimization | The assistant can retrieve or expose data beyond what is necessary for the interaction. | Restrict retrieval scope, define sanctioned use cases, and gate sensitive data responses. |
| `GDPR-05` | LumaCredit-EU, AutoUnderwriter Agent | The parent may struggle to explain or govern automated decision support using inherited models and workflows. | Automated decisions, accountability | Decision logic, rationale, and human oversight are not clearly documented. | Document decision boundaries, create review evidence, and define escalation for challenged outcomes. |

---

## 4. ISO/IEC 42001

| ID | AI Apps | Interim Parent Risk | Clause / Theme | Risk | Suggested Controls |
| --- | --- | --- | --- | --- | --- |
| `ISO42K-01` | All | Nordhaven cannot quickly apply a coherent AI management system to LumaPay’s AI estate. | AI management system governance | AI responsibilities, policies, and oversight are fragmented or informal. | Stand up a combined AI governance structure with named owners and reporting lines. |
| `ISO42K-02` | All | AI asset and lifecycle records may be insufficient to support audit or structured management. | Documentation and accountability | Models, prompts, datasets, MCP tools, and third-party AI assets are not fully inventoried. | Build the unified AI registry and require minimum metadata for every system. |
| `ISO42K-03` | LumaCredit-EU, AutoUnderwriter Agent | Lifecycle controls are inconsistent across design, data, deployment, and monitoring. | Lifecycle control | Critical approvals and validation gates are not reliably applied. | Introduce stage-gates for design approval, deployment, monitoring review, and retirement decisions. |
| `ISO42K-04` | LumaAssist Chat, AutoUnderwriter Agent | Emerging LLM and agent risks are not integrated into the formal governance system. | Risk treatment and monitoring | Prompt abuse, MCP misuse, and trace exposure remain outside standard control processes. | Add AI-specific control requirements for prompts, tools, traces, and evaluations. |
| `ISO42K-05` | All | Nordhaven may inherit undocumented exceptions and shadow tools that are invisible to formal governance. | Assurance and continual improvement | Governance appears stronger on paper than in actual LumaPay operations. | Require exception logging, shadow-AI discovery, and targeted assurance reviews in the first 100 days. |

---

## 5. ISO/IEC 27001

| ID | AI Apps | Interim Parent Risk | Annex A / Theme | Risk | Suggested Controls |
| --- | --- | --- | --- | --- | --- |
| `ISO27K-01` | All | Sensitive data and AI assets are insufficiently segregated between `test` and `production`. | Environment segregation | Lower environments contain live `PII` and weakly controlled AI artefacts. | Enforce environment segregation, data masking, and least-privilege access for non-production. |
| `ISO27K-02` | LumaAssist Chat, AutoUnderwriter Agent | Shared credentials and over-broad service roles may enable misuse of models, logs, or tools. | Access control | IAM roles, secrets, and service identities may exceed business need. | Review roles, rotate secrets, and constrain tool-specific permissions. |
| `ISO27K-03` | FraudShield, LumaCredit-EU | Third-party dependencies may lack adequate information-security oversight. | Supplier security | Inherited contracts and vendor controls may not match Nordhaven’s security baseline. | Review supplier assurance, contracts, security clauses, and incident notification rights. |
| `ISO27K-04` | All | Audit trails may be incomplete across application logic, model usage, and MCP tool invocations. | Logging and monitoring | The combined entity may not be able to reconstruct incidents or explain actions. | Centralize logs, keep model and MCP invocation records, and define retention standards. |
| `ISO27K-05` | LumaAssist Chat, AutoUnderwriter Agent | Secure development practices for prompts, evaluations, and agent tooling are immature. | Secure development | Prompt and agent changes may bypass structured review. | Extend SDLC controls to prompts, agent configurations, evaluations, and MCP schemas. |

---

## 6. NIST CSF

| ID | AI Apps | Interim Parent Risk | Function | Risk | Suggested Controls |
| --- | --- | --- | --- | --- | --- |
| `NCSF-01` | All | Nordhaven lacks a clear inherited view of AI assets, tool chains, and third-party dependencies. | `Identify` | The combined attack surface is larger than management believes. | Complete inherited-asset and dependency identification, including MCP services and logs. |
| `NCSF-02` | LumaAssist Chat, AutoUnderwriter Agent | Protective boundaries around prompts, traces, and MCP tools are too weak. | `Protect` | LLM and agent workflows can access sensitive systems and data too broadly. | Implement prompt guardrails, tool scoping, secret control, and lower-environment restrictions. |
| `NCSF-03` | All | The parent may not detect abuse or silent degradation quickly enough during integration. | `Detect` | Drift, prompt attacks, and environment misuse may go unnoticed. | Create Datadog alerts, trace review workflows, and KRI thresholds for each application. |
| `NCSF-04` | FraudShield, LumaCredit-EU | Incident response ownership may be unclear across parent, target, and vendors. | `Respond` | Security and operational incidents can stall because accountability is split. | Define joint incident playbooks with vendor, platform, and business roles. |
| `NCSF-05` | FraudShield, AutoUnderwriter Agent | Recovery planning may be weak for tool failure, vendor loss, or model degradation. | `Recover` | Business continuity for AI-enabled processes may be underdeveloped. | Define fallback modes, manual alternatives, and restoration priorities for critical AI services. |

---

## 7. OWASP LLM Top 10 And MITRE ATLAS

| ID | AI Apps | Interim Parent Risk | Theme | Risk | Suggested Controls |
| --- | --- | --- | --- | --- | --- |
| `LLM-01` | LumaAssist Chat, AutoUnderwriter Agent | Customer or document inputs can be weaponized before Nordhaven’s controls are in place. | Prompt injection / adversarial input | Malicious inputs can influence model behavior or tool use. | Add input screening, prompt hardening, document sanitization, and test suites for abuse cases. |
| `LLM-02` | LumaAssist Chat, AutoUnderwriter Agent | Trace and memory stores may expose sensitive content from prompts, tools, and outputs. | Sensitive data disclosure | Logs and traces become a secondary leakage channel. | Minimize trace content, redact sensitive fields, and restrict access to evaluation platforms. |
| `LLM-03` | AutoUnderwriter Agent | Agent tool use can exceed intended authority. | Excessive agency | The model can turn reasoning errors into direct system actions through MCP tools. | Implement tool allow-lists, approval checkpoints, action simulation, and fine-grained authorization. |
| `LLM-04` | LumaAssist Chat | Users or attackers may extract hidden instructions or system prompts. | Prompt / system exposure | Guardrails and internal logic may be revealed and reused against the system. | Use prompt compartmentalization, content controls, and active attack pattern monitoring. |
| `LLM-05` | LumaAssist Chat, AutoUnderwriter Agent | Teams may over-trust model output because the systems appear fluent and productive. | Overreliance | Humans may defer too readily to outputs that are incomplete, biased, or wrong. | Train reviewers, monitor override patterns, and define mandatory manual review for sensitive cases. |

---

## 8. DORA And ISO/IEC 27036

| ID | AI Apps | Interim Parent Risk | Theme | Risk | Suggested Controls |
| --- | --- | --- | --- | --- | --- |
| `TPRM-01` | FraudShield | Nordhaven may lose or weaken access to a critical fraud-control dependency during the transaction. | Change-of-control, third-party risk | Contractual terms may be triggered by the acquisition. | Review change-of-control clauses, assignment rights, and exit/fallback options before close. |
| `TPRM-02` | FraudShield, LumaCredit-EU | Critical services rely on external data or model providers with uneven assurance. | Supplier assurance | Service continuity and security posture may be poorly evidenced. | Obtain security reports, SLAs, incident history, and resilience commitments from suppliers. |
| `TPRM-03` | AutoUnderwriter Agent, LumaAssist Chat | Third-party APIs or hosted services may expose data outside intended jurisdictions or retention rules. | ICT third-party dependency | Cross-border and retention obligations may be breached through vendor tooling. | Review subprocessors, transfer mechanisms, data locations, and logging retention settings. |
| `TPRM-04` | FraudShield | The vendor model is opaque and difficult to challenge when fraud outcomes degrade. | Third-party opacity | The parent inherits a business-critical black box without strong challenge rights. | Define challenge process, threshold reviews, and vendor review cadence with explicit evidence requirements. |
| `TPRM-05` | All, especially FraudShield | Integration-phase outages or degraded vendor service could create immediate business disruption. | Operational resilience | The interim phase increases the chance of control gaps at the exact moment dependency matters most. | Map critical supplier dependencies into the 100-day plan and define manual fallback procedures. |

---

## 9. Company-Wide Interim Integration Risks

| ID | AI Apps | Interim Parent Risk | Theme | Risk | Suggested Controls |
| --- | --- | --- | --- | --- | --- |
| `INT-01` | All | Nordhaven becomes accountable for inherited AI harms before harmonization is complete. | Governance misalignment | Parent and target operate under different policies, evidence standards, and risk appetite. | Define interim AI operating rules approved by the Group Risk Committee. |
| `INT-02` | All | Duplicate platforms and mixed suppliers create exploitable seams during the `12–18 month` transition. | Expanded attack surface | Systems, APIs, and access paths multiply during integration. | Perform transition-specific architecture and access reviews, not just BAU security checks. |
| `INT-03` | All | Key LumaPay engineers may leave before knowledge is captured. | Talent flight / orphaned models | The combined entity may inherit systems no one fully understands or owns. | Identify key people, create runbooks, and assign named owners early in the roadmap. |
| `INT-04` | All | Shadow AI and undocumented tools may remain invisible to Nordhaven’s formal control stack. | Hidden estate risk | The parent may underestimate what it has acquired. | Run discovery and attestation exercises for AI tools, prompts, and datasets. |
| `INT-05` | All | Board reporting may blur current-state inherited risk with target-state planned maturity. | Decision-quality risk | Executives may believe risk has been reduced when only plans exist. | Separate inherited-state risk, planned remediation, and residual risk in all board materials. |
