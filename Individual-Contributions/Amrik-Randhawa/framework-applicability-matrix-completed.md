# Framework Applicability Matrix — Completed
## Nordhaven–LumaPay AI Risk Taskforce

**Document status:** Draft v1.0  
**Prepared by:** Amrik Randhawa 
**Date:** 2026-05-29  
**Source mappings:**
- `03-ai-applications/01-lumaassist-chat/framework-mapping-owasp-mitre-nistcsf.md`
- `03-ai-applications/02-autounderwriter-agent/framework-mapping-nist-mitre-owasp-iso42001.md`
- `03-ai-applications/03-lumacredit-eu/framework-mapping-euaiact-iso42001-iso5259-nistrmf.md`
- `03-ai-applications/04-fraudshield/framework-mapping-iso27036-dora-nistcsf-gdpr-euaiact.md`

---

## Key

| Symbol | Meaning |
|---|---|
| `✓` | Clearly and directly applicable — a concrete gap or risk exists at this component |
| `~` | Partially applicable or conditionally relevant |
| *(blank)* | Not applicable to this component |

---

## Component Reference

| Short Name | Component |
|---|---|
| `LCEU-API` | `LumaCredit-EU` decision API / ECS decision service |
| `LCEU-DATA` | `LumaCredit-EU` feature pipeline, Aurora, S3 feature store / data lake |
| `LCEU-MODEL` | `LumaCredit-EU` SageMaker model endpoint |
| `LCEU-RULES` | `LumaCredit-EU` rules engine and manual review queue |
| `LAC-ORCH` | `LumaAssist Chat` ECS chat orchestrator |
| `LAC-LLM` | `LumaAssist Chat` Bedrock model |
| `LAC-MCP` | `LumaAssist Chat` MCP server and connected tools |
| `LAC-RAG` | `LumaAssist Chat` retrieval index and S3 knowledge base |
| `AUA-ORCH` | `AutoUnderwriter Agent` ECS agent orchestrator |
| `AUA-WF` | `AutoUnderwriter Agent` Step Functions workflow |
| `AUA-LLM` | `AutoUnderwriter Agent` Bedrock model |
| `AUA-MCP` | `AutoUnderwriter Agent` MCP server cluster and tools |
| `AUA-HITL` | `AutoUnderwriter Agent` manual underwriter review queue |
| `FS-WRAP` | `FraudShield` Lambda decision wrapper |
| `FS-VENDOR` | `FraudShield` vendor API |
| `FS-REVIEW` | `FraudShield` manual review / fallback path |

---

## NIST Risk Themes

> Scenario-specific risk themes derived from NIST AI RMF Govern · Map · Measure · Manage applied to the LumaPay estate.

| NIST Risk Theme | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES | LAC-ORCH | LAC-LLM | LAC-MCP | LAC-RAG | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL | FS-WRAP | FS-VENDOR | FS-REVIEW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1. Missing AI governance, ownership, or accountability | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ~ |
| 2. Incomplete AI inventory or dependency mapping | ✓ | ✓ | ✓ | ~ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ~ | ✓ | ✓ | ~ |
| 3. Uncontrolled `PII` in lower environments | ~ | ✓ | ~ |  | ✓ | ✓ | ✓ | ~ | ✓ | ~ | ~ | ✓ |  | ~ |  |  |
| 4. Weak data lineage, provenance, or data quality | ~ | ✓ | ✓ | ~ | ~ | ~ | ~ | ✓ | ~ | ~ | ~ | ✓ |  | ~ | ✓ |  |
| 5. Model drift or performance degradation not detected | ~ | ~ | ✓ | ~ | ~ | ✓ | ~ | ✓ | ~ | ~ | ✓ | ~ | ~ | ✓ | ✓ | ~ |
| 6. Human oversight or manual challenge process ineffective | ~ |  | ~ | ✓ | ✓ | ✓ | ~ |  | ✓ | ~ | ~ | ~ | ✓ | ✓ | ~ | ✓ |
| 7. Logging, traceability, or audit evidence insufficient | ✓ | ~ | ✓ | ✓ | ✓ | ✓ | ✓ | ~ | ✓ | ✓ | ✓ | ✓ | ~ | ✓ | ✓ | ~ |
| 8. Prompt, tool, or workflow misuse not bounded | ~ |  | ~ | ~ | ✓ | ✓ | ✓ | ~ | ✓ | ✓ | ✓ | ✓ | ~ | ~ | ~ |  |
| 9. Third-party or supplier dependence not governed | ✓ | ✓ | ~ |  | ~ | ✓ | ~ | ~ | ~ | ~ | ✓ | ✓ |  | ✓ | ✓ | ~ |
| 10. Incident response, recovery, or fallback maturity weak | ✓ | ~ | ✓ | ✓ | ✓ | ✓ | ~ | ~ | ✓ | ✓ | ✓ | ~ | ~ | ✓ | ✓ | ✓ |

