# Clause Traceability Matrix

## Purpose
This matrix links the Capstone risk register, due-diligence checklist, and `100-day` roadmap to framework clauses, articles, functions, or recognized control topics. It is designed for Deliverable B and for checking that Deliverable A is traceable rather than assertion-led.

## Traceability Rules

- Use `NIST AI RMF` as the primary organizing anchor: `Govern`, `Map`, `Measure`, and `Manage`.
- Use clause or article numbers when the current project facts support them.
- Use function-level mapping for `NIST AI RMF` and `NIST CSF` unless a more precise subcategory is agreed by the team.
- Treat ISO clause references as appendix support, not as legal advice or a claim of certification coverage.
- Do not use a framework name alone in the final appendix when a more specific article, clause, function, or control topic is available.

## Framework Reference Set

| Framework Or Regulation | Specific Reference To Use | Capstone Use |
| --- | --- | --- |
| `NIST AI RMF` | `Govern`, `Map`, `Measure`, `Manage` | Primary structure for AI governance, classification, measurement, and treatment. |
| `NIST CSF` | `Identify`, `Protect`, `Detect`, `Respond`, `Recover` | Cyber, logging, monitoring, incident response, and resilience mapping. |
| `EU AI Act` | Annex III high-risk credit and creditworthiness use cases; Article `9` risk management; Article `10` data governance; Article `11` technical documentation; Article `12` record-keeping; Article `13` transparency; Article `14` human oversight; Article `15` accuracy, robustness, and cybersecurity; Article `16` provider obligations; Article `17` quality management system; Article `72` post-market monitoring | High-risk credit decisioning, documentation, oversight, logging, robustness, provider obligations, quality management, and post-market monitoring. |
| `GDPR` / `UK GDPR` | Article `5(1)(b)` purpose limitation; Article `5(1)(c)` data minimisation; Article `5(1)(f)` integrity and confidentiality; Article `25` data protection by design and default; Article `32` security of processing; Article `35` DPIA; Articles `44-49` international transfers | `PII`, lower environments, traces, prompt logs, cross-border transfers, and DPIA evidence. |
| `ISO/IEC 42001` | Clauses `5.3` roles and responsibilities; `6.1` risks and opportunities; `8.2` AI risk assessment; `8.3` AI risk treatment; `9.1` monitoring, measurement, analysis, and evaluation | AI management system, ownership, risk assessment, treatment, and monitoring. |
| `ISO/IEC 27001` | Annex A `5.15` access control; `5.16` identity management; `5.19` information security in supplier relationships; `5.22` monitoring supplier services; `8.15` logging; `8.25` secure development lifecycle; `8.31` separation of development, test, and production environments | IAM, MCP permissions, logging, supplier oversight, secure development, and environment segregation. |
| `ISO/IEC 27036` | Supplier relationship and ICT supply-chain security control topics | Vendor assurance, contract assignment, assurance rights, and external AI dependencies. |
| `ISO/IEC 23894` | AI risk-management process topics | AI risk identification, analysis, evaluation, treatment, and monitoring. |
| `ISO/IEC 5259` | Data quality and data governance topics for analytics and machine learning | Training, validation, scoring data, lineage, and drift-related data quality. |
| `DORA` | Article `5` governance and organization; Article `6` ICT risk management framework; Article `8` identification; Article `10` detection; Article `11` response and recovery; Article `24-25` digital operational resilience testing; Article `28` ICT third-party risk management; Article `30` key contractual provisions | Operational resilience, third-party ICT risk, incident readiness, testing, and vendor contracts. |
| `OWASP LLM Top 10` | Prompt injection, sensitive information disclosure, insecure output handling, excessive agency, overreliance | LLM assistant and agent control mapping. |
| `OWASP Agentic Top 10` | Goal hijack, tool misuse, identity and privilege abuse, agentic supply-chain vulnerabilities, memory and context poisoning, cascading failures, human-agent trust exploitation | Agentic risk mapping for `AutoUnderwriter Agent` and MCP-enabled workflows. |
| `OWASP MCP Themes` | Tool poisoning, MCP-connected prompt injection, memory poisoning, tool chaining abuse, weak authentication, weak authorization, unsafe server discovery, insufficient MCP logging, missing human approval for sensitive actions | MCP server and tool governance for `LumaAssist Chat` and `AutoUnderwriter Agent`. |
| `MITRE ATLAS` | Adversarial ML threat and mitigation topics | Prompt abuse, model misuse, and adversarial testing. |

