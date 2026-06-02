# AutoUnderwriter Agent — Framework Mapping
## NIST AI RMF · MITRE ATLAS · OWASP LLM Top 10 (2025) · ISO/IEC 42001

**Document status:** Draft v1.0  
**Prepared by:** Nordhaven–LumaPay AI Risk Taskforce  
**Role context:** Amrik Randhawa 
**Date:** 2026-05-29  


---

## 1. Purpose and Scope

This document maps AutoUnderwriter Agent against four frameworks:

- **NIST AI RMF** — Govern · Map · Measure · Manage (the primary capstone anchor framework)
- **MITRE ATLAS** — adversarial threat modelling for AI/ML systems
- **OWASP LLM Top 10 (2025)** — application-level LLM threat catalogue
- **ISO/IEC 42001** — AI management system standard (governance, lifecycle, accountability)

The mapping is performed at the component level using the five AutoUnderwriter Agent components defined in the Framework Applicability Matrix:

| Component ID | Description |
|---|---|
| `AUA-ORCH` | ECS agent orchestrator — entry point, session management, workflow dispatch |
| `AUA-WF` | AWS Step Functions workflow — sequences tool calls, manages agent reasoning loop |
| `AUA-LLM` | Amazon Bedrock model — inference, recommendation generation, case summarisation |
| `AUA-MCP` | Internal MCP server cluster — affordability checks, policy lookup, fraud/identity tools, document retrieval, case summarisation tools |
| `AUA-HITL` | Manual underwriter review queue — human approval checkpoint before any credit decision is issued |

**Out of scope for this document:** LumaAssist Chat, LumaCredit-EU, FraudShield. Those are mapped separately.

---

## 2. System Snapshot — Why This System Demands the Most Rigorous Treatment

AutoUnderwriter Agent carries the highest inherent risk profile of the four LumaPay AI systems for three compounding reasons:

| Factor | Detail |
|---|---|
| **Decision criticality: High** | Recommendations influence real credit decisions affecting customers' access to BNPL and SME lending. A wrong recommendation, if rubber-stamped, causes direct financial harm |
| **Agentic pattern** | The system chains multiple tool calls autonomously through Step Functions before a human sees the output. Each tool call is an opportunity for control to break silently |
| **Substrate properties: Autonomy + Dependency + Emergent Capability** | The agent's real-world authority is the product of its tool permissions multiplied by its reasoning chains — both of which can expand incrementally without a governance change being formally acknowledged |
| **Document ingestion attack surface** | Real customer-uploaded financial documents (bank statements, payslips, accounts) enter the agent's context. These are adversarially controllable inputs in a way that chat messages are not — a prepared adversary can embed instructions in a document |
| **MCP cluster breadth** | A single agent session can invoke affordability scoring, fraud/identity checks, policy lookup, and document retrieval tools — each connecting to live Aurora PostgreSQL or S3 data |
| **Human override fatigue risk** | The HITL checkpoint is real but fragile: underwriters reviewing high volumes of pre-packaged recommendations are susceptible to automation bias and rubber-stamping |
| **Traceability required by regulators** | FCA Consumer Duty, UK GDPR Article 22, and EU AI Act Article 13 all create obligations to explain how a credit-related recommendation was generated. The current HLD has no explainability or audit-trail guarantee |
| **No dedicated security team at LumaPay** | The most autonomous and consequential AI system in the estate operates with no security team to review it |

---

## 3. NIST AI RMF Mapping

The NIST AI Risk Management Framework organises AI risk management into four functions: **GOVERN → MAP → MEASURE → MANAGE**. For AutoUnderwriter Agent, all four functions have specific, actionable requirements.

---

### 3.1 GOVERN

> Establish the policies, accountability structures, and oversight mechanisms that create organisational capacity to manage AI risk responsibly.

The GOVERN function is foundational — without it, MAP, MEASURE, and MANAGE lack authority. For AutoUnderwriter Agent, GOVERN is currently the weakest function.

#### GV.1 — Policies, Processes, Procedures, and Practices

| Sub-function | Requirement for AutoUnderwriter Agent | Current State | Required State |
|---|---|---|---|
| GV.1.1 | Policies are in place governing the agent's permitted scope: which decisions it can prepare, which tools it can invoke, and what it is explicitly prohibited from doing | No AI-specific policy documented for AutoUnderwriter Agent | Formal acceptable-use and scope policy approved by Chief Credit Officer and reviewed by Legal |
| GV.1.2 | Roles and responsibilities clearly assigned: executive owner, technical owner, risk owner, and data owner | Executive owner (Chief Credit Officer) and technical owner (AI Workflow Lead) named in HLD but not formally appointed with documented accountabilities | Formal ownership matrix published; each role has defined responsibilities and escalation authority |
| GV.1.3 | AI risk tolerance for credit-decision automation is explicitly defined and board-approved | Not documented. LumaPay has no AI risk appetite statement | AI risk appetite statement published, covering: autonomous decision tolerance, override rate thresholds, acceptable recommendation error rate, and MCP tool-scope limits |
| GV.1.4 | Change management process exists for agent updates: new tools, new prompts, Step Functions workflow changes, and MCP schema changes | No evidence of formal change control for agent components | Stage-gate change approval process: all MCP tool additions, prompt changes, and workflow modifications require review and sign-off before deployment |
| GV.1.5 | Third-party AI dependencies (Bedrock, LangSmith, external fraud/identity APIs) are governed through a formal supplier policy | No supplier governance documented | Third-party AI supplier policy in place; Bedrock and all MCP-connected external APIs under contract review |

**Gap assessment:** LumaPay has no governance infrastructure for AutoUnderwriter Agent. The Chief Credit Officer is named as executive owner in the HLD but has no documented accountability, escalation authority, or risk appetite parameters to operate against. This is a pre-close critical gap.

---

#### GV.2 — Accountability and Responsibility

| Sub-function | Requirement for AutoUnderwriter Agent | Current State | Required State |
|---|---|---|---|
| GV.2.1 | Accountable individual formally owns the system and is answerable to the board for its outputs | Named in HLD but not formally accountable | Chief Credit Officer formally accountable; reports to Group Risk Committee on agent performance |
| GV.2.2 | Human underwriters understand their role as genuine decision-makers, not ratifiers of agent output | No training or operating procedure documented | Underwriter operating procedure defines: what the recommendation pack contains, what the underwriter must independently verify, and what constitutes unacceptable rubber-stamping |
| GV.2.3 | Override decisions are logged and reviewed | No override logging process described | Every underwriter override recorded with rationale; override rate reported monthly to Chief Credit Officer |
| GV.2.4 | Incident escalation authority is defined for agent misbehaviour | No AI incident playbooks | Escalation matrix published: agent producing unsafe recommendations → Chief Credit Officer + CISO within 1 hour |

---

#### GV.3 — Organisational Culture