---

## OWASP LLM Top 10 (2025)

> Uses OWASP GenAI Top 10 for LLM Applications 2025. Entries rated blank for components where the risk category is structurally inapplicable (e.g. prompt injection against a non-LLM rules engine).

| OWASP LLM Risk | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES | LAC-ORCH | LAC-LLM | LAC-MCP | LAC-RAG | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL | FS-WRAP | FS-VENDOR | FS-REVIEW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `LLM01` Prompt Injection | ~ |  |  |  | ✓ | ✓ | ✓ | ~ | ✓ | ✓ | ✓ | ✓ |  |  |  |  |
| `LLM02` Sensitive Information Disclosure | ~ | ~ | ~ |  | ✓ | ✓ | ✓ | ✓ | ✓ | ~ | ✓ | ✓ |  | ~ | ~ |  |
| `LLM03` Supply Chain |  |  | ~ |  | ~ | ✓ | ~ | ~ | ~ | ~ | ✓ | ✓ |  | ~ | ✓ |  |
| `LLM04` Data and Model Poisoning |  | ✓ | ~ |  | ~ | ~ | ~ | ✓ | ~ | ~ | ~ | ✓ |  |  | ~ |  |
| `LLM05` Improper Output Handling |  |  |  |  | ✓ | ✓ | ~ |  | ✓ | ✓ | ✓ | ~ |  |  |  |  |
| `LLM06` Excessive Agency |  |  |  |  | ✓ |  | ✓ |  | ✓ | ✓ |  | ✓ |  |  |  |  |
| `LLM07` System Prompt Leakage |  |  |  |  | ✓ | ✓ |  |  | ✓ |  | ✓ |  |  |  |  |  |
| `LLM08` Vector and Embedding Weaknesses |  |  |  |  | ~ |  |  | ✓ |  |  | ~ | ~ |  |  |  |  |
| `LLM09` Misinformation |  |  | ✓ | ~ | ~ | ✓ |  | ✓ |  |  | ✓ | ✓ | ~ |  | ~ |  |
| `LLM10` Unbounded Consumption | ~ |  | ~ |  | ✓ | ✓ | ~ |  | ✓ | ✓ | ✓ | ~ |  | ~ | ~ |  |

---

## OWASP Agentic Top 10 (2026)

> Uses OWASP GenAI Top 10 for Agentic Applications 2026. Strongest applicability to `AutoUnderwriter Agent` and `LumaAssist Chat`. `LumaCredit-EU` and `FraudShield` are not agentic; isolated partial applicability noted where relevant.

| OWASP Agentic Risk | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES | LAC-ORCH | LAC-LLM | LAC-MCP | LAC-RAG | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL | FS-WRAP | FS-VENDOR | FS-REVIEW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `ASI01` Agent Goal Hijack |  |  |  |  | ✓ | ~ | ~ |  | ✓ | ✓ | ✓ | ✓ |  |  |  |  |
| `ASI02` Tool Misuse and Exploitation |  |  |  |  | ~ |  | ✓ |  | ✓ | ✓ |  | ✓ |  |  |  |  |
| `ASI03` Identity and Privilege Abuse |  |  |  |  | ~ |  | ✓ |  | ✓ | ~ |  | ✓ |  | ~ | ~ |  |
| `ASI04` Agentic Supply Chain Vulnerabilities |  |  |  |  | ~ | ✓ | ~ |  | ~ | ~ | ✓ | ✓ |  |  | ~ |  |
| `ASI05` Unexpected Code Execution |  |  |  |  |  |  | ~ |  | ~ | ~ |  | ✓ |  |  |  |  |
| `ASI06` Memory and Context Poisoning |  |  |  |  | ~ | ✓ | ~ | ✓ | ~ | ~ | ✓ | ✓ |  |  |  |  |
| `ASI07` Insecure Inter-Agent Communication |  |  |  |  | ~ |  | ~ |  | ~ | ~ |  | ~ |  |  | ~ |  |
| `ASI08` Cascading Failures |  |  |  |  | ~ |  | ~ |  | ~ | ✓ |  | ✓ |  | ✓ | ✓ |  |
| `ASI09` Human-Agent Trust Exploitation |  |  |  | ~ | ~ | ~ |  |  | ~ |  | ✓ |  | ✓ |  |  | ~ |
| `ASI10` Rogue Agents |  |  |  |  | ~ | ~ |  |  | ~ | ~ | ~ |  |  |  |  |  |