## Risk-To-Clause Matrix

| Risk ID | Primary Control Objective | Clause / Function Trace | Evidence Artefacts | Related Roadmap Items |
| --- | --- | --- | --- | --- |
| `R-01` | Prevent live customer `PII` from being exposed in lower environments. | `GDPR` Articles `5(1)(c)`, `5(1)(f)`, `25`, `32`; `UK GDPR` equivalent obligations; `ISO/IEC 27001` Annex A `8.31`; `NIST CSF` `Protect`; `NIST AI RMF` `Map` / `Manage` | Environment inventory, dataset register, masking standard, purge plan, exception log, access review. | `I-01`, `I-02`, `I-16` |
| `R-02` | Establish high-risk AI governance for credit decisioning. | `EU AI Act` Annex III creditworthiness use case; Articles `9`, `11`, `13`, `14`, `15`; `ISO/IEC 42001` clauses `5.3`, `6.1`, `8.2`, `8.3`; `NIST AI RMF` `Govern` / `Map` | Classification memo, AI system card, model documentation, approval record, accountability RACI, oversight procedure. | `I-02`, `I-06`, `I-07`, `I-14`, `I-15` |
| `R-03` | Detect and manage model drift in credit decisioning. | `EU AI Act` Article `15`; `NIST AI RMF` `Measure` / `Manage`; `ISO/IEC 42001` clause `9.1`; `ISO/IEC 5259` data quality topics; `NIST CSF` `Detect` | Drift thresholds, validation reports, model performance dashboards, monthly review minutes, escalation records. | `I-07`, `I-09`, `I-13` |
| `R-04` | Reduce prompt-injection and adversarial misuse of the customer assistant. | `OWASP LLM Top 10` prompt injection and insecure output handling; `MITRE ATLAS` adversarial testing topics; `NIST CSF` `Protect` / `Detect`; `NIST AI RMF` `Measure` / `Manage` | Red-team report, abuse-case test suite, prompt hardening record, detection logs, remediation tracker. | `I-12`, `I-13` |
| `R-05` | Restrict `MCP` tool access for customer support to least privilege. | `ISO/IEC 27001` Annex A `5.15`, `5.16`; `OWASP LLM Top 10` excessive agency; `NIST CSF` `Protect`; `NIST AI RMF` `Manage` | MCP inventory, permission matrix, tool allow-list, approval workflow, scoped data-return design. | `I-02`, `I-04`, `I-12`, `I-15` |
| `R-06` | Prevent `PII` leakage through prompts, traces, logs, and observability tooling. | `GDPR` Articles `5(1)(c)`, `5(1)(f)`, `25`, `32`, `35`, `44-49`; `UK GDPR`; `ISO/IEC 27001` Annex A `8.15`; `NIST CSF` `Detect`; `NIST AI RMF` `Map` / `Manage` | Trace samples, redaction standard, retention schedule, access-control evidence, transfer map, DPIA or privacy assessment. | `I-01`, `I-08`, `I-13`, `I-16` |
| `R-07` | Keep underwriting agent authority within documented human-oversight boundaries. | `EU AI Act` Article `14`; `ISO/IEC 42001` clauses `5.3`, `8.2`, `8.3`; `NIST AI RMF` `Govern` / `Manage`; `NIST CSF` `Protect` | Agent design document, no-auto-decision policy, approval checkpoint evidence, override reporting, exception logs. | `I-03`, `I-10`, `I-14`, `I-15` |
| `R-08` | Restrict underwriting agent tools and prevent broad read or write misuse. | `ISO/IEC 27001` Annex A `5.15`, `5.16`, `8.15`; `OWASP LLM Top 10` excessive agency; `MITRE ATLAS`; `NIST CSF` `Protect` / `Detect`; `NIST AI RMF` `Manage` | Tool permission matrix, read/write separation, invocation logs, approval workflow, access review. | `I-02`, `I-04`, `I-12`, `I-15` |
| `R-09` | Preserve audit-ready traceability for underwriting recommendations. | `EU AI Act` Articles `11`, `12`, `13`; `GDPR` Article `5(2)` accountability; `ISO/IEC 42001` clauses `8.2`, `9.1`; `NIST AI RMF` `Measure` | Trace bundle, reason-code documentation, case review pack, sampled explanation records, audit log retention evidence. | `I-08`, `I-10`, `I-15` |
| `R-10` | Confirm critical vendor continuity through change of control and service disruption. | `DORA` Articles `6`, `11`, `28`, `30`; `ISO/IEC 27001` Annex A `5.19`, `5.22`; `ISO/IEC 27036`; `NIST CSF` `Recover`; `NIST AI RMF` `Map` | Vendor contracts, assignment-rights analysis, SLA, assurance reports, fallback runbook, legal summary. | `I-02`, `I-11`, `I-13` |
| `R-11` | Strengthen oversight of opaque third-party fraud model dependency. | `DORA` Articles `28`, `30`; `ISO/IEC 27001` Annex A `5.19`, `5.22`; `ISO/IEC 27036`; `NIST AI RMF` `Map` / `Measure`; `ISO/IEC 42001` clause `9.1` | Vendor assurance pack, model performance trend, challenge rights, supplier review minutes, resilience evidence. | `I-09`, `I-11`, `I-14` |
| `R-12` | Align AI governance during the `12-18 month` parallel operations window. | `NIST AI RMF` `Govern`; `ISO/IEC 42001` clauses `5.3`, `6.1`, `8.2`, `8.3`, `9.1`; `DORA` Article `5`; `NIST CSF` `Identify`; `ISO/IEC 23894` AI risk-management topics | Interim governance charter, RACI, risk forum terms of reference, board reporting pack, decision log, unified AI registry. | `I-02`, `I-03`, `I-05`, `I-14`, `I-15`, `I-16` |
| `R-13` | Discover and govern shadow AI and undocumented tools before Nordhaven inherits blind liability. | `NIST AI RMF` `Map`; `NIST CSF` `Identify`; `ISO/IEC 42001` clauses `4`, `5.3`, `8.2`; `EU AI Act` Articles `6-7`, `9` | Shadow AI discovery evidence, department attestations, AI registry export, risk-tier classification, mandatory disclosure records. | `R-G02`, `R-G05`, `R-O01` |
| `R-14` | Prevent talent flight from creating orphaned, undocumented, or unmaintained AI systems. | `ISO/IEC 42001` clauses `7`, `8`, `9.1`; `EU AI Act` Article `17`; `NIST AI RMF` `Manage`; `ISO/IEC 23894` monitoring and treatment topics | Knowledge-transfer packs, model cards, prompt review records, named backup owners, training records, 180-day review schedule. | `R-G03`, `R-M05`, `R-O01` |
| `R-15` | Confirm IP, data, prompt, model, and output provenance before production reliance. | `GDPR` accountability; `EU AI Act` GPAI and copyright transparency themes; `ISO/IEC 27036`; `ISO/IEC 42001` clauses `6.1`, `8`; `NIST AI RMF` `Map` | Data provenance register, licence register, provider contracts, prompt repository, synthetic-data policy, model lineage evidence. | `R-G02`, `R-M03`, `R-M04`, `R-M05` |
| `R-16` | Detect and prevent discriminatory or unfair credit outcomes. | `EU AI Act` Annex III 5(b), Articles `10`, `15`, `72`; `GDPR` Article `22`; `NIST AI RMF` `Measure`; `ISO/IEC 5259`; `ISO/IEC 42001` clause `9.1` | Fairness assessment, disparate-impact metrics, appeal trends, override trends, data-quality evidence, bias remediation records. | `I-07`, `I-09`, `R-M05`, `R-M07`, `R-O01` |
| `R-17` | Prove human oversight is meaningful and not a rubber-stamp control. | `EU AI Act` Article `14`; `GDPR` Article `22`; `ISO/IEC 42001` clauses `5.3`, `8.2`, `8.3`; `NIST AI RMF` `Govern` / `Manage` | HITL design, reviewer training, reviewer rationale samples, override dashboard, escalation records, automation-bias training evidence. | `I-10`, `R-G03`, `R-M06`, `R-O01` |
| `R-18` | Preserve tamper-evident audit trails and prevent unauthorized model, prompt, rule, or data changes. | `EU AI Act` Articles `12`, `15`; `ISO/IEC 27001` Annex A `8.15`, `8.25`; `NIST CSF` `Protect` / `Detect`; `MITRE ATLAS`; `NIST AI RMF` `Measure` | Immutable or WORM logs, model-version hashes, prompt-version history, change approvals, audit-integrity checks, incident investigation records. | `I-08`, `I-12`, `I-13`, `R-M05`, `R-M07`, `R-O01` |