| Sub-function | Requirement for AutoUnderwriter Agent | Current State | Required State |
|---|---|---|---|
| GV.3.1 | Teams building and operating the agent understand AI risk concepts: emergent capability, automation bias, and prompt injection | No AI risk training programme at LumaPay | AI risk awareness training mandatory for engineering, underwriting, and operations teams before go-live |
| GV.3.2 | Psychological safety exists for underwriters to reject agent recommendations | Unknown — no data | Override rate is treated as a quality signal, not a performance metric against underwriters |

---

### 3.2 MAP

> Understand the context, capabilities, and risks of the AI system with enough precision to make governance decisions based on evidence, not assumption.

The MAP function translates the HLD into a risk-grade system classification that drives all downstream decisions.

#### System Classification

| Dimension | Assessment | Basis |
|---|---|---|
| **Risk tier** | High | Credit decisions affecting financial access; FCA Consumer Duty applies; UK GDPR Article 22 relevance |
| **Decision type** | Consequential, human-in-the-loop | Agent prepares; human approves — but automation bias degrades HITL effectiveness at scale |
| **Substrate properties** | Autonomy · Dependency · Emergent Capability | Multi-step tool chaining without per-step human review; relies on external Bedrock and fraud APIs; incremental tool additions expand real authority |
| **Data sensitivity** | Very High | Customer PII, financial statements, identity documents, underwriting rationale — all present in context window and traces |
| **Regulatory exposure** | High | FCA, Consumer Duty, UK GDPR Article 22, EU AI Act (potential high-risk classification under Annex III credit scoring) |

#### MAP Actions for AutoUnderwriter Agent

| MAP Sub-function | What Must Be Done | Current State |
|---|---|---|
| MAP.1 — Context | Document the business context: which lending products use the agent, which customer segments, and what decisions it influences | Not fully documented |
| MAP.2 — Categorise | Formally classify AutoUnderwriter Agent as a consequential, high-criticality AI system — triggering the full NIST AI RMF treatment | Not classified |
| MAP.3 — AI risks identified | Enumerate the specific risks: excessive autonomy, MCP overreach, document injection, override fatigue, traceability gap, emergent capability creep | Partial — risk list exists in `04-risk-and-controls` but not formally linked to the system |
| MAP.4 — Risk context | Map each risk to a concrete scenario: what fails, who is harmed, which regulation is breached | Not done |
| MAP.5 — Impacts | Define downstream impacts: customer denied credit unfairly, complaint upheld, regulator investigates, reputational damage to Nordhaven post-acquisition | Not documented |

**Component-level dependency map:**

```
Customer Application → AUA-ORCH → AUA-WF (Step Functions)
                                      ├─→ AUA-LLM (Bedrock inference)
                                      └─→ AUA-MCP
                                               ├─→ Affordability Tool → Aurora PostgreSQL
                                               ├─→ Policy Lookup Tool → S3 Policy Store
                                               ├─→ Document Retrieval Tool → S3 Document Store
                                               ├─→ Fraud / Identity Tool → External API (third-party)
                                               └─→ Case Summarisation Tool → Case Management System
                                      └─→ AUA-HITL (Underwriter queue — mandatory)
```

Every node in this map is a dependency. If any node fails, returns corrupt data, or is manipulated, the recommendation pack delivered to `AUA-HITL` is compromised — and the underwriter may not know.

---

### 3.3 MEASURE

> Assess the severity, likelihood, and current control effectiveness of identified risks with evidence — not assertion.

#### Risk Register Extract — AutoUnderwriter Agent

| # | Risk | Likelihood | Impact | Current Control Maturity | Key Risk Indicator |
|---|---|---|---|---|---|
| 1 | Excessive agent autonomy — agent chains tools and generates recommendations beyond intended scope | Medium | High | Low — no scope boundary formally defined | Number of multi-step tool chains exceeding defined maximum per session |
| 2 | MCP tool permission overreach — agent accesses data beyond case scope | Medium | High | Low — no least-privilege model documented | Number of MCP tool calls per session that retrieve records outside the submitted case |
| 3 | Prompt injection through uploaded documents | Medium | High | None — no document sanitisation described | Number of flagged anomalous tool invocations correlated with specific document submissions |
| 4 | Recommendation traceability gap — cannot explain why a recommendation was made | High | High | Low — traces exist in LangSmith but no structured explainability output | Percentage of recommendations where the evidence bundle is auditor-complete |
| 5 | Human override fatigue — underwriters rubber-stamp agent output | High | High | None — no override rate monitoring or training | Override rate trend (declining rate without corresponding quality improvement is a warning signal) |
| 6 | Unredacted PII in `test` — adversarial agent tests run against live customer data | High | High | None — confirmed present | Number of test-environment sessions containing live PII (target: zero) |
| 7 | Tool-chain dependency failure — tool returns partial or inconsistent data silently | Medium | Medium | Low — no documented failure-handling logic | Tool error rate, partial-response rate, and recommendation-generation failure rate |
| 8 | Cross-border trace retention — LangSmith and Datadog traces cross US boundary with sensitive financial data | High | High | None — no data-flow controls documented | Confirmation that LangSmith data residency is EU/UK or that transfer controls are in place |
| 9 | Emergent capability creep — incremental tool additions expand agent authority without governance review | Medium | High | None — no change control for MCP schemas | Number of MCP tool scope changes in past 12 months reviewed through formal governance |

#### Measurement Indicators (KRIs)

The following KRIs should be reported monthly to the AI Risk Forum and quarterly to the Group Risk Committee:

| KRI | Threshold (Amber) | Threshold (Red) | Data Source |
|---|---|---|---|
| Override rate — underwriter rejects or modifies agent recommendation | < 5% (possible automation bias) | > 30% (agent quality failing) | AUA-HITL queue logs |
| Unsupported recommendation rate — recommendation cannot be traced to tool outputs | > 2% | > 5% | LangSmith trace review |
| MCP tool error rate — tool call returns error or null in live workflow | > 1% | > 5% | CloudWatch / Datadog |
| Agent sessions exceeding max tool-call limit | > 0 | > 5 per day | Step Functions execution logs |
| PII detected in test environment | > 0 | > 0 (binary — never acceptable) | DSPM scan / manual audit |
| Adverse case outcomes correlated with agent recommendation | > 2% | > 5% | Case management outcome data |

---

### 3.4 MANAGE

> Take risk treatment actions — prioritised, practical, and sequenced for the integration period.

The MANAGE function converts MEASURE findings into actions. For AutoUnderwriter Agent, these are the highest-priority treatment actions within the 100-day integration plan:

#### Pre-Close Critical (Day 0–5)

| Action | Rationale | Owner |
|---|---|---|
| Halt use of unredacted PII in `test` for agent testing | Live financial documents and identity data in test is an active GDPR/UK GDPR breach risk | Engineering + DPO |
| Freeze all new MCP tool additions pending a permission review | Every new tool increases the agent's real authority; freeze until a baseline is established | Chief Credit Officer + CISO |
| Document the current MCP tool inventory — name, scope, data access, and IAM role | Cannot manage what is not inventoried | AI Workflow Engineering Lead |

#### Day 1–30