---

## OWASP MCP Risk Themes

> 10-theme working checklist synthesised from OWASP guidance on secure MCP server development. Strongest applicability to `LAC-MCP` and `AUA-MCP`. Other components rated where indirect exposure exists.

| OWASP MCP Theme | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES | LAC-ORCH | LAC-LLM | LAC-MCP | LAC-RAG | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL | FS-WRAP | FS-VENDOR | FS-REVIEW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1. Tool poisoning |  |  |  |  | ~ |  | ✓ |  | ~ |  |  | ✓ |  |  |  |  |
| 2. Prompt injection through MCP-connected content or tools |  |  |  |  | ✓ | ~ | ✓ |  | ✓ | ~ | ~ | ✓ |  |  |  |  |
| 3. Memory poisoning through MCP interactions |  |  |  |  |  | ~ | ✓ |  |  |  | ~ | ✓ |  |  |  |  |
| 4. Tool interference or tool chaining abuse |  |  |  |  | ~ |  | ✓ |  | ~ | ✓ |  | ✓ |  |  |  |  |
| 5. Weak authentication to MCP servers |  |  |  |  | ~ |  | ✓ |  | ~ |  |  | ✓ |  |  |  |  |
| 6. Weak authorization or over-privileged MCP tools |  |  |  |  | ~ |  | ✓ |  | ~ |  |  | ✓ |  |  |  |  |
| 7. Weak client isolation or sandboxing |  |  |  |  | ~ |  | ✓ |  |  | ~ |  | ✓ |  |  |  |  |
| 8. Unsafe server discovery, onboarding, or trust model |  |  |  |  |  |  | ✓ |  |  |  |  | ✓ |  |  |  |  |
| 9. Insufficient logging and governance of MCP calls |  |  |  |  | ~ |  | ✓ |  | ~ |  |  | ✓ |  |  |  |  |
| 10. Missing human-in-the-loop for sensitive MCP actions |  |  |  |  | ~ |  | ✓ |  | ~ |  |  | ✓ | ✓ |  |  |  |

---

## EU AI Act Risk Themes

> Scenario-specific themes derived from EU AI Act Chapter III Section 2 (Articles 9–17), Article 26 (deployer obligations), and Article 72 (post-market monitoring). `LumaCredit-EU` is formally classified as high-risk under Annex III Section 5(b). `AutoUnderwriter Agent` requires classification review. `FraudShield` is likely not high-risk but the determination must be documented and Article 26 deployer obligations apply.

| EU AI Act Theme | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES | LAC-ORCH | LAC-LLM | LAC-MCP | LAC-RAG | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL | FS-WRAP | FS-VENDOR | FS-REVIEW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1. High-risk system classification missed or under-scoped | ✓ | ✓ | ✓ | ✓ | ~ | ~ |  |  | ✓ | ~ | ✓ | ~ | ✓ |  | ~ |  |
| 2. Risk management system not defined (Art. 9) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ~ | ✓ | ✓ | ✓ | ✓ | ✓ | ~ | ~ |  |
| 3. Data governance and data quality controls weak (Art. 10) | ~ | ✓ | ✓ | ~ | ~ |  | ~ | ✓ | ~ | ~ | ~ | ✓ |  |  | ~ |  |
| 4. Technical documentation incomplete (Art. 11 / Annex IV) | ✓ | ✓ | ✓ | ✓ | ~ | ~ |  |  | ✓ | ✓ | ✓ | ✓ | ~ |  | ~ |  |
| 5. Logging and record-keeping insufficient (Art. 12) | ✓ | ~ | ✓ | ✓ | ✓ | ✓ | ~ |  | ✓ | ✓ | ✓ | ✓ |  | ~ | ~ |  |
| 6. Transparency to users or deployers weak (Art. 13) | ~ |  | ✓ | ✓ | ~ | ~ |  |  | ~ |  | ✓ |  | ✓ |  | ~ | ~ |
| 7. Human oversight ineffective or nominal only (Art. 14) | ~ |  | ~ | ✓ | ~ | ~ |  |  | ~ | ~ |  |  | ✓ | ~ |  | ✓ |
| 8. Accuracy, robustness, cybersecurity insufficient (Art. 15) | ~ | ~ | ✓ | ~ | ~ | ✓ |  |  | ~ |  | ✓ | ~ |  |  | ~ |  |
| 9. Post-market monitoring and incident escalation weak (Art. 72) | ~ |  | ✓ | ~ | ~ | ~ |  |  | ~ |  | ✓ |  | ~ |  | ~ |  |
| 10. Conformity assessment readiness poor (Art. 16, 17) | ✓ | ✓ | ✓ | ✓ | ~ | ~ |  |  | ✓ | ~ | ✓ | ~ | ~ |  | ~ |  |

