# Framework Applicability Matrix

## Purpose
Use this matrix to mark whether a framework risk, control theme, or compliance requirement applies to each AI application component.

## How To Use
- mark `✓` if clearly applicable
- mark `~` if partially applicable
- leave blank if not applicable
- use this as a workshop tool, not as the final wording for the board pack

## Important Note
- `NIST`, `EU AI Act`, `GDPR`, and `ISO` do not publish a single official “top 10 risks” list for this scenario, so those rows are **scenario-specific risk themes** derived from the assignment and the relevant standards.
- `OWASP LLM` uses the current OWASP GenAI `Top 10 for LLM Applications 2025`.
- `OWASP Agentic` uses the current OWASP GenAI `Top 10 for Agentic Applications 2026`.
- `OWASP MCP` is a **10-theme working checklist** synthesized from OWASP guidance on secure MCP server development and securely using third-party MCP servers, because OWASP guidance is currently structured as practical guides rather than one standalone MCP “Top 10”.

## Component Key

| Short Name | Component |
| --- | --- |
| `LCEU-API` | `LumaCredit-EU` decision API / decision service |
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

| NIST Risk Theme | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES | LAC-ORCH | LAC-LLM | LAC-MCP | LAC-RAG | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL | FS-WRAP | FS-VENDOR | FS-REVIEW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1. Missing AI governance, ownership, or accountability |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 2. Incomplete AI inventory or dependency mapping |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 3. Uncontrolled `PII` in lower environments |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 4. Weak data lineage, provenance, or data quality |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 5. Model drift or performance degradation not detected |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 6. Human oversight or manual challenge process ineffective |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 7. Logging, traceability, or audit evidence insufficient |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 8. Prompt, tool, or workflow misuse not bounded |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 9. Third-party or supplier dependence not governed |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 10. Incident response, recovery, or fallback maturity weak |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

---

## OWASP LLM Top 10 2025

| OWASP LLM Risk | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES | LAC-ORCH | LAC-LLM | LAC-MCP | LAC-RAG | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL | FS-WRAP | FS-VENDOR | FS-REVIEW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `LLM01` Prompt Injection |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `LLM02` Sensitive Information Disclosure |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `LLM03` Supply Chain |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `LLM04` Data and Model Poisoning |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `LLM05` Improper Output Handling |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `LLM06` Excessive Agency |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `LLM07` System Prompt Leakage |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `LLM08` Vector and Embedding Weaknesses |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `LLM09` Misinformation |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `LLM10` Unbounded Consumption |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

---

## OWASP Agentic Top 10 2026

| OWASP Agentic Risk | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES | LAC-ORCH | LAC-LLM | LAC-MCP | LAC-RAG | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL | FS-WRAP | FS-VENDOR | FS-REVIEW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `ASI01` Agent Goal Hijack |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `ASI02` Tool Misuse and Exploitation |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `ASI03` Identity and Privilege Abuse |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `ASI04` Agentic Supply Chain Vulnerabilities |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `ASI05` Unexpected Code Execution |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `ASI06` Memory and Context Poisoning |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `ASI07` Insecure Inter-Agent Communication |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `ASI08` Cascading Failures |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `ASI09` Human-Agent Trust Exploitation |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| `ASI10` Rogue Agents |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

---

## OWASP MCP Risk Themes

| OWASP MCP Theme | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES | LAC-ORCH | LAC-LLM | LAC-MCP | LAC-RAG | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL | FS-WRAP | FS-VENDOR | FS-REVIEW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1. Tool poisoning |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 2. Prompt injection through MCP-connected content or tools |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 3. Memory poisoning through MCP interactions |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 4. Tool interference or tool chaining abuse |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 5. Weak authentication to MCP servers |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 6. Weak authorization or over-privileged MCP tools |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 7. Weak client isolation or sandboxing |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 8. Unsafe server discovery, onboarding, or trust model |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 9. Insufficient logging and governance of MCP calls |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 10. Missing human-in-the-loop for sensitive MCP actions |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

---

## EU AI Act Risk Themes

| EU AI Act Theme | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES | LAC-ORCH | LAC-LLM | LAC-MCP | LAC-RAG | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL | FS-WRAP | FS-VENDOR | FS-REVIEW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1. High-risk system classification missed or under-scoped |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 2. Risk management system not defined |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 3. Data governance and data quality controls weak |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 4. Technical documentation incomplete |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 5. Logging and record-keeping insufficient |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 6. Transparency to users or deployers weak |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 7. Human oversight ineffective or nominal only |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 8. Accuracy, robustness, or cybersecurity safeguards insufficient |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 9. Post-market monitoring and incident escalation weak |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 10. Conformity assessment readiness poor |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

---

## ISO Risk Themes

| ISO Theme | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES | LAC-ORCH | LAC-LLM | LAC-MCP | LAC-RAG | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL | FS-WRAP | FS-VENDOR | FS-REVIEW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1. AI management system not defined (`ISO/IEC 42001`) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 2. Information security controls weak (`ISO/IEC 27001`) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 3. AI risk treatment not formalized (`ISO/IEC 23894`) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 4. Data quality management weak (`ISO/IEC 5259`) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 5. Supplier governance weak (`ISO/IEC 27036`) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 6. Environment segregation and lower-environment controls weak (`ISO/IEC 27001`) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 7. Change control and release approval weak (`ISO/IEC 42001` / `27001`) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 8. Monitoring, review, and improvement loops weak (`ISO/IEC 42001`) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 9. Traceability, evidence, and auditability weak (`ISO/IEC 42001`) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 10. Business continuity and fallback not defined (`ISO/IEC 27001` / `27036`) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

---

## GDPR Risk Themes

| GDPR Theme | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES | LAC-ORCH | LAC-LLM | LAC-MCP | LAC-RAG | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL | FS-WRAP | FS-VENDOR | FS-REVIEW |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1. Lawful basis, purpose limitation, or fairness unclear |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 2. Data minimization weak |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 3. Live `PII` copied into `test` or lower environments |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 4. International transfer controls weak |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 5. DPIA or privacy risk assessment missing |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 6. Security of processing insufficient |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 7. Logging, retention, or deletion controls weak |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 8. Data subject rights support weak |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 9. Processor / subprocessor governance weak |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 10. Profiling / automated decision-making safeguards weak |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

---

## Suggested First-Pass Priorities
- Start by marking the obvious high-applicability cells for:
- `LCEU-MODEL`
- `LCEU-DATA`
- `LAC-MCP`
- `AUA-MCP`
- `FS-VENDOR`
- Then review:
- lower-environment `PII`
- cross-border data flows
- logging and trace retention
- human oversight
- vendor continuity and fallback

## Source Notes
- OWASP GenAI `Top 10 for LLM Applications 2025`
- OWASP GenAI `Top 10 for Agentic Applications 2026`
- OWASP GenAI guidance on secure MCP server development and secure use of third-party MCP servers
- Assignment slide themes for `NIST AI RMF`, `EU AI Act`, `GDPR`, and `ISO`