## Due-Diligence Domain Traceability

| Domain | Required Traceability Standard | Minimum Evidence Standard |
| --- | --- | --- |
| Data and IP | `GDPR` / `UK GDPR` Articles `5`, `25`, `32`, `35`, `44-49`; `ISO/IEC 5259`; `NIST AI RMF` `Map` | Data lineage, transfer maps, masking evidence, retention settings, provenance records, DPIAs or privacy assessments. |
| Model risk | `EU AI Act` Articles `9-15`; `ISO/IEC 42001` clauses `8.2`, `8.3`, `9.1`; `NIST AI RMF` `Govern`, `Measure`, `Manage` | Classification memos, model cards, validation reports, performance dashboards, approval records, drift thresholds. |
| Cyber | `ISO/IEC 27001` Annex A `5.15`, `5.16`, `8.15`, `8.25`, `8.31`; `NIST CSF` `Protect`, `Detect`, `Respond`, `Recover`; `OWASP LLM Top 10`; `MITRE ATLAS` | IAM roles, MCP permissions, logs, red-team results, incident playbooks, vulnerability findings, remediation records. |
| Regulation and ethics | `NIST AI RMF` `Govern`; `ISO/IEC 42001` clauses `5.3`, `6.1`, `8.2`, `8.3`; `EU AI Act` high-risk requirements; `GDPR` accountability and DPIA requirements | Governance charter, RACI, board reports, risk appetite statements, AI impact assessments, legal review notes. |
| Vendor and supply chain | `DORA` Articles `28`, `30`; `ISO/IEC 27001` Annex A `5.19`, `5.22`; `ISO/IEC 27036`; `NIST CSF` `Identify`, `Recover` | Supplier inventory, contracts, assignment-rights analysis, audit rights, SLAs, fallback runbooks, assurance reports. |