| Action | Rationale | Owner |
|---|---|---|
| Define and publish the agent scope policy: permitted tools, permitted data access, maximum tool-chain length per session | Establishes the governance baseline that all subsequent controls reference | Chief Credit Officer + Legal |
| Implement session-scoped authorisation for all MCP tool calls: each call restricted to the submitted case ID | Eliminates the MCP overreach vector — tool calls cannot retrieve data for cases other than the one being processed | Engineering |
| Add document sanitisation at the ingestion layer — scan uploaded documents for adversarial instruction patterns before passing to agent context | Closes the document-based prompt injection vector | Engineering + Security |
| Enable structured explainability output in the recommendation pack: for each recommendation point, record which tool output and which prompt segment produced it | Required for FCA, Consumer Duty, and UK GDPR Article 22 compliance | Engineering + Governance |
| Configure override-rate monitoring in CloudWatch and Datadog; report weekly to Chief Credit Officer | Override rate is the primary signal of automation bias and HITL degradation | Engineering + Operations |

#### Day 31–60

| Action | Rationale | Owner |
|---|---|---|
| Conduct full IAM privilege review: Bedrock invocation role, all MCP tool service accounts, Step Functions execution role, S3 and Aurora access | Identify and remediate over-privileged roles before Nordhaven completes integration | Cloud Security / Platform |
| Deploy PII redaction before trace data is written to LangSmith and Datadog | Closes the cross-border trace exposure vector; required for GDPR/UK GDPR | Engineering + DPO |
| Conduct supplier security assessment for LangSmith (data residency, DPA, incident notification) and all external fraud/identity API providers | Required under ISO/IEC 27036 and NIST AI RMF supplier governance | Legal + GRC |
| Deliver underwriter training: role of the recommendation pack, what to independently verify, how to escalate concerns, override recording procedure | Converts HITL from nominal to effective | Operations + HR |
| Publish AI incident playbooks: agent producing unsafe recommendation, MCP tool abuse, document injection detected, Bedrock unavailability | Cannot respond to what has not been planned for | CISO |

#### Day 61–100

| Action | Rationale | Owner |
|---|---|---|
| Run a formal red-team exercise against the agent: document injection attacks, MCP permission probing, jailbreak via case notes | Evidence of attack resistance required for board pack | CISO + Engineering |
| Establish a quarterly agent review cycle: output quality, override trends, tool scope review, emergent capability check | Converts one-time actions into a managed AI lifecycle | AI Risk Forum |
| Implement synthetic data pipeline for test environment: all agent testing uses anonymised or synthetic financial documents | Permanent solution replacing the "halt unredacted PII" interim measure | Engineering + DPO |
| Publish AutoUnderwriter Agent in the unified AI registry with classification, ownership, risk rating, and review schedule | Required for Nordhaven's group-level AI governance | GRC |

---

## 4. MITRE ATLAS Mapping

For an agentic underwriting workflow, MITRE ATLAS is particularly relevant because the attack surface is broader than a simple LLM chat interface: adversaries can manipulate the agent through uploaded documents, tool-chain exploitation, credential compromise, and workflow logic abuse.

### 4.1 Reconnaissance

| Technique | ID | Relevance to AutoUnderwriter Agent | Component | Gap |
|---|---|---|---|---|
| Discover ML Model Ontology | AML.T0013 | An internal adversary (rogue employee, compromised underwriter account) probes the agent by submitting crafted cases to map its reasoning patterns, tool invocation sequence, and decision boundaries before crafting a targeted attack | `AUA-LLM` `AUA-ORCH` | No detection for probe patterns in LangSmith or CloudWatch |
| Discover ML Model Family | AML.T0014 | Attacker infers the underlying Bedrock model to use known model-specific jailbreaks tuned to that model's weaknesses | `AUA-LLM` | Model identity potentially inferable from error messages or response structure |
| Gather ML Artifacts | AML.T0002 | Attacker with access to LangSmith or Datadog traces extracts prompt templates, tool schemas, and workflow logic to build an offline replica for attack development | `AUA-ORCH` `AUA-WF` | LangSmith and Datadog access controls undocumented; traces contain rich agent reasoning data |

**Control:** Restrict LangSmith and Datadog to security and audit roles. Normalise error messages to remove model identity signals. Add anomaly detection for repeated low-diversity case submissions.

---

### 4.2 ML Attack Staging

| Technique | ID | Relevance to AutoUnderwriter Agent | Component | Gap |
|---|---|---|---|---|
| Craft Adversarial Data | AML.T0043 | Attacker prepares a financial document (bank statement, payslip) with embedded adversarial instructions designed to manipulate the agent's tool invocations or recommendation output | `AUA-MCP` `AUA-LLM` | No document sanitisation or adversarial input filtering before documents enter the agent context |
| Create Proxy ML Model | AML.T0005 | Attacker submits many carefully varied cases to extract a behavioural model of the underwriting agent, enabling offline development of optimal manipulation inputs | `AUA-LLM` `AUA-WF` | No rate limiting or case submission anomaly detection at API Gateway |
| Poison Training Data | AML.T0020 | If the agent's outputs are used downstream to fine-tune or evaluate models, poisoned case submissions can corrupt that feedback loop | `AUA-LLM` | No documented control separating agent outputs from any downstream training pipeline |

**Control:** Implement document pre-processing to extract text and strip metadata/embedded objects before passing to agent context. Apply rate limiting on the underwriting API. Establish a clear policy prohibiting agent output from entering training data without human-reviewed curation.

---

### 4.3 Initial Access

| Technique | ID | Relevance to AutoUnderwriter Agent | Component | Gap |
|---|---|---|---|---|
| LLM Prompt Injection | AML.T0051 | Adversarial text embedded in an uploaded financial document instructs the agent to invoke MCP tools outside case scope, modify its recommendation, or expose internal policy logic | `AUA-MCP` `AUA-LLM` `AUA-WF` | No prompt-injection detection on document content entering the context window — critical gap |
| Valid Accounts | AML.T0012 | Attacker uses a compromised underwriter account or IAM credential to access the underwriting workbench, submit crafted cases, or directly call MCP tool endpoints | `AUA-ORCH` `AUA-MCP` | IAM roles and underwriter account access controls not reviewed; no MFA enforcement confirmed |
| Exploit Public-Facing ML Application | AML.T0049 | The underwriting API gateway is accessible to internal users — a malicious insider or compromised developer can submit specially crafted cases at scale | `AUA-ORCH` | No anomaly detection on case submission patterns; insider risk not formally addressed |

**Control:** Treat all document content as untrusted input — extract text, apply injection pattern detection, and enforce structural validation before passing to agent context. Enforce MFA for all underwriting workbench access. Deploy anomaly detection on case submission volume and pattern.

---

### 4.4 Execution — Agent Workflow Exploitation

This tactic class is uniquely relevant to AutoUnderwriter Agent because the agent executes multi-step tool chains autonomously through Step Functions. An attacker who can influence the agent's reasoning can drive arbitrary tool invocations.