---

## ISO Risk Themes

> Themes derived from ISO/IEC 42001 (AI management system), ISO/IEC 27001 (information security), ISO/IEC 23894 (AI risk management), ISO/IEC 5259 (data quality for AI), and ISO/IEC 27036 (supplier security).

| ISO Theme | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES | LAC-ORCH | LAC-LLM | LAC-MCP | LAC-RAG | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL | FS-WRAP | FS-VENDOR | FS-REVIEW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1. AI management system not defined (`ISO/IEC 42001`) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ~ | ✓ | ✓ | ✓ | ✓ | ✓ | ~ | ✓ |  |
| 2. Information security controls weak (`ISO/IEC 27001`) | ~ | ✓ | ✓ | ~ | ~ | ~ | ✓ |  | ~ | ~ | ~ | ✓ |  | ~ | ✓ |  |
| 3. AI risk treatment not formalised (`ISO/IEC 23894`) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ~ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| 4. Data quality management weak (`ISO/IEC 5259`) | ~ | ✓ | ✓ | ~ |  |  | ~ | ✓ | ~ |  | ~ | ✓ |  |  | ✓ |  |
| 5. Supplier governance weak (`ISO/IEC 27036`) | ✓ | ✓ | ~ |  | ~ | ✓ | ~ |  | ~ |  | ✓ | ✓ |  | ✓ | ✓ |  |
| 6. Environment segregation and lower-environment controls weak (`ISO/IEC 27001`) | ~ | ✓ | ~ |  | ✓ | ~ | ~ |  | ~ |  |  | ~ |  | ~ |  |  |
| 7. Change control and release approval weak (`ISO/IEC 42001` / `27001`) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ~ |  | ✓ | ✓ | ✓ | ✓ |  | ✓ | ~ |  |
| 8. Monitoring, review, and improvement loops weak (`ISO/IEC 42001`) | ~ | ~ | ✓ | ~ | ✓ | ✓ | ~ | ~ | ✓ | ✓ | ✓ | ✓ | ~ | ✓ | ✓ | ~ |
| 9. Traceability, evidence, and auditability weak (`ISO/IEC 42001`) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ~ | ✓ | ✓ | ✓ | ✓ | ~ | ✓ | ✓ | ~ |
| 10. Business continuity and fallback not defined (`ISO/IEC 27001` / `27036`) | ✓ | ~ | ✓ | ✓ | ✓ | ✓ | ~ |  | ✓ | ✓ | ✓ | ~ | ~ | ✓ | ✓ | ✓ |

---

## GDPR Risk Themes

> Scenario-specific themes derived from GDPR and UK GDPR / DPA 2018 obligations as they apply to the four AI applications. Cross-border flows and lower-environment PII are common threads across all systems.