## Board-Pack Traceability Check

| Board Slide Topic | Must Trace To | Evidence Source |
| --- | --- | --- |
| Transaction context and AI risk profile | `R-12`; `NIST AI RMF` `Govern`; parallel operations assumption | Company profile, risk register, roadmap `I-03` / `I-05` |
| AI systems in scope | `NIST AI RMF` `Map`; system inventory | HLDs and AI application folders |
| Top `5-7` AI risks | Risk IDs, lens, category, lifecycle stage, KRI, owner, framework mapping | Risk register extract and this matrix |
| Due-diligence evidence requests | Domain traceability, artefact requested, risk addressed | Due-diligence checklist |
| Cyber and monitoring enhancements | `NIST CSF`; `ISO/IEC 27001`; `OWASP LLM Top 10`; `MITRE ATLAS` | Roadmap items `I-04`, `I-08`, `I-09`, `I-12`, `I-13` |
| Risk appetite and tolerance statements | Substrate properties: `Opacity`, `Autonomy`, `Dependency`, `Drift`, `Scale Asymmetry` | Risk appetite document and risk register |
| `100-day` integration plan | Roadmap initiative IDs, risk IDs, maturity shift, `NIST AI RMF` / `NIST CSF` mapping | `100-day-ai-integration-roadmap.md` |