| Technique | ID | Relevance to AutoUnderwriter Agent | Component | Gap |
|---|---|---|---|---|
| LLM Jailbreak | AML.T0054 | Crafted case submission or embedded document content bypasses the agent's behavioural guardrails, causing it to produce recommendations that violate policy (e.g., approving a case that should be rejected, or generating a recommendation with fabricated evidence) | `AUA-LLM` `AUA-ORCH` | No jailbreak test suite documented; Bedrock Guardrails configuration not described |
| Indirect Prompt Injection | AML.T0051.001 | A case management system note, a document retrieved from S3, or a fraud-tool response contains adversarial text that re-enters the agent's context window and redirects its subsequent reasoning | `AUA-MCP` `AUA-LLM` | All MCP tool returns are passed into model context without secondary sanitisation |
| Exploit ML Software | AML.T0047 | Vulnerabilities in the ECS container images, Step Functions definitions, or MCP server code are exploited to alter agent behaviour outside the model layer | `AUA-ORCH` `AUA-WF` `AUA-MCP` | No CSPM; no container image vulnerability scanning described |

**Control:** Configure Bedrock Guardrails with topic restrictions for the underwriting context. Treat all MCP tool returns as untrusted — apply secondary input validation before re-injection into context. Implement container image scanning in the CI/CD pipeline.

---

### 4.5 Privilege Escalation — MCP Tool Abuse

| Technique | ID | Relevance to AutoUnderwriter Agent | Component | Gap |
|---|---|---|---|---|
| Manipulate ML Model Input | AML.T0031 | Attacker crafts inputs that cause the agent to invoke higher-privilege MCP tools than the submitted case requires — for example, causing the fraud tool to query identity records for individuals not associated with the case | `AUA-MCP` | No session-scoped authorisation model for MCP tool calls; tools can potentially be invoked with arbitrary parameters |
| Establish Accounts | AML.T0036 | Attacker creates or elevates a service account with access to MCP tool endpoints, bypassing the agent orchestrator and calling tools directly | `AUA-MCP` | MCP tool endpoints accessible via internal network; direct API access controls unreviewed |

**Control:** Session-scoped MCP authorisation: every tool call must be bound to the case ID of the active session and validated at the MCP server — not just at the orchestrator. MCP tool endpoints must not be directly callable without going through the orchestrator's session context.

---

### 4.6 Collection and Exfiltration