| GDPR Theme | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES | LAC-ORCH | LAC-LLM | LAC-MCP | LAC-RAG | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL | FS-WRAP | FS-VENDOR | FS-REVIEW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1. Lawful basis, purpose limitation, or fairness unclear | ~ | ~ | ~ | ~ | ~ | ~ |  |  | ~ |  | ~ |  |  | ~ | ✓ |  |
| 2. Data minimisation weak | ~ | ~ |  |  | ~ |  | ~ |  | ~ |  |  | ~ |  | ✓ | ✓ |  |
| 3. Live `PII` copied into `test` or lower environments |  | ✓ | ~ |  | ✓ | ✓ | ✓ |  | ✓ | ~ |  | ✓ |  |  |  |  |
| 4. International transfer controls weak | ~ | ✓ |  |  | ~ | ~ |  |  | ~ |  | ~ |  |  | ~ | ✓ |  |
| 5. DPIA or privacy risk assessment missing | ✓ | ✓ | ✓ | ~ | ✓ | ~ | ~ |  | ✓ |  | ✓ | ~ |  | ✓ | ✓ |  |
| 6. Security of processing insufficient | ~ | ✓ | ✓ |  | ~ |  | ✓ |  | ~ |  |  | ✓ |  | ~ | ✓ |  |
| 7. Logging, retention, or deletion controls weak | ✓ | ✓ | ~ |  | ✓ | ✓ | ~ |  | ✓ |  | ~ | ~ |  | ~ | ✓ |  |
| 8. Data subject rights support weak | ~ | ~ |  | ~ | ~ |  |  |  | ~ |  |  |  | ~ | ~ | ✓ |  |
| 9. Processor / subprocessor governance weak | ✓ | ~ |  |  | ~ | ✓ |  |  | ~ |  | ✓ | ~ |  |  | ✓ |  |
| 10. Profiling / automated decision-making safeguards weak | ~ |  | ✓ | ✓ | ~ | ~ |  |  | ~ |  | ✓ |  | ✓ | ~ | ✓ | ✓ |

---

## Heat Map — Highest-Density Components

The summary below counts `✓` cells per component across all seven framework tables. It indicates which components carry the broadest risk exposure across the full framework set and should be prioritised in the risk register and 100-day plan.

| Component | ✓ Count | Risk Concentration Summary |
|---|---|---|
| `AUA-MCP` | 38 | Highest across the estate — MCP tool permissions, agentic agency, data access, supply chain, ISO controls, GDPR |
| `AUA-ORCH` | 34 | Governance, logging, change control, incident response, GDPR, EU AI Act |
| `LAC-MCP` | 33 | MCP themes dominate; prompt injection, excessive agency, authentication, authorization |
| `LCEU-DATA` | 30 | Data quality (ISO 5259), PII in test, GDPR, EU AI Act Art. 10, lineage |
| `LCEU-MODEL` | 29 | EU AI Act Art. 9–15, drift, ISO 42001, traceability, accuracy |
| `AUA-LLM` | 28 | Misinformation, supply chain, EU AI Act, ISO 42001, GDPR Art. 22 |
| `LAC-ORCH` | 27 | Prompt injection, governance, logging, GDPR, change control |
| `FS-VENDOR` | 27 | ISO 27036, DORA Art. 30, GDPR Art. 28, supplier governance — all concentrated here |
| `LCEU-API` | 22 | Governance, logging, GDPR, EU AI Act, supplier (bureau APIs), incident response |
| `LCEU-RULES` | 20 | EU AI Act Art. 12–14, change control, traceability, human oversight |
| `AUA-WF` | 19 | Step Functions workflow — change control, logging, agentic risks, cascading failure |
| `LAC-LLM` | 18 | Misinformation, supply chain, system prompt leakage, NIST CSF |
| `AUA-HITL` | 15 | Human oversight (EU AI Act Art. 14, NIST GOVERN), automation bias, GDPR Art. 22 |
| `FS-WRAP` | 14 | Fallback design, credential management, GDPR data minimisation, NIST CSF |
| `LAC-RAG` | 13 | Vector store, data poisoning, ISO 5259, GDPR retention |
| `FS-REVIEW` | 7 | Fallback path — incident response, recovery, human oversight, DORA |

---

## Source Notes

| Table | Primary Sources |
|---|---|
| NIST Risk Themes | NIST AI RMF Govern · Map · Measure · Manage; assignment scenario themes |
| OWASP LLM Top 10 | OWASP GenAI Top 10 for LLM Applications 2025 |
| OWASP Agentic Top 10 | OWASP GenAI Top 10 for Agentic Applications 2026 |
| OWASP MCP Themes | OWASP guidance on secure MCP server development and secure use of third-party MCP servers |
| EU AI Act Themes | EU AI Act (Regulation 2024/1689) Chapter III Section 2, Articles 9–17, 26, 72 |
| ISO Themes | ISO/IEC 42001:2023, ISO/IEC 27001:2022, ISO/IEC 23894:2023, ISO/IEC 5259 series, ISO/IEC 27036 series |
| GDPR Themes | GDPR (Regulation 2016/679), UK GDPR, UK DPA 2018 |

---

*This completed matrix feeds directly into the risk register at `04-risk-and-controls/risk-register-template.md`, the board deck at `05-deliverables/board-deck-draft-v1.md`, and the 100-day integration roadmap at `04-risk-and-controls/100-day-ai-integration-roadmap.md`.*