| Technique | ID | Relevance to AutoUnderwriter Agent | Component | Gap |
|---|---|---|---|---|
| Data from ML Artifacts | AML.T0037 | Attacker extracts financial documents, identity records, and underwriting rationale from LangSmith traces, CloudWatch logs, or S3 document store via compromised credentials or misconfigured bucket policies | `AUA-MCP` `AUA-ORCH` | No DSPM; S3 bucket policies unreviewed; LangSmith traces contain highly sensitive financial PII |
| Exfiltration via ML Inference API | AML.T0025 | Attacker uses crafted case submissions to cause the agent to reproduce sensitive data (other customers' financial details, internal policy rules) in its recommendation output | `AUA-LLM` `AUA-MCP` | No output monitoring for data-exfiltration patterns; session-scoped data boundaries not enforced |
| Data from Cloud Storage | AML.T0035 | Direct exfiltration from S3 document store or Aurora PostgreSQL via over-privileged IAM role or misconfigured S3 bucket ACL | `AUA-MCP` | No CSPM; IAM roles unreviewed; S3 bucket policies not confirmed |

**Control:** Deploy DSPM tooling to classify and alert on sensitive data in S3, Aurora, and trace stores. Implement S3 access logging with anomaly alerting. Apply PII detection on model outputs. Review all IAM roles for least-privilege.

---

### 4.7 Impact

| Technique | ID | Relevance to AutoUnderwriter Agent | Component | Gap |
|---|---|---|---|---|
| Harm to Other Systems via Compromised ML | AML.T0048 | Manipulated agent produces systematically biased recommendations: approving fraudulent applications, rejecting legitimate ones, or generating fabricated evidence bundles that underwriters ratify without challenge | `AUA-LLM` `AUA-HITL` | Override rate not monitored; no systematic quality review of agent recommendations |
| Denial of ML Service | AML.T0029 | High-volume or computationally expensive case submissions exhaust Bedrock token quota, Step Functions concurrency, or MCP tool capacity — stalling the underwriting queue | `AUA-ORCH` `AUA-WF` `AUA-LLM` | No rate limiting on case submission API; no queue depth alerting |
| Evade ML Model | AML.T0015 | Attacker learns the agent's guardrail patterns (via proxy model or prompt probing) and crafts inputs that produce policy-violating recommendations while evading all detection rules | `AUA-LLM` | No guardrail evasion testing documented |

**Control:** Implement queue depth and latency alerting in CloudWatch. Establish a monthly case-sample review: human auditors review a random sample of agent recommendation packs for quality, accuracy, and policy compliance. Define a kill-switch: ability to route all cases to full human underwriting if agent integrity is in question.

---

## 5. OWASP LLM Top 10 (2025) Mapping

For an agentic underwriting system, the OWASP LLM Top 10 risks are weighted differently from a customer-facing chatbot. LLM06 Excessive Agency and LLM01 Prompt Injection are the dominant concerns because the system has both consequential outputs and multi-tool execution authority.

---

### LLM01 — Prompt Injection

**Applicability:** `✓ AUA-ORCH` · `✓ AUA-LLM` · `✓ AUA-MCP` · `✓ AUA-WF`

**How it applies:**  
AutoUnderwriter Agent has a more dangerous prompt injection surface than a chat assistant because the injected content can drive **tool execution**, not just text generation. Two distinct vectors exist:

1. **Document-based injection (highest severity):** A customer or fraudster submits a crafted financial document (bank statement, payslip, identity document) containing embedded instructions. When the document retrieval MCP tool extracts and passes the text to the agent's context, those instructions enter the model's reasoning chain. The agent may then invoke tools it should not, modify its recommendation, or suppress evidence in the output pack. This attack is particularly dangerous because the injection arrives through a legitimate, expected data pathway — and the content is inherently trusted because it comes from an "internal" MCP tool.

2. **Case note injection:** Adversarial text in a case management note (entered by a rogue employee or a compromised system) is retrieved by the MCP case summarisation tool and re-injected into the context.

**Current gap:** No document content sanitisation before ingestion into agent context. MCP tool returns are passed directly into model context without secondary validation.

**Required controls:**
- Pre-process all uploaded documents: extract plain text, strip metadata and embedded objects, apply injection-pattern detection before the text reaches the agent
- Treat all MCP tool returns as untrusted data regardless of source — apply structural validation before re-injection
- Implement a "taint" marker in the prompt construction: content from untrusted sources (documents, case notes) must be structurally separated from system instructions
- Include document-based injection scenarios in the red-team test suite

---

### LLM02 — Sensitive Information Disclosure

**Applicability:** `✓ AUA-LLM` · `✓ AUA-MCP` · `✓ AUA-ORCH`

**How it applies:**  
The agent's context window contains extraordinarily sensitive data: financial statements, identity documents, affordability calculations, fraud scores, and underwriting rationale. Three disclosure vectors exist:

1. **Cross-case leakage:** Without session-scoped authorisation, a crafted prompt could cause the agent to retrieve and include data from a different case or customer in its recommendation output.
2. **Trace leakage:** LangSmith traces contain the full agent reasoning chain including all tool inputs and outputs — meaning full financial documents and identity data are present in a third-party SaaS with unreviewed access controls.
3. **Policy rule disclosure:** The agent can potentially be prompted to reproduce the content of internal policy documents retrieved by the policy lookup tool.

**Current gap:** No session-scoped authorisation for MCP tools. LangSmith DPA and access controls not reviewed. No PII redaction before traces are written.

**Required controls:**
- Session-scoped MCP authorisation enforced at the tool server layer — not just in the orchestrator prompt
- PII and document content redacted or tokenised before writing to LangSmith traces
- Policy documents retrieved by MCP tools should be used for reasoning but not reproduced verbatim in model outputs
- LangSmith treated as a personal data processor — DPA required, data residency confirmed

---

### LLM03 — Supply Chain

**Applicability:** `✓ AUA-LLM` · `~ AUA-MCP` · `~ AUA-WF`

**How it applies:**  
AutoUnderwriter Agent has a richer supply chain than LumaAssist Chat because it also uses external fraud and identity APIs through its MCP tool cluster:

1. **Bedrock foundation model:** No visibility into training data, alignment tuning, or version update policy. An unannounced model version change could alter recommendation quality silently.
2. **LangSmith:** Third-party SaaS processing sensitive financial trace data. Data residency, breach notification, and access control terms unreviewed.
3. **External fraud/identity APIs:** These are called by MCP tools during live underwriting. If a fraud API provider is compromised, returns tampered scores, or becomes unavailable, the agent will either generate recommendations based on bad data or fail silently.

**Current gap:** No supplier inventory. No contracts reviewed for AI-specific provisions. No fallback logic if fraud/identity API returns an error.

**Required controls:**
- Inventory all external dependencies with version, provider, contract status, and criticality rating
- Bedrock model version pinned — version updates require formal change approval
- LangSmith supplier assessment: data residency, DPA, incident notification terms
- External fraud/identity API: SLA defined, fallback to manual fraud check if API unavailable, data handling reviewed under GDPR Article 28

---

### LLM04 — Data and Model Poisoning

**Applicability:** `✓ AUA-MCP` · `~ AUA-LLM`

**How it applies:**  
Since AutoUnderwriter Agent uses retrieval and tool-based grounding rather than fine-tuning, the poisoning vector is the **data the tools return**, not the model weights:

1. **Policy repository poisoning:** If an attacker gains write access to the S3 policy store, they can modify lending policy rules that the agent retrieves and applies to cases — causing it to make recommendations that violate current policy while appearing correctly grounded.
2. **Aurora data manipulation:** If the affordability scoring tool queries Aurora PostgreSQL and an attacker has modified underlying customer financial data, the agent will produce recommendations based on tampered inputs.
3. **Document store contamination:** Malicious documents injected into the S3 document store could be retrieved for legitimate cases and corrupt the recommendation.

**Current gap:** Write-access controls for S3 policy store and Aurora are not reviewed. No audit trail for policy document changes. No DSPM to detect anomalous data modifications.

**Required controls:**
- Immutable audit log for all changes to the S3 policy store and policy documents
- Principle of least privilege on Aurora write access — the MCP affordability tool should be read-only
- S3 versioning enabled on the policy and document stores — all changes reversible and auditable
- DSPM tooling to detect unexpected writes to policy and document stores

---

### LLM05 — Improper Output Handling

**Applicability:** `✓ AUA-ORCH` · `✓ AUA-LLM` · `~ AUA-WF`

**How it applies:**  
The agent's output is a recommendation pack consumed by the underwriter workbench. Two output-handling risks exist:

1. **MCP tool parameter injection:** If the agent constructs MCP tool call parameters directly from unvalidated model output (e.g., uses a model-generated case reference to query Aurora), unsanitised output could become a SQL injection or parameter manipulation vector at the tool layer.
2. **Workbench rendering:** If the recommendation pack includes model-generated text that is rendered by the underwriting workbench without escaping, adversarial content in the output could manipulate the workbench UI or inject instructions into other workbench integrations.

**Current gap:** No documented output validation before MCP tool parameter construction or workbench rendering.

**Required controls:**
- Never construct MCP tool query parameters directly from raw model output — use typed, schema-validated parameter construction
- Sanitise all model-generated text before rendering in the underwriting workbench
- Test for injection via adversarial model outputs in the security test suite

---

### LLM06 — Excessive Agency

**Applicability:** `✓ AUA-ORCH` · `✓ AUA-WF` · `✓ AUA-MCP`

**This is the primary OWASP risk for AutoUnderwriter Agent.**

**How it applies:**  
AutoUnderwriter Agent was designed with a clear intent: gather data, score affordability, and prepare a recommendation pack for human approval. But the agent's real-world authority is the product of:

- The tools it can invoke (affordability, fraud, identity, policy, document retrieval, case summarisation)
- The data those tools can access (Aurora PostgreSQL, S3, external APIs, case management)
- The parameters it can construct for those tool calls (potentially arbitrary case references)
- The number of tool-call steps it can chain in a single session (no documented maximum)

This creates a gap between the **intended agency** (prepare one recommendation pack per submitted case) and the **possible agency** (potentially access broad customer records, invoke external identity queries for arbitrary individuals, chain arbitrary numbers of tool calls). The gap widens each time a new MCP tool is added without a governance review — this is what the HLD calls "emergent capability creep."

**Current gap:** No MCP permission matrix. No maximum tool-chain length defined. No session-scoped authorisation. Tool additions not subject to formal governance review.

**Required controls:**
- Publish and enforce an MCP permission matrix: each tool listed with permitted scope, permitted parameters, and maximum call frequency per session
- Implement a hard maximum on tool-chain length per agent session at the Step Functions level — if exceeded, the session is terminated and escalated
- Session-scoped authorisation at the MCP server: tool calls bound to the submitted case ID — no cross-case data access
- Require formal governance sign-off (Chief Credit Officer + CISO) for any new MCP tool addition
- Quarterly review of the MCP tool inventory against the permission matrix — check for scope drift

---

### LLM07 — System Prompt Leakage

**Applicability:** `✓ AUA-ORCH` · `✓ AUA-LLM`

**How it applies:**  
The AutoUnderwriter Agent system prompt contains the agent's operating instructions, tool-use logic, decision criteria, and policy interpretation rules. If an attacker extracts this prompt (via a crafted case submission or rogue insider), they gain a precise map of how to manipulate the agent's recommendations.

**Current gap:** No prompt protection controls documented. Prompt templates likely stored in code or S3 without access restriction.

**Required controls:**
- System prompt treated as sensitive configuration — stored in AWS Secrets Manager or SSM Parameter Store, not in code or plain S3
- Explicitly instruct the model not to reproduce system prompt content in its outputs
- Include system prompt extraction in the red-team test suite

---

### LLM08 — Vector and Embedding Weaknesses

**Applicability:** `~ AUA-MCP` · `~ AUA-LLM`

**How it applies:**  
AutoUnderwriter Agent uses document retrieval and policy lookup tools rather than a dedicated vector store, so this risk is lower than for a RAG-first system. However, if the policy retrieval or document retrieval tools use semantic similarity search, the embedding store becomes relevant.

**Current gap:** Retrieval mechanism for policy and document tools not fully described in HLD — may include semantic search components.

**Required controls:**
- Confirm whether any MCP tool uses a vector/embedding index for retrieval — if so, apply the same controls as LAC-RAG in the LumaAssist Chat mapping
- Restrict write access to any embedding index to a controlled ingestion pipeline

---

### LLM09 — Misinformation

**Applicability:** `✓ AUA-LLM` · `✓ AUA-MCP`

**How it applies:**  
For AutoUnderwriter Agent, misinformation takes a specific and severe form: the agent produces a recommendation pack that contains fabricated or inaccurate evidence — case data it did not actually retrieve, affordability conclusions not supported by the tool output, or policy citations that do not exist. This is not a quality issue: it is a fraud enablement and regulatory breach risk.

1. **Fabricated evidence bundle:** The model may "hallucinate" supporting evidence in the recommendation pack if tool output is sparse or ambiguous, creating a record that looks complete but is not grounded.
2. **Policy misapplication:** The model may misinterpret retrieved policy rules, applying the wrong policy to a case, or combining incompatible policy clauses.
3. **Confidence without basis:** The recommendation pack may present a high-confidence recommendation without any mechanism to surface that the underlying tool outputs were incomplete or low-quality.

**Current gap:** No hallucination evaluation for the recommendation pack. No completeness check confirming that every recommendation claim is traceable to a specific tool output.

**Required controls:**
- Structured explainability output: the recommendation pack must include a citation for each material claim pointing to the specific tool output that supports it
- Confidence scoring: the agent must flag when tool outputs are incomplete, inconsistent, or missing — and surface this prominently in the recommendation pack for the underwriter
- Regular case-sample review: human auditors verify a sample of recommendation packs against underlying tool outputs
- Formal hallucination evaluation as part of the pre-deployment gate for any agent or prompt update

---

### LLM10 — Unbounded Consumption

**Applicability:** `✓ AUA-ORCH` · `✓ AUA-WF` · `✓ AUA-LLM` · `~ AUA-MCP`

**How it applies:**  
1. **Runaway tool chains:** An agent session with no maximum tool-call limit could enter a reasoning loop that makes hundreds of MCP calls — exhausting API quotas, overwhelming Aurora, and consuming significant Bedrock tokens.
2. **Adversarial cost attack:** An attacker submitting large documents or complex cases at high volume can drive Bedrock inference costs and Step Functions execution costs to significant levels.
3. **Queue saturation:** Malicious or runaway agent sessions can fill the underwriting queue and block legitimate cases.

**Current gap:** No maximum tool-call limit per session. No rate limiting on case submission API. No Bedrock cost anomaly alerting.

**Required controls:**
- Hard maximum on tool-call steps per session enforced in Step Functions (terminate and escalate if exceeded)
- Rate limiting at API Gateway: maximum case submissions per underwriter account per hour
- Bedrock token budget and cost anomaly alerting in AWS Cost Explorer
- Step Functions concurrency limit configured with queue overflow alerting

---

## 6. ISO/IEC 42001 Mapping

ISO/IEC 42001 is the AI management system (AIMS) standard. It applies the management-system model (Plan–Do–Check–Act) to AI governance. For AutoUnderwriter Agent, it is the framework that most directly governs the organisational processes that must surround the system — not just the technical controls.

**Important context:** ISO/IEC 42001 is an organisational standard, not a system-level standard. The mapping below applies the standard's requirements to the AutoUnderwriter Agent as a specific AI system within LumaPay's overall AIMS. Many of the gaps identified are organisation-wide gaps that happen to be most acute for AutoUnderwriter Agent because of its decision criticality.

---

### Clause 4 — Context of the Organisation

| Requirement | Relevance to AutoUnderwriter Agent | Current State | Required State |
|---|---|---|---|
| 4.1 — Understand the organisation and its context | Identify internal and external factors affecting AutoUnderwriter Agent: FCA regulation, Consumer Duty, GDPR, customer expectations, competitive environment | Not formally documented for AutoUnderwriter Agent | Context analysis completed; FCA, Consumer Duty, and GDPR obligations explicitly mapped to agent design and operation |
| 4.2 — Understand interested parties | Identify stakeholders: customers (lending applicants), underwriters, FCA, ICO, Nordhaven Group Risk Committee, LumaPay board | Not documented | Stakeholder register maintained; each stakeholder's AI-related requirements captured |
| 4.3 — AIMS scope | Define the boundary of the AI management system as it applies to AutoUnderwriter Agent | No AIMS exists at LumaPay | AIMS scope defined to include all four AI applications; AutoUnderwriter Agent classified as highest-criticality |

---

### Clause 5 — Leadership

| Requirement | Relevance to AutoUnderwriter Agent | Current State | Required State |
|---|---|---|---|
| 5.1 — Leadership and commitment | Top management (LumaPay board / Nordhaven Group Risk Committee) demonstrates commitment to responsible AI management for high-criticality systems | No board-level AI governance structure documented | Board-level AI risk ownership confirmed; Group Risk Committee receives quarterly AI risk reports |
| 5.2 — AI policy | An AI policy exists that governs AutoUnderwriter Agent's purpose, boundaries, and principles | No AI policy at LumaPay | AI policy published covering: permitted use cases, prohibited agent actions, human oversight requirements, and data handling principles |
| 5.3 — Roles and responsibilities | Roles formally assigned with accountability | Named in HLD but not formally appointed | Accountable executive (Chief Credit Officer), technical owner, risk owner, and data owner formally appointed with documented responsibilities |

**Gap assessment:** Leadership commitment and AI policy are foundational ISO 42001 requirements. Their absence means no other clause can be effectively implemented. This is a governance prerequisite for the Nordhaven integration.

---

### Clause 6 — Planning

| Requirement | Relevance to AutoUnderwriter Agent | Current State | Required State |
|---|---|---|---|
| 6.1.1 — AI risk assessment process | A documented process exists to identify, analyse, and evaluate AI-specific risks for AutoUnderwriter Agent | No formal AI risk assessment process | AI risk assessment completed using the NIST AI RMF risk register approach (see Section 3.3 above); reviewed annually and after material changes |
| 6.1.2 — AI impact assessment | Assessment of potential impacts on individuals: customers denied credit, customers approved for unsuitable lending | Not conducted | AI impact assessment completed covering: decision fairness, customer harm scenarios, Consumer Duty implications, and GDPR Article 22 profiling obligations |
| 6.1.4 — Risk treatment | Risk treatment plan for identified AI risks | Not documented | Risk treatment plan published (aligns to NIST AI RMF MANAGE actions in Section 3.4) |
| 6.2 — AI objectives | Measurable objectives defined for the system | Not defined | Objectives defined and tracked: recommendation accuracy rate, underwriter override rate, time-to-decision, KRI thresholds (see Section 3.3) |

---

### Clause 7 — Support

| Requirement | Relevance to AutoUnderwriter Agent | Current State | Required State |
|---|---|---|---|
| 7.1 — Resources | Adequate human and infrastructure resources to manage AutoUnderwriter Agent safely | Thin platform team (5 people); no security or GRC function | Minimum viable governance team defined for integration period; resource gap formally accepted and tracked by board |
| 7.2 — Competence | Individuals operating the agent (engineers, underwriters, risk managers) are competent in its capabilities and risks | No AI-specific training documented | Competency requirements defined for each role; training delivered and recorded before individuals interact with the agent |
| 7.3 — Awareness | All relevant staff aware of the AI policy, the agent's limitations, and their responsibilities | No awareness programme | Awareness communication sent to all underwriters and supporting staff; refreshed annually |
| 7.4 — Communication | Process for communicating AI-related information to internal and external stakeholders | No process | Communication plan covers: underwriter operational guidance, FCA/ICO notification procedures, customer-facing transparency statements |
| 7.5 — Documented information | Required documentation created, controlled, and retained | Partial documentation in HLD; no formal document control | Document inventory maintained for: AI policy, risk assessment, impact assessment, MCP permission matrix, override records, evaluation results, incident logs |

---

### Clause 8 — Operation

This is the most technically substantive clause for AutoUnderwriter Agent — it governs the AI system lifecycle.

| Requirement | Relevance to AutoUnderwriter Agent | Current State | Required State |
|---|---|---|---|
| 8.1 — Operational planning and control | Planned and controlled processes for agent operation: case intake, tool invocation, recommendation generation, human review | Informal — dependent on engineer knowledge | Operational procedures documented: intake criteria, tool invocation rules, session limits, HITL requirements, escalation triggers |
| 8.2 — AI risk assessment (operational) | Risk assessment performed before deploying changes (new tools, prompt updates, workflow changes) | No pre-deployment risk assessment process | Stage-gate change process: every agent change requires risk assessment sign-off before deployment |
| 8.3 — AI impact assessment (operational) | Impact assessment updated when system changes materially | Not conducted | Impact assessment reviewed and updated with every major agent change |
| 8.4 — AI system design and development | Design requirements, constraints, and testing requirements documented and followed | Partial — HLD exists; no formal design requirements documentation | Design requirements document (DRD) published covering: scope constraints, tool permission model, session limits, HITL boundaries, explainability requirements |
| 8.5 — Data for AI systems | Data used in the agent (documents, financial data, policy rules) managed with quality, provenance, and access controls | No data management documentation; unredacted PII in test | Data management plan covering: document ingestion controls, policy store versioning, test-environment data rules, retention and deletion |
| 8.6 — System documentation | Technical documentation sufficient for audit and regulatory review | HLD exists; insufficient for regulatory audit | Full system documentation package: architecture diagram, data flows, tool inventory, permission matrix, evaluation results, incident log |
| 8.7 — Information for interested parties | Users and deployers (underwriters) given information to use the agent safely and understand its limitations | Not documented | Underwriter guidance document: what the recommendation pack contains, what it does not contain, how to challenge it, and when to escalate |

---

### Clause 9 — Performance Evaluation

| Requirement | Relevance to AutoUnderwriter Agent | Current State | Required State |
|---|---|---|---|
| 9.1 — Monitoring, measurement, and evaluation | KRIs defined and measured for AutoUnderwriter Agent; performance reviewed against objectives | No monitoring framework documented | KRI dashboard operational (see Section 3.3); monthly review by AI Risk Forum; quarterly report to Group Risk Committee |
| 9.2 — Internal audit | Periodic internal audit of AutoUnderwriter Agent against AIMS requirements | No internal audit function for AI | Bi-annual internal audit of AutoUnderwriter Agent; findings reported to board; corrective actions tracked |
| 9.3 — Management review | Management reviews AutoUnderwriter Agent performance, risk posture, and control effectiveness | No management review process | Annual management review: performance vs objectives, risk register review, control effectiveness, and resource adequacy |

---

### Clause 10 — Improvement

| Requirement | Relevance to AutoUnderwriter Agent | Current State | Required State |
|---|---|---|---|
| 10.1 — Continual improvement | Processes in place to improve AIMS effectiveness over time | Not established | Quarterly improvement cycle: review KRIs, incorporate incident lessons, update risk assessments |
| 10.2 — Nonconformity and corrective action | Process to identify, document, and correct nonconformities (deviations from requirements) | No formal nonconformity process | Nonconformity log maintained; corrective action owners assigned; closure verified before sign-off |

#### Annex A — Organisational Controls Relevant to AutoUnderwriter Agent

ISO/IEC 42001 Annex A provides an AI-specific control set. The highest-priority controls for AutoUnderwriter Agent are:

| Annex A Control | Relevance | Gap |
|---|---|---|
| A.2.2 — AI policy | AI policy covering AutoUnderwriter Agent scope and principles | Absent |
| A.3.2 — Roles and responsibilities | Formal accountability matrix for the agent | Absent |
| A.4.3 — Assessment of AI systems | Formal risk and impact assessment process | Absent |
| A.5.1 — AI system lifecycle | Defined and controlled lifecycle for agent design, build, test, deploy, monitor, retire | Partial — HLD exists; no lifecycle governance |
| A.5.2 — Documentation of AI system | Complete system documentation available for audit | Partial |
| A.5.3 — Logging of AI system activities | All agent sessions, tool calls, and recommendations logged and retained | Partial — tools in place; retention and access policies absent |
| A.6.1 — Data governance | Data used by the agent managed with quality, provenance, and privacy controls | Absent |
| A.6.2 — Data acquisition and preparation | Controls on how financial documents and customer data enter the agent | Absent |
| A.8 — Use of AI by the organisation | Controls on how underwriters interact with agent output; guidance on appropriate reliance | Absent |
| A.9.1 — Third-party AI relationships | Governance of Bedrock, LangSmith, and external fraud/identity APIs | Absent |

---

## 7. Cross-Framework Risk Summary

The table below consolidates the highest-priority risks across all four frameworks. Risks that appear across multiple frameworks simultaneously represent the most urgent priorities for the Nordhaven 100-day plan.

| Risk | NIST AI RMF | MITRE ATLAS | OWASP LLM | ISO 42001 | Components | Severity |
|---|---|---|---|---|---|---|
| Document-based prompt injection | MAP.3, MANAGE | AML.T0051, AML.T0043 | LLM01 | A.5.1, A.6.2 | `AUA-MCP` `AUA-LLM` | **Critical** |
| Excessive MCP tool agency / permission overreach | GOVERN GV.1, MANAGE | AML.T0031 | LLM06 | A.2.2, A.5.1 | `AUA-MCP` `AUA-WF` | **Critical** |
| Recommendation traceability gap | GOVERN GV.2, MEASURE | AML.T0048 | LLM09 | A.5.2, A.5.3 | `AUA-LLM` `AUA-HITL` | **Critical** |
| Unredacted PII in `test` | MANAGE | AML.T0037 | LLM02 | A.6.1, A.6.2 | `AUA-ORCH` `AUA-MCP` | **Critical** |
| Human override fatigue — nominal HITL | GOVERN GV.2, MEASURE | AML.T0048 | LLM09 | A.8, Clause 5 | `AUA-HITL` | **Critical** |
| No AI governance, policy, or accountability structure | GOVERN (all) | — | — | Clause 5, A.2.2, A.3.2 | All | **Critical** |
| Cross-border trace retention (LangSmith) | MAP.3, MANAGE | AML.T0037 | LLM02, LLM03 | A.6.1, A.9.1 | `AUA-ORCH` `AUA-LLM` | **High** |
| Supply chain — Bedrock version, LangSmith, fraud APIs | MAP.5, MANAGE | AML.T0005 | LLM03 | A.9.1 | `AUA-LLM` `AUA-MCP` | **High** |
| Emergent capability creep — tool additions without governance | GOVERN GV.1, MAP | AML.T0013 | LLM06 | A.5.1, Clause 6 | `AUA-MCP` `AUA-WF` | **High** |
| Tool-chain dependency failure — silent partial output | MAP.3, MEASURE | AML.T0029 | LLM07, LLM10 | A.5.1, Clause 9 | `AUA-WF` `AUA-MCP` | **High** |
| IAM privilege — over-privileged roles | MAP.3, MANAGE | AML.T0012, AML.T0036 | LLM06 | A.5.1 | `AUA-ORCH` `AUA-MCP` | **High** |
| Policy store / document store poisoning | MAP.3 | AML.T0020 | LLM04 | A.6.1, A.6.2 | `AUA-MCP` | **Medium** |
| Unbounded session consumption | MANAGE | AML.T0029 | LLM10 | A.5.1 | `AUA-ORCH` `AUA-WF` | **Medium** |

---

## 8. Matrix Feed — Framework Applicability Matrix Cells

These ratings feed directly into `04-risk-and-controls/framework-applicability-matrix.md`.

### OWASP LLM Top 10 — AutoUnderwriter Agent Components

| OWASP Risk | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL |
|---|---|---|---|---|---|
| LLM01 Prompt Injection | ✓ | ✓ | ✓ | ✓ | |
| LLM02 Sensitive Information Disclosure | ✓ | ~ | ✓ | ✓ | |
| LLM03 Supply Chain | ~ | ~ | ✓ | ✓ | |
| LLM04 Data and Model Poisoning | | ~ | ~ | ✓ | |
| LLM05 Improper Output Handling | ✓ | ✓ | ✓ | ~ | |
| LLM06 Excessive Agency | ✓ | ✓ | | ✓ | |
| LLM07 System Prompt Leakage | ✓ | | ✓ | | |
| LLM08 Vector and Embedding Weaknesses | | | ~ | ~ | |
| LLM09 Misinformation | | | ✓ | ✓ | ~ |
| LLM10 Unbounded Consumption | ✓ | ✓ | ✓ | ~ | |

### NIST AI RMF — AutoUnderwriter Agent Components

| NIST AI RMF Function | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL |
|---|---|---|---|---|---|
| GOVERN | ✓ | ✓ | ✓ | ✓ | ✓ |
| MAP | ✓ | ✓ | ✓ | ✓ | ✓ |
| MEASURE | ✓ | ✓ | ✓ | ✓ | ✓ |
| MANAGE | ✓ | ✓ | ✓ | ✓ | ✓ |

### ISO/IEC 42001 — AutoUnderwriter Agent Components

| ISO 42001 Clause / Annex A | AUA-ORCH | AUA-WF | AUA-LLM | AUA-MCP | AUA-HITL |
|---|---|---|---|---|---|
| Clause 5 — Leadership and policy | ✓ | | ✓ | | ✓ |
| Clause 6 — Planning and risk assessment | ✓ | ✓ | ✓ | ✓ | ✓ |
| Clause 7 — Support (resources, competence) | ✓ | | | ✓ | ✓ |
| Clause 8 — Operation and lifecycle | ✓ | ✓ | ✓ | ✓ | ✓ |
| Clause 9 — Performance evaluation | ✓ | ✓ | ✓ | ✓ | ✓ |
| Clause 10 — Improvement | ✓ | ✓ | ✓ | ✓ | ✓ |
| A.5.1 — AI system lifecycle | ✓ | ✓ | ✓ | ✓ | ✓ |
| A.5.3 — Logging | ✓ | ✓ | ✓ | ✓ | ~ |
| A.6.1 — Data governance | ~ | | ✓ | ✓ | |
| A.8 — Use of AI by organisation | | | | | ✓ |
| A.9.1 — Third-party relationships | | | ✓ | ✓ | |

---

## 9. Artefacts Required for Due Diligence

| Artefact | Framework Relevance | Status |
|---|---|---|
| Agent design document: permitted scope, tool list, maximum tool-chain length | NIST GOVERN · ISO Clause 8 · LLM06 | Not confirmed to exist |
| MCP tool inventory and permission matrix | NIST MAP · LLM06 · ISO A.5.1 | Not confirmed to exist |
| Document ingestion controls: pre-processing pipeline, injection detection approach | LLM01 · MITRE AML.T0051 · ISO A.6.2 | Not confirmed to exist |
| Structured explainability output specification for recommendation pack | NIST MEASURE · ISO A.5.2 · LLM09 | Not confirmed to exist |
| Override rate data: last 12 months, trend, anomaly notes | NIST MEASURE · ISO Clause 9 | Not confirmed to exist |
| LangSmith trace policy: access controls, data residency, retention, deletion | LLM02 · MITRE AML.T0037 · ISO A.6.1 | Not confirmed to exist |
| IAM role definitions: orchestrator, MCP service accounts, Step Functions execution role | LLM06 · MITRE AML.T0012 · NIST MANAGE | Not confirmed to exist |
| Evaluation results: recommendation accuracy, hallucination rate, tool-chain testing | NIST MEASURE · LLM09 · ISO Clause 9 | Not confirmed to exist |
| Supplier assessments: Bedrock, LangSmith, external fraud/identity API providers | LLM03 · ISO A.9.1 · NIST MAP.5 | Not confirmed to exist |
| Evidence of test-environment data masking | LLM02 · NIST MANAGE · GDPR | Confirmed absent — live PII in test |
| Incident playbooks for AI-specific events | NIST MANAGE · ISO Clause 10 | Not confirmed to exist |

---

*This document is part of the Nordhaven–LumaPay AI Risk Taskforce deliverable set. The next mapping will cover LumaCredit-EU. All findings feed into the master Framework Applicability Matrix at `04-risk-and-controls/framework-applicability-matrix.md` and the risk register at `04-risk-and-controls/risk-register-template.md`.*
