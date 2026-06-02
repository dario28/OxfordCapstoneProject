# LumaCredit-EU — Framework Mapping
## EU AI Act · ISO/IEC 42001 · ISO/IEC 5259 · NIST AI RMF

**Document status:** Draft v1.0  
**Prepared by:** Nordhaven–LumaPay AI Risk Taskforce  
**Role context:** Amrik Randhawa 
**Date:** 2026-05-29  


---

## 1. Purpose and Scope

This document maps LumaCredit-EU against four frameworks with a deliberate order: EU AI Act first, because it sets the hard legal obligations that all other frameworks support; ISO/IEC 42001 second, because it provides the management system to operationalise compliance; ISO/IEC 5259 third, because data quality is the foundational technical requirement for a credit-scoring system; and NIST AI RMF last, as the integrating governance lens that translates all findings into action.

The mapping is performed at the component level using the four LumaCredit-EU components defined in the Framework Applicability Matrix:

| Component ID | Description |
|---|---|
| `LCEU-API` | Decision API and ECS decision service — intake, orchestration, third-party API calls, output dispatch |
| `LCEU-DATA` | Feature pipeline, Aurora PostgreSQL, S3 feature store and data lake — data transformation, storage, lineage |
| `LCEU-MODEL` | Amazon SageMaker model endpoint — inference, scoring, model artefacts |
| `LCEU-RULES` | Rules engine on ECS — policy layer, approve/decline/refer logic, manual review queue |

---

## 2. System Snapshot — The Regulatory Stakes

LumaCredit-EU is the highest-stakes system in the LumaPay estate from a regulatory compliance standpoint. Four facts define its exposure:

| Fact | Regulatory Consequence |
|---|---|
| **EU AI Act Annex III, point 5(b)** — AI system used to evaluate the creditworthiness of natural persons and establish credit scores | LumaPay is a **provider** of a **high-risk AI system** under EU AI Act. The full obligations of Articles 9–17 apply before the system can be placed on the market or put into service |
| **GDPR Article 22** — automated decisions with legal or similarly significant effects | Credit approval and denial constitute significant effects; Article 22 safeguards apply unless an exemption is properly established; a DPIA is likely mandatory |
| **FCA Consumer Duty** — fair outcomes for retail customers across BNPL and lending | Biased, unexplainable, or drifting credit decisions are not just technical failures — they are regulatory breaches causing concrete customer harm |
| **Substrate properties: opacity + drift + dependency** | The model is a black box (opacity), its performance degrades over time without detection (drift), and its inputs rely on third-party bureau and credit APIs it does not control (dependency) |
| **No documentation, no lineage, no validation evidence** | LumaPay cannot currently demonstrate compliance with any of the above. The Nordhaven acquisition means Nordhaven inherits this liability from day one of close |

**The core finding before any framework analysis begins:** LumaCredit-EU is making high-risk credit decisions affecting EU natural persons without the governance infrastructure required by law. This is not a maturity gap — it is a legal exposure that must be treated as a pre-close critical risk.

---

## 3. EU AI Act Mapping

### 3.1 Classification — High-Risk AI Under Annex III

Before applying any Articles, the classification must be formally confirmed and documented.

**Applicable provision:** EU AI Act Annex III, Section 5(b)

> *AI systems intended to be used to evaluate the creditworthiness of natural persons or establish their credit score, with the exception of AI systems used for the purpose of detecting financial fraud.*

**Classification determination for LumaCredit-EU:**

| Classification criterion | Assessment |
|---|---|
| Does the system evaluate creditworthiness of natural persons? | **Yes** — BNPL and SME lending eligibility for individual customers |
| Does it establish a credit score? | **Yes** — SageMaker model returns a credit score used in the approve/decline/refer decision |
| Is it intended for the EU market? | **Yes** — explicit EU legal entity and EU lending operations |
| Does it fall within the fraud-detection exception? | **No** — LumaCredit-EU is the credit-scoring function, not the fraud-detection function (FraudShield is separate) |

**Verdict: LumaCredit-EU is unambiguously a high-risk AI system under EU AI Act Annex III, Section 5(b).**

This means LumaPay, as the entity that develops and deploys LumaCredit-EU, is a **provider** under Article 3(3) and bears the full obligations of Chapter III, Section 2 (Articles 9–17).

**Current state:** Classification has not been formally confirmed or documented. There is no conformity assessment, no CE marking process initiated, and no EU AI Act compliance programme in place.

---

### 3.2 Article 9 — Risk Management System

**Requirement:** Providers must establish, implement, document, and maintain a risk management system throughout the entire lifecycle of the high-risk AI system. The system must identify, analyse, and estimate known and foreseeable risks; evaluate risks that may emerge post-market; adopt appropriate risk management measures; and test the system for the purpose of identifying the most appropriate risk management measures.

**Mapping to LumaCredit-EU:**

| Article 9 Obligation | Requirement | Current State | Required State |
|---|---|---|---|
| 9.1 — Lifecycle risk management system | Documented, iterative process covering design through decommission | Absent | Formal risk management programme for LumaCredit-EU; reviewed at each model or rule change |
| 9.2(a) — Identify and analyse known risks | Risk enumeration for each component and data flow | Partial risk list exists in `04-risk-and-controls`; not formally linked to Article 9 | Risk register for LumaCredit-EU formally approved and maintained under Article 9 |
| 9.2(b) — Estimate foreseeable risks | Reasonably foreseeable misuse scenarios and edge cases documented | Not documented | Misuse analysis completed: applicant gaming the model, bureau data failure, drift-induced bias, third-party manipulation |
| 9.4 — Risk management measures | Measures adopted to address identified risks; residual risks evaluated | No formal risk treatment documented | Risk treatment plan published; residual risks accepted by Head of Lending and reviewed by board |
| 9.6 — Testing to identify appropriate measures | System tested before market placement; testing regime documented | No test regime documented | Pre-deployment testing protocol: model validation, adversarial input testing, fairness assessment, bias screening |
| 9.7 — Serious incident feedback loop | Testing incorporates feedback from serious incidents and post-market monitoring | No incident feedback mechanism | Incident review process feeds into the next model validation cycle |

**Gap assessment:** No risk management system exists. This is a hard legal requirement under Article 9 — without it, LumaCredit-EU cannot lawfully remain in service under EU AI Act obligations.

---

### 3.3 Article 10 — Data and Data Governance

**Requirement:** Training, validation, and testing datasets must be subject to appropriate data governance and management practices. Data must be relevant, sufficiently representative, free of errors to the extent possible, and complete with regard to the intended purpose. Datasets must be examined for possible biases. Personal data used only where strictly necessary.

This is the article where ISO/IEC 5259 directly reinforces EU AI Act obligations — see Section 5 for the detailed ISO 5259 mapping.

| Article 10 Obligation | Requirement | Current State | Required State |
|---|---|---|---|
| 10.2(a) — Design choices | Data design choices documented including relevant feature categories, labelling criteria, and exclusion decisions | Not documented | Feature selection rationale, label definitions, and exclusion decisions documented and version-controlled |
| 10.2(b) — Data collection | Data collection processes described: source systems, third-party bureaux, open-banking providers | Partial — systems described in HLD; no formal data collection specification | Data collection specification covering all sources: internal Aurora data, third-party bureau APIs, open-banking feeds, device signals |
| 10.2(c) — Data preparation | Pre-processing, cleaning, enrichment, and transformation steps documented | Not documented | Feature pipeline documented with step-by-step transformation logic; every transformation versioned |
| 10.2(d) — Assumptions about collected data | Documented assumptions about what the data represents and its limitations | Not documented | Data assumptions register: what each feature measures, known limitations, and relevance to creditworthiness |
| 10.2(e) — Assessment of data availability, quantity, and suitability | Data sufficiency assessment performed before training | Not confirmed | Formal data sufficiency assessment: volume, recency, representativeness, and suitability for the UK/EU lending population |
| 10.2(f) — Examination for biases | Training and validation data examined for potential bias across protected characteristics | Not confirmed | Bias audit of training dataset; protected characteristics cross-tabulated against approval rates; findings documented |
| 10.2(g) — Identify data gaps | Gaps in datasets relevant to foreseeable uses of the system identified and addressed | Not confirmed | Data gap analysis: identify underrepresented populations; document whether model performance is validated across those segments |
| 10.5 — Special category data | Special categories of personal data used only where strictly necessary and with additional safeguards | Unknown — open-banking data may contain health or financial difficulty signals | Audit of all input features for special category data; document necessity basis; remove features that cannot be justified |
| 10.6 — Lower-environment data | Appropriate measures for personal data used in test and validation | **Confirmed gap** — unredacted PII copied into `test` | Immediate: halt further copying; remediation: tokenise or synthesise test datasets; permanent: synthetic data pipeline |

**Gap assessment:** Essentially all Article 10 obligations are unmet. This means the foundation of the high-risk AI compliance case — demonstrating that the model was built on appropriate, representative, bias-examined data — cannot currently be made.

---

### 3.4 Article 11 — Technical Documentation

**Requirement:** Providers must draw up technical documentation before placing a high-risk AI system on the market. The documentation must demonstrate compliance with the requirements and provide authorities with the information needed to assess compliance. Annex IV specifies the minimum content.

**Annex IV minimum content — gap assessment for LumaCredit-EU:**

| Annex IV Element | Requirement | Current State |
|---|---|---|
| 1. General description | Purpose, context, version, intended geography, intended users | Partial — HLD captures this at high level; no formal technical document |
| 2. Description of elements and development process | Architecture, components, training and validation approach, algorithms used | Partial — HLD exists; no development process documentation |
| 3. Monitoring, functioning, and control | Monitoring approach, performance thresholds, output interpretation | Partial — monitoring tools described; no thresholds or interpretation guidance |
| 4. Description of changes through the system's lifecycle | Version history, change log, validation evidence per change | Not documented |
| 5. Risk management system description | Reference to Article 9 documentation | Absent |
| 6. Description of post-market monitoring system | How the provider monitors performance after deployment | Absent |
| 7. Relevant standards applied | Which harmonised standards or common specifications applied | Not documented |

**Required state:** A formal Annex IV technical documentation package must be prepared and maintained. This is a pre-market obligation — LumaCredit-EU should not be in live service without it.

---

### 3.5 Article 12 — Record-Keeping

**Requirement:** High-risk AI systems must be capable of automatically recording events (logs) relevant to ensuring traceability throughout the system's lifecycle. Logs must include the period of operation, reference data used, input data that led to decisions, and where applicable, the identity of the persons involved.

| Article 12 Obligation | Requirement | Current State | Required State |
|---|---|---|---|
| 12.1 — Automatic event logging | System capable of recording events; logging built into the system design | Partial — CloudWatch and CloudTrail in place; no AI-specific event logging spec | AI-specific logging specification: every decision event records model version, feature values, score, policy outcome, reason codes, and timestamp |
| 12.2 — Traceability throughout lifecycle | Logs enable reconstruction of the decision-making process for any given case | Not confirmed — decision logs exist in Aurora but completeness and format unreviewed | Complete decision audit trail in Aurora: every decision reconstructable from stored inputs, model version, and rules state |
| 12.3(a) — Duration of operation | Each operational session logged with start and end timestamps | Not confirmed | Session-level logging confirmed and validated |
| 12.3(b) — Reference database used | The dataset or model version used for each inference recorded | Not confirmed | Model version recorded with every inference event; version transitions logged with timestamps |
| 12.3(c) — Input data | Input data that led to each output recorded or at minimum retrievable | Not confirmed | Input feature vector (post-transformation) recorded per decision; raw input reference stored for audit reconstruction |

**Gap assessment:** The logging infrastructure exists but has not been configured, validated, or specified to meet Article 12 requirements. A compliance audit could not currently use the logs to reconstruct a challenged credit decision.

---

### 3.6 Article 13 — Transparency and Provision of Information to Deployers

**Requirement:** High-risk AI systems must be designed and developed to ensure sufficient transparency to enable deployers to interpret the system's output and use it appropriately. Technical documentation must include information enabling deployers to understand the system's limitations, intended use, and performance characteristics.

| Article 13 Obligation | Requirement | Current State | Required State |
|---|---|---|---|
| 13.1 — Sufficient transparency | System transparency sufficient for deployer to interpret outputs correctly | Absent — no model card, no performance summary, no limitation disclosure | Model card published: intended use, performance statistics, known limitations, contraindicated use cases |
| 13.2(a) — Identity and contact details of provider | Documented | Partial | Full provider identification documented |
| 13.2(b) — System capabilities and limitations | Documented including accuracy metrics, failure modes, and edge cases | Not documented | Capability and limitation statement covering: performance by segment, known bias risks, data dependency limitations, bureau API failure behaviour |
| 13.2(c) — Performance level | Performance metrics documented | Not confirmed | Performance metrics published: accuracy, Gini coefficient, approval rate, bad-debt rate by segment |
| 13.2(d) — Human oversight measures | Human oversight design documented and communicated to deployers | Partial — manual review queue described but not documented as a formal oversight mechanism | Human oversight document: when manual review is triggered, what the reviewer is expected to do, what constitutes an override, and how decisions are recorded |
| 13.3(b) — Reason codes | Outputs include decision-support information sufficient for the deployer to understand the basis of each decision | Not confirmed | Every decline and manual-refer decision accompanied by reason codes traceable to model features or policy rules |

---

### 3.7 Article 14 — Human Oversight

**Requirement:** High-risk AI systems must be designed and developed to allow effective oversight by natural persons. Providers must ensure that the system is designed with appropriate human-machine interface tools; deployers can effectively oversee the system; persons can intervene, override, or stop the system; and persons can identify anomalies, dysfunctions, and unexpected performance.

| Article 14 Obligation | Requirement | Current State | Required State |
|---|---|---|---|
| 14.1 — Effective oversight enabled | System designed to allow effective human oversight | Partial — manual review queue exists; no evidence that oversight is effective | Oversight effectiveness audit: verify that reviewers understand model outputs, can exercise genuine judgment, and are not rubber-stamping |
| 14.2 — Human-machine interface tools | Tools provided to allow persons assigned oversight to understand system outputs | Not documented | Dashboard or review interface that presents: score, reason codes, input feature summary, confidence indicators, and model version |
| 14.3(a) — Understand capabilities and limitations | Persons assigned oversight able to understand the system's capabilities and limitations | Not confirmed — no training or guidance documented | Mandatory training for all staff with oversight responsibility; refreshed annually and after model changes |
| 14.3(b) — Aware of automation bias | Persons aware of the tendency to over-rely on AI outputs | Not confirmed | Automation bias module included in oversight training |
| 14.3(c) — Correctly interpret outputs | Persons can correctly interpret the high-risk AI system's output | Not confirmed | Reason-code interpretation guide produced; tested in training exercises |
| 14.3(d) — Refuse, override, or abstain | Persons assigned oversight can decide to disregard, override, or reverse the output | Partial — manual review queue allows override; no formal override recording process | Override recording procedure: every override recorded with reviewer identity, rationale, and outcome; reviewed monthly by Head of Lending |
| 14.3(e) — Intervene or interrupt | Persons can intervene in real-time operation or interrupt the system | Not documented | Kill-switch procedure documented: ability to route all decisions to manual review and halt automated decisions without system outage |

---

### 3.8 Article 15 — Accuracy, Robustness, and Cybersecurity

**Requirement:** High-risk AI systems must be designed to achieve appropriate levels of accuracy, robustness, and cybersecurity throughout their lifecycle. Systems must be resilient to errors, faults, and inconsistencies. Performance must remain consistent even when facing inputs designed to fool or manipulate the system.

| Article 15 Obligation | Requirement | Current State | Required State |
|---|---|---|---|
| 15.1 — Appropriate accuracy | Performance metrics defined, measured, and maintained at appropriate levels | Not documented — no performance baseline | Performance baseline established: Gini, accuracy, approval rate, bad-debt rate; thresholds defined and breach triggers action |
| 15.2 — Resilience to errors | System resilient to errors, faults, and inconsistencies in inputs | Partial — rules engine provides a fallback path; no formal resilience testing | Fault injection testing: bureau API failure, feature pipeline error, SageMaker endpoint unavailability; resilience behaviour documented |
| 15.3 — Resilience to adversarial inputs | System resilient to inputs designed to manipulate outputs | Not tested | Adversarial testing: crafted application inputs designed to game the model; results documented |
| 15.4 — Cybersecurity | Technical and organisational measures to address cybersecurity risks specific to the AI system | Partial — CloudWatch and CloudTrail in place; no AI-specific cybersecurity controls | AI-specific cybersecurity controls: inference endpoint access control, input validation, model artefact integrity, third-party API certificate management |
| 15.5 — Fallback modes | Technical solutions for backup or fail-safe modes and hardware-software interdependencies | Partial — manual review queue exists as fallback but not formally documented | Fallback specification: what happens when SageMaker is unavailable, when bureau API fails, and when the rules engine returns an error |

---

### 3.9 Article 16 and Article 17 — Provider Obligations and Quality Management System

**Article 16** requires providers to draw up technical documentation, keep records, ensure compliance, affix CE marking (where applicable), and register the system in the EU database for high-risk AI systems.

**Article 17** requires providers to implement a quality management system covering: AI policy, risk management procedures, data governance procedures, technical documentation procedures, change management, conformity assessment procedures, complaint handling, and post-market monitoring.

| Obligation | Current State | Required State |
|---|---|---|
| Technical documentation (Art. 16(b)) | Absent | Annex IV documentation package completed before continued live operation |
| Record-keeping (Art. 16(c)) | Partial | Article 12 logging specification implemented and validated |
| Post-market monitoring plan (Art. 72) | Absent | Post-market monitoring plan: performance tracking, drift detection, complaint analysis, KRI reporting |
| EU AI Act database registration (Art. 49, Art. 71) | Not initiated | Registration in EU AI Act database before market placement |
| Quality management system (Art. 17) | Absent | QMS implemented covering: AI policy, risk management, data governance, change management, conformity assessment, post-market monitoring |

**Gap assessment:** Nordhaven, upon acquiring LumaPay, becomes accountable for a high-risk AI system that has none of its provider obligations in place. The legal exposure is immediate and material. The 100-day plan must include a formal EU AI Act remediation programme.

---

## 4. ISO/IEC 42001 Mapping

ISO/IEC 42001 provides the AI management system (AIMS) scaffolding that operationalises the EU AI Act's quality management system requirement (Article 17). The two frameworks are complementary: the EU AI Act sets the legal obligations; ISO/IEC 42001 provides the operational system to meet them. For LumaCredit-EU, the ISO 42001 mapping focuses on the lifecycle, data, and accountability requirements most relevant to a credit-scoring system.

---

### Clause 4 — Context

| Requirement | Relevance to LumaCredit-EU | Current State | Required State |
|---|---|---|---|
| 4.1 — Organisational context | External factors: FCA, EU AI Act, GDPR, ECB consumer credit guidelines, competitive lending market. Internal factors: immature governance, no GRC function, thin platform team | Not formally documented | Context analysis completed; regulatory obligations mapped to system design |
| 4.2 — Interested parties | Customers (EU and UK), FCA, EU AI Office, ICO, Nordhaven Group Risk Committee, LumaPay board, credit bureaux, merchants | Not documented | Stakeholder register maintained; each stakeholder's requirements mapped to system controls |
| 4.3 — AIMS scope | AIMS explicitly includes LumaCredit-EU as a high-risk, high-criticality system | No AIMS at LumaPay | AIMS scope defined; LumaCredit-EU classified as highest-priority system within scope |

---

### Clause 5 — Leadership

| Requirement | Relevance to LumaCredit-EU | Current State | Required State |
|---|---|---|---|
| 5.1 — Leadership commitment | Board and senior leadership demonstrate commitment to responsible AI governance for a credit-scoring system with direct customer impact | No board-level AI governance | Board-level AI risk ownership confirmed; LumaCredit-EU presented to board annually |
| 5.2 — AI policy | AI policy covers LumaCredit-EU's purpose, boundaries, fairness principles, and human oversight requirements | No AI policy | AI policy published; includes specific provisions for high-risk credit AI: fairness, explainability, human oversight, and regular review |
| 5.3 — Roles | Head of Lending formally accountable; Credit Platform Engineering Manager formally responsible; risk owner and data owner named | Named in HLD; not formally appointed | Formal accountability matrix signed off by Chief Executive and Chief Risk Officer |

---

### Clause 6 — Planning

| Requirement | Relevance to LumaCredit-EU | Current State | Required State |
|---|---|---|---|
| 6.1.1 — AI risk assessment | Documented process to assess risks for LumaCredit-EU | No formal AI risk assessment process | AI risk assessment completed and linked to EU AI Act Article 9 risk management system |
| 6.1.2 — AI impact assessment | Assessment of impacts on individuals: credit denial, pricing disadvantage, financial exclusion | Not conducted | AI impact assessment covering: fairness impacts by demographic, financial harm scenarios, GDPR Article 22 implications |
| 6.1.4 — Risk treatment | Treatment plan for identified risks | Not documented | Risk treatment plan aligned to NIST AI RMF MANAGE actions (Section 6 below) |
| 6.2 — AI objectives | Measurable objectives for the system | Not defined | Objectives defined: Gini coefficient above threshold, approval rate within policy band, bad-debt rate below threshold, override rate within expected range, zero unresolved bias findings |

---

### Clause 8 — Operation (AI Lifecycle)

This is the most technically detailed clause for LumaCredit-EU, governing the entire model lifecycle from design through post-deployment monitoring.

| Clause 8 Requirement | Relevance to LumaCredit-EU | Current State | Required State |
|---|---|---|---|
| 8.1 — Operational planning | Documented operational procedures for running LumaCredit-EU | Informal; dependent on engineer knowledge | Runbook published: model inference operations, rules engine management, bureau API operations, manual review queue management |
| 8.2 — AI risk assessment (operational) | Risk assessment performed before any model update, rules change, or data pipeline change | No pre-deployment risk assessment process | Stage-gate: all changes assessed for risk before promotion to production |
| 8.4 — AI system design and development | Design requirements, intended use, constraints, and fairness requirements documented | Partial — HLD exists; no design requirements document | Design requirements document: permitted use cases, prohibited uses, fairness constraints, explainability requirements, human oversight design |
| 8.4.3 — Verification and validation | The system is verified (built correctly) and validated (solves the right problem) before deployment | No validation record | Validation protocol: holdout dataset testing, backtesting against historical decisions, fairness testing, adversarial input testing; results documented |
| 8.4.4 — Data management | Training, validation, and operational data managed with documented controls | No data management documentation | Data management plan: source documentation, quality controls, lineage, retention, and lower-environment masking (see ISO 5259 mapping below) |
| 8.4.5 — Documentation of AI system | Complete system documentation maintained | Partial (HLD only) | Full system documentation: architecture, data flows, model card, validation results, known limitations, change history |
| 8.5 — Data for AI systems | Data governance covering all data used by the system | Absent | Data governance framework aligned to ISO 5259 (see Section 5 below) |
| 8.6 — System documentation | Documentation available for audit | Partial | Regulatory-grade documentation package: Article 11/Annex IV content, model card, validation reports, audit trail |
| 8.7 — Information for deployers/users | Underwriters and business users given information to use the system safely | Not documented | Model user guide: score interpretation, reason codes, confidence indicators, when to override, how to escalate |

---

### Clause 9 — Performance Evaluation

| Requirement | Relevance to LumaCredit-EU | Current State | Required State |
|---|---|---|---|
| 9.1 — Monitoring and evaluation | Performance KRIs defined and reviewed regularly | Partial — monitoring infrastructure exists; no thresholds or review cadence | Monthly KRI review by Head of Lending; quarterly report to Group Risk Committee; KRIs: Gini coefficient, approval rate, bad-debt rate, override rate, bureau API error rate |
| 9.2 — Internal audit | Regular audit against AIMS requirements for LumaCredit-EU | No internal audit | Annual audit of LumaCredit-EU against EU AI Act and ISO 42001 requirements |
| 9.3 — Management review | Management reviews system performance, risk posture, and evidence | No management review | Annual management review: performance vs objectives, risk register review, EU AI Act compliance status |

---

### Annex A — Control Priorities for LumaCredit-EU

| Control | Description | Gap |
|---|---|---|
| A.4.3 — Assessment of AI systems | Formal risk and impact assessment for LumaCredit-EU | Absent |
| A.5.1 — AI system lifecycle | Controlled lifecycle from design through decommission | Partial — development exists; governance absent |
| A.5.2 — AI system documentation | Complete system documentation package | Partial |
| A.5.3 — Logging | Decision event logging meeting Article 12 requirements | Partial |
| A.6.1 — Data governance | Data quality, lineage, and access controls | Absent — see ISO 5259 mapping |
| A.6.2 — Data acquisition and preparation | Controls on training and operational data intake | Absent |
| A.6.3 — Data quality | Data quality standards applied throughout lifecycle | Absent — see ISO 5259 mapping |
| A.9.1 — Third-party AI relationships | Bureau and credit-check API governance | Absent |

---

## 5. ISO/IEC 5259 Mapping

ISO/IEC 5259 is a multi-part series governing data quality for AI. For LumaCredit-EU, it is the framework that determines whether the model's training data, operational feature inputs, and bureau data meet the quality bar required for high-risk credit decisions. Poor data quality in a credit-scoring model is not just a technical concern — it is a direct compliance failure under EU AI Act Article 10.

The series comprises:
- **5259-1**: Overview and general requirements for data quality in AI
- **5259-2**: Data quality measures — the specific dimensions by which quality is assessed
- **5259-3**: Data quality management requirements and guidelines
- **5259-4**: Data quality process framework for AI

---

### 5.1 ISO/IEC 5259-1 — Overview and General Requirements

This part establishes the foundational requirements: data used for AI systems must meet quality requirements appropriate to the AI system's intended use, risk level, and potential impact on persons.

| Requirement | Relevance to LumaCredit-EU | Current State | Required State |
|---|---|---|---|
| Data quality requirements defined relative to the AI system's risk level | LumaCredit-EU is high-risk — data quality requirements must be correspondingly rigorous | Not defined | Data quality requirements specification published; requirements mapped to EU AI Act Article 10 obligations |
| Data quality requirements applied to all data categories | Training data, validation data, test data, operational feature data, and third-party bureau inputs each need quality specifications | Not documented | Quality specification for each data category: internal Aurora data, bureau API data, open-banking data, device signals |
| Data quality managed throughout the AI lifecycle | Quality requirements apply at design, development, deployment, and monitoring | Not managed | Quality checkpoints at each lifecycle stage: data collection, feature engineering, model training, validation, production monitoring |

---

### 5.2 ISO/IEC 5259-2 — Data Quality Measures

This part defines the specific quality dimensions against which data must be assessed. The following dimensions are directly relevant to LumaCredit-EU's credit-scoring function:

| Quality Dimension | Definition | Relevance to LumaCredit-EU | Current State | Required State |
|---|---|---|---|---|
| **Accuracy** | Data correctly represents the real-world values it is intended to represent | Credit scores depend on accurate income, repayment history, and identity data — inaccurate inputs produce inaccurate scores | Not measured | Accuracy measurement programme: sample validation of input features against source records; bureau data accuracy assessed against challenge outcomes |
| **Completeness** | All required data is present and no mandatory values are missing | Missing affordability or identity data can cause the model to produce unreliable scores or default to incorrect feature values | Not measured | Completeness monitoring: missing-value rates tracked per feature in production; alerts triggered when completeness falls below threshold |
| **Consistency** | Data values are consistent across systems and time periods | If bureau data, Aurora records, and open-banking signals are inconsistent for the same applicant, the model receives contradictory inputs | Not measured | Cross-source consistency checks: reconciliation rules applied between data sources before feature pipeline output |
| **Timeliness** | Data is sufficiently recent to be relevant for the decision being made | Stale bureau data or outdated income signals can cause the model to make decisions based on a customer's historical rather than current financial position | Not measured | Data freshness policy: maximum permitted age for each input source defined; stale data triggers manual review |
| **Representativeness** | Training data represents the real-world distribution of cases the model will encounter in production | If training data over-represents certain demographics or underrepresents EU-resident customers, the model will perform poorly on the groups it has seen least | Not assessed | Representativeness assessment: training data cross-tabulated against EU lending population; underrepresented segments identified and addressed |
| **Traceability / Lineage** | The origin and transformation history of data values is documented and recoverable | Required for EU AI Act Article 10 compliance; enables explanation of any individual credit decision | Absent | End-to-end data lineage: every feature value traceable from source system through feature pipeline to model input; lineage stored with decision record |
| **Relevance** | Features used in the model are relevant to the prediction target and do not include prohibited or proxy attributes | Credit regulation prohibits discrimination; proxy features that correlate with protected characteristics must be identified and managed | Not assessed | Feature relevance assessment: all features evaluated for relevance to creditworthiness; correlation analysis for protected-characteristic proxies; exclusions documented |

---

### 5.3 ISO/IEC 5259-3 — Data Quality Management Requirements

This part specifies the management processes that must be in place to achieve and maintain the quality dimensions above.

| Management Requirement | Relevance to LumaCredit-EU | Current State | Required State |
|---|---|---|---|
| **Data quality policy** | Documented policy defining quality requirements for AI data | Absent | Data quality policy published; specific requirements for LumaCredit-EU feature data, training data, and bureau inputs defined |
| **Data quality roles and responsibilities** | Named data quality owner; data stewards for each source system | No data governance roles at LumaPay | Data owner (Head of Lending or CPTO), data stewards for Aurora, S3 feature store, and bureau API integrations |
| **Data quality assessment** | Regular formal assessment of data quality against the defined measures | Not performed | Quarterly data quality assessment: each dimension measured; results reported to Head of Lending; findings tracked to resolution |
| **Data quality improvement** | Process to identify and remediate data quality failures | Not defined | Corrective action process: data quality finding triggers root-cause analysis, remediation, and re-assessment |
| **Data quality monitoring in production** | Ongoing monitoring of operational data quality | Partial — Datadog monitors system metrics; no data-quality-specific monitoring | Data quality dashboard: completeness, timeliness, and consistency measures tracked in production; alerts on threshold breaches |
| **Third-party data quality** | Quality requirements applied to data received from bureau APIs and credit-check providers | Not applied | Third-party data quality obligations included in bureau and credit-check API contracts; API response quality validated before use in feature pipeline |

---

### 5.4 ISO/IEC 5259-4 — Data Quality Process Framework

This part provides the process structure for managing data quality across the AI lifecycle — from initial data acquisition through production monitoring and feedback.

| Process | Relevance to LumaCredit-EU | Current State | Required State |
|---|---|---|---|
| **Data requirements definition** | Define what data is needed, at what quality, for model training and operation | Not documented | Data requirements specification: each feature, its source, its quality threshold, and its relevance rationale |
| **Data acquisition** | Controlled process for acquiring training data from internal and external sources | Informal | Data acquisition procedure: approved sources listed, acquisition events logged, quality check applied at ingestion |
| **Data profiling** | Statistical analysis of data to understand its distribution, quality, and fitness | Not confirmed | Pre-training data profiling report: distributions, missing values, outliers, correlations, protected-characteristic correlations |
| **Data validation** | Validation that data meets quality requirements before use in training or inference | Not confirmed | Validation gate before model training: data must pass all quality checks before training proceeds |
| **Data documentation** | Comprehensive documentation of datasets used in training and validation | Not documented | Dataset documentation (equivalent to a data sheet or datacard): sources, collection date, transformations applied, quality assessment results, known limitations |
| **Operational data monitoring** | Ongoing monitoring of data quality in production feature pipeline | Partial | Feature distribution monitoring in production: alerts on distribution shift, missing-value spikes, and bureau API response quality degradation |
| **Data lifecycle and retention** | Data lifecycle managed from collection through deletion | Not documented | Data retention policy: training data retained for model governance period; production decision data retained per GDPR and Article 12 requirements; deletion procedures defined |

**Specific gap for LumaCredit-EU — unredacted PII in test:**
ISO 5259-4 requires that data used in test and development environments is handled with appropriate controls. The confirmed presence of unredacted customer PII in the `test` environment, where model validation and threshold testing are performed, is a direct violation of both ISO 5259 data management requirements and GDPR Article 5(1)(f) (integrity and confidentiality). This must be treated as a Day 1 remediation action.

---

## 6. NIST AI RMF Mapping

The NIST AI RMF provides the integrating governance lens — it translates the legal obligations (EU AI Act), management system requirements (ISO 42001), and data quality requirements (ISO 5259) into a structured, actionable risk management programme for LumaCredit-EU.

---

### 6.1 GOVERN

The GOVERN function establishes the accountability, policy, and oversight infrastructure that makes all other functions possible.

| GOVERN Sub-function | Requirement for LumaCredit-EU | Current State | Required State |
|---|---|---|---|
| GV.1.1 — AI policy | Policy governing LumaCredit-EU's permitted use, fairness obligations, and explainability requirements | Absent | AI policy published; specific credit-scoring provisions aligned to EU AI Act and FCA Consumer Duty |
| GV.1.2 — Roles and accountability | Executive owner (Head of Lending) and technical owner formally accountable | Named but not formally appointed | Formal appointment letters; accountability matrix approved by board |
| GV.1.3 — Risk tolerance | AI risk tolerance for credit decisions explicitly defined | Not defined | Risk appetite statement: acceptable error rate, acceptable approval rate band, acceptable demographic disparity, override rate thresholds |
| GV.1.4 — Change management | Stage-gate approval for model, rules, and pipeline changes | No change control documented | Change management process: all changes require risk assessment, validation evidence, and sign-off before production promotion |
| GV.2.1 — Accountability | Individual accountable for each decision the system makes | Not established | Head of Lending accountable for all credit decisions made by or with LumaCredit-EU; escalation path to Group Risk Committee |
| GV.3.1 — Culture | Staff understand model limitations, automation bias, and their oversight responsibility | No training programme | Mandatory training for lending operations staff; includes model limitations, reason-code interpretation, and override procedure |

---

### 6.2 MAP

The MAP function produces the evidence base for risk management — translating the system architecture and data flows into a classified risk profile.

#### System Classification

| Dimension | Assessment |
|---|---|
| **Risk tier** | Critical — high-risk AI under EU AI Act Annex III; direct customer impact; FCA-regulated decisions |
| **Decision type** | Automated with human oversight — but human oversight effectiveness is currently unverified |
| **Substrate properties** | Opacity (black-box SageMaker model) · Drift (performance degrades over time) · Dependency (bureau APIs and third-party credit-check providers) |
| **Data sensitivity** | Very High — creditworthiness data, financial data, identity data, potentially special-category data via open-banking |
| **Regulatory exposure** | EU AI Act Annex III (provider obligations) · GDPR Article 22 · FCA Consumer Duty · UK GDPR |

#### Data and Dependency Map

```
Customer Application
        │
        ▼
LCEU-API (ECS Decision Service)
        │                    │
        ▼                    ▼
LCEU-DATA                Third-Party APIs
Feature Pipeline         ├─ Credit Bureau API
(Aurora PostgreSQL        ├─ Affordability Check
 S3 Feature Store)        ├─ Open-Banking Aggregator
        │                 └─ Identity / Fraud Signal
        ▼
LCEU-MODEL
(SageMaker Endpoint)
        │
        ▼
LCEU-RULES
(Rules Engine / Policy Layer)
        │
        ▼
Approve / Decline / Manual Review Queue
        │
        ▼
Core Lending Platform + Audit Log (Aurora)
```

Every node in this map is a risk. The third-party API layer is particularly high-risk because it introduces dependency on data sources outside LumaPay's control — if a bureau API degrades, returns stale data, or becomes unavailable, the model receives corrupted inputs silently.

#### MAP Actions

| MAP Sub-function | Action | Current State |
|---|---|---|
| MAP.1 — Context | Document which customer segments, geographies, and lending products LumaCredit-EU serves | Partially described in HLD; not formally documented |
| MAP.2 — Categorise | Formally classify as high-risk, consequential, customer-facing credit-scoring AI system | Not classified |
| MAP.3 — Risks identified | Full risk enumeration with scenario descriptions | Partial risk list; not formally linked to the system |
| MAP.4 — Risk context | Map each risk to a concrete failure scenario and a specific regulatory breach | Not done |
| MAP.5 — Suppliers | Inventory all third-party dependencies with contract status, SLA, and data quality obligations | Not inventoried |

---

### 6.3 MEASURE

The MEASURE function converts identified risks into evidence-based assessments with KRIs and measurement approaches.

#### Risk Register Extract — LumaCredit-EU

| # | Risk | Likelihood | Impact | Control Maturity | Key Risk Indicator | Regulatory Link |
|---|---|---|---|---|---|---|
| 1 | EU AI Act high-risk obligations unmet — system in live service without required compliance posture | High | Critical | None | Number of open Article 9–17 gaps (target: zero before continued operation) | EU AI Act Articles 9–17 |
| 2 | Unredacted PII in `test` — customer creditworthiness data used in model validation and threshold testing | High | High | None — confirmed present | Number of test datasets containing live PII (target: zero) | GDPR Art. 5(1)(f), Art. 25; EU AI Act Art. 10 |
| 3 | Data quality and lineage failure — feature provenance, label quality, and bureau data provenance not documented | High | High | None | Percentage of features with documented lineage (target: 100%) | EU AI Act Art. 10; ISO 5259 |
| 4 | Model drift — performance degradation not detected in production | Medium | High | Low — monitoring infrastructure exists; no thresholds or review cadence | Gini coefficient against baseline; approval rate against 6-month average; bad-debt rate trend | EU AI Act Art. 72 |
| 5 | Rules and model misalignment — rules engine and model updated through different change paths | Medium | High | None | Number of rules changes deployed without corresponding model validation review | ISO 42001 Clause 8; EU AI Act Art. 9 |
| 6 | Third-party data dependency failure — bureau or credit-check API degrades or becomes unavailable | Medium | High | Low — no SLA monitoring or fallback logic documented | Bureau API error rate; API latency p99; last successful quality check date | ISO 5259-3; NIST AI RMF MAP.5 |
| 7 | Cross-border processing exposure — EU decision data in US-hosted Aurora backups or services | High | High | None | Confirmation of data residency for all LumaCredit-EU data stores | GDPR Art. 44–49; UK GDPR |
| 8 | No explainability for declined decisions — customers and regulators cannot understand why credit was refused | High | High | Low — reason codes described but not confirmed to be implemented and complete | Percentage of decline decisions with complete, auditable reason codes | EU AI Act Art. 13; GDPR Art. 22(3); Consumer Duty |
| 9 | Privileged access — developers and analysts with over-broad access to model endpoints and decision data | Medium | High | None — no IAM review documented | Number of identities with write access to SageMaker endpoint or Aurora decision tables | EU AI Act Art. 15; ISO 27001 |

#### KRIs for Monthly Reporting

| KRI | Amber Threshold | Red Threshold | Data Source |
|---|---|---|---|
| Gini coefficient vs baseline | Drop > 5 percentage points | Drop > 10 percentage points | Model monitoring / SageMaker |
| Approval rate vs 6-month average | Shift > ±5% | Shift > ±10% | Aurora decision log |
| Bad-debt rate at 3-month horizon | Rise > 10% relative | Rise > 20% relative | Core lending platform |
| Bureau API error rate | > 0.5% | > 2% | CloudWatch / API Gateway |
| Manual review queue depth | > 120% of baseline | > 200% of baseline | LCEU-RULES queue metrics |
| Override rate — human reviewer reverses system decision | > 15% (possible quality signal) | > 30% (system quality failing) | Aurora override log |
| Features with documented lineage | < 90% | < 75% | Data governance register |
| PII in test environment | > 0 records | > 0 records (binary — never acceptable) | DSPM scan / audit |

---

### 6.4 MANAGE

The MANAGE function sequences the treatment actions across the 100-day integration plan. For LumaCredit-EU, these actions are sequenced by legal obligation first, then governance, then technical improvement.

#### Pre-Close Critical (Day 0–5)

| Action | Rationale | Owner |
|---|---|---|
| Confirm EU AI Act high-risk classification in writing; brief Nordhaven Group Risk Committee | Nordhaven is acquiring a high-risk AI system with unmet provider obligations — this must be disclosed to the board before close | Legal + Head of Lending |
| Halt further copying of unredacted PII into `test`; initiate dataset audit | Active GDPR breach risk; Day 1 legal obligation | Engineering + DPO |
| Freeze all SageMaker model and rules engine changes pending governance review | Cannot manage what is changing; freeze establishes a baseline | CTO + Head of Lending |

#### Day 1–30

| Action | Rationale | Owner |
|---|---|---|
| Appoint formal system owner (Head of Lending) with documented accountability | EU AI Act Article 16 and ISO 42001 Clause 5 pre-requisite; enables all other governance actions | CRO + Head of Lending |
| Initiate EU AI Act Article 11 / Annex IV technical documentation package | Legal pre-market obligation; required before continued live operation can be defended | Head of Lending + Legal + Engineering |
| Implement Article 12 logging specification: model version, feature vector, score, reason codes, policy outcome, timestamp recorded per decision | Required for traceability, GDPR Art. 22(3) explanation, and audit reconstruction | Engineering |
| Conduct IAM privilege review: SageMaker endpoint, Aurora decision tables, S3 feature store, feature pipeline service accounts | High-risk system should have strict least-privilege access; no-security-team environment makes this urgent | Cloud Security / Platform |
| Begin data lineage documentation: map each feature from source system through feature pipeline to model input | EU AI Act Art. 10 requirement; also required for ISO 5259 traceability | Data Engineering |
| Draft reason-code specification: define which model features and rules produce each reason code; implement in LCEU-RULES output | Required for Article 13 transparency and Consumer Duty fairness | Engineering + Head of Lending |

#### Day 31–60

| Action | Rationale | Owner |
|---|---|---|
| Complete data quality assessment for training and operational data against ISO 5259-2 dimensions | Foundation for Article 10 compliance; also required for Article 11 documentation | Data Engineering + Model Governance |
| Conduct representativeness and bias assessment: cross-tabulate approval rates against available demographic proxies; document findings | EU AI Act Art. 10(2)(f); Consumer Duty fairness obligation | Data Science + Legal |
| Define model performance KRIs and thresholds; implement monitoring in CloudWatch and Datadog | EU AI Act Article 72 post-market monitoring; NIST AI RMF MEASURE | Engineering + Operations |
| Conduct supplier assessment for all bureau and credit-check APIs: SLA, data quality obligations, incident notification, DPAs | ISO 5259-3 third-party data quality; ISO 27036 supplier governance; GDPR Art. 28 | Legal + GRC |
| Remediate lower-environment PII: implement synthetic data pipeline for model validation and threshold testing | GDPR Art. 5(1)(f) permanent remediation; EU AI Act Art. 10(6) | Engineering + DPO |
| Publish initial risk appetite statement for credit-decision AI | NIST AI RMF GOVERN pre-requisite; enables the board to understand accepted residual risk | CRO + Head of Lending |

#### Day 61–100

| Action | Rationale | Owner |
|---|---|---|
| Complete EU AI Act Article 9 risk management system documentation | Legal obligation; required before a compliance defence can be maintained | Head of Lending + Legal |
| Conduct a formal model validation against holdout and recent production data; document results | EU AI Act Art. 9(6); ISO 42001 Clause 8.4.3 | Data Science + Model Governance |
| Register LumaCredit-EU in EU AI Act database (when applicable under implementation timeline) | Article 49 / Article 71 obligation | Legal |
| Establish quarterly model review cycle: Gini review, approval rate review, bad-debt review, bias review | EU AI Act Art. 72 post-market monitoring; ISO 42001 Clause 9 | Head of Lending + Data Science |
| Implement kill-switch procedure: route all decisions to manual review without system outage | EU AI Act Art. 14(3)(e); NIST AI RMF resilience | Engineering + Operations |
| Publish model card (Article 13 transparency document) for internal deployers and for regulatory readiness | EU AI Act Art. 13; Consumer Duty transparency | Head of Lending + Legal |

---

## 7. Cross-Framework Risk Summary

| Risk | EU AI Act | ISO 42001 | ISO 5259 | NIST AI RMF | Components | Severity |
|---|---|---|---|---|---|---|
| High-risk obligations unmet — system in service without compliance posture | Art. 9–17 | Clause 5–8, Annex A | 5259-1 general requirements | GOVERN, MAP | All | **Critical** |
| Unredacted PII in test | Art. 10(6) | Clause 8.5, A.6.1 | 5259-4 data lifecycle | MANAGE | `LCEU-DATA` | **Critical** |
| No Article 12 logging — decisions not reconstructable | Art. 12 | Clause 8.6, A.5.3 | 5259-4 documentation | MEASURE | `LCEU-API` `LCEU-MODEL` `LCEU-RULES` | **Critical** |
| No reason codes or explainability for declined decisions | Art. 13, Art. 14 | Clause 8.7, A.8 | — | GOVERN, MEASURE | `LCEU-RULES` | **Critical** |
| No technical documentation (Annex IV) | Art. 11 | Clause 8.4.5, A.5.2 | 5259-4 documentation | MAP, MEASURE | All | **Critical** |
| Data quality and lineage failure | Art. 10 | Clause 8.5, A.6.3 | All 5259 parts | MEASURE | `LCEU-DATA` | **Critical** |
| No representativeness or bias assessment | Art. 10(2)(f) | A.6.1 | 5259-2 representativeness | MEASURE | `LCEU-DATA` `LCEU-MODEL` | **High** |
| Model drift not detected | Art. 72 (post-market) | Clause 9.1, A.5.1 | 5259-3 monitoring | MEASURE | `LCEU-MODEL` | **High** |
| Rules/model misalignment — separate change paths | Art. 9 | Clause 8.2, A.5.1 | — | GOVERN, MANAGE | `LCEU-MODEL` `LCEU-RULES` | **High** |
| Third-party bureau API — no SLA, no data quality obligation, no fallback | Art. 15(2) | A.9.1 | 5259-3 third-party | MAP.5, MANAGE | `LCEU-API` | **High** |
| Cross-border processing — EU data in US services | Art. 10 (data governance) | Clause 8.5 | 5259-4 data lifecycle | MAP, MANAGE | `LCEU-DATA` | **High** |
| No human oversight mechanism — HITL nominal only | Art. 14 | Clause 8.7, A.8 | — | GOVERN | `LCEU-RULES` | **High** |
| Privileged access to model endpoint and decision data | Art. 15(4) | A.5.1 | — | MANAGE | `LCEU-MODEL` `LCEU-DATA` | **High** |

---

## 8. Matrix Feed — Framework Applicability Matrix Cells

### EU AI Act Risk Themes — LumaCredit-EU Components

| EU AI Act Theme | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES |
|---|---|---|---|---|
| 1. High-risk system classification missed or under-scoped | ✓ | ✓ | ✓ | ✓ |
| 2. Risk management system not defined (Art. 9) | ✓ | ✓ | ✓ | ✓ |
| 3. Data governance and data quality controls weak (Art. 10) | ~ | ✓ | ✓ | ~ |
| 4. Technical documentation incomplete (Art. 11 / Annex IV) | ✓ | ✓ | ✓ | ✓ |
| 5. Logging and record-keeping insufficient (Art. 12) | ✓ | ~ | ✓ | ✓ |
| 6. Transparency to deployers weak (Art. 13) | ~ | | ✓ | ✓ |
| 7. Human oversight ineffective or nominal only (Art. 14) | ~ | | ~ | ✓ |
| 8. Accuracy, robustness, cybersecurity insufficient (Art. 15) | ~ | ~ | ✓ | ~ |
| 9. Post-market monitoring weak (Art. 72) | ~ | | ✓ | ~ |
| 10. Conformity assessment readiness poor (Art. 16, 17) | ✓ | ✓ | ✓ | ✓ |

### ISO Risk Themes — LumaCredit-EU Components

| ISO Theme | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES |
|---|---|---|---|---|
| 1. AI management system not defined (ISO 42001) | ✓ | ✓ | ✓ | ✓ |
| 2. Information security controls weak (ISO 27001) | ~ | ✓ | ✓ | ~ |
| 3. AI risk treatment not formalised (ISO 23894) | ✓ | ✓ | ✓ | ✓ |
| 4. Data quality management weak (ISO 5259) | ~ | ✓ | ✓ | ~ |
| 5. Supplier governance weak (ISO 27036) | ✓ | ✓ | ~ | |
| 6. Environment segregation weak (ISO 27001) | ~ | ✓ | ~ | |
| 7. Change control weak (ISO 42001 / 27001) | ✓ | ✓ | ✓ | ✓ |
| 8. Monitoring and improvement loops weak (ISO 42001) | ~ | ✓ | ✓ | ~ |
| 9. Traceability and auditability weak (ISO 42001) | ✓ | ✓ | ✓ | ✓ |
| 10. Business continuity and fallback not defined (ISO 27001 / 27036) | ✓ | ~ | ✓ | ✓ |

### NIST AI RMF — LumaCredit-EU Components

| NIST AI RMF Function | LCEU-API | LCEU-DATA | LCEU-MODEL | LCEU-RULES |
|---|---|---|---|---|
| GOVERN | ✓ | ✓ | ✓ | ✓ |
| MAP | ✓ | ✓ | ✓ | ✓ |
| MEASURE | ✓ | ✓ | ✓ | ✓ |
| MANAGE | ✓ | ✓ | ✓ | ✓ |

---

## 9. Artefacts Required for Due Diligence

| Artefact | Framework Relevance | Status |
|---|---|---|
| EU AI Act high-risk classification decision and legal basis | EU AI Act Annex III | Not confirmed to exist |
| Article 11 / Annex IV technical documentation package | EU AI Act Art. 11 | Not confirmed to exist |
| Article 9 risk management system documentation | EU AI Act Art. 9 | Not confirmed to exist |
| Model card: performance metrics, known limitations, contraindicated uses | EU AI Act Art. 13; ISO 42001 A.5.2 | Not confirmed to exist |
| Training and validation data documentation: sources, lineage, quality assessment | EU AI Act Art. 10; ISO 5259 | Not confirmed to exist |
| Bias and representativeness assessment of training data | EU AI Act Art. 10(2)(f) | Not confirmed to exist |
| Reason-code specification and implementation evidence | EU AI Act Art. 13; GDPR Art. 22(3); Consumer Duty | Not confirmed to exist |
| Article 12 decision audit log specification and sample | EU AI Act Art. 12 | Not confirmed to exist |
| Bureau and credit-check API contracts and SLAs | ISO 5259-3; ISO 27036; GDPR Art. 28 | Not confirmed to exist |
| DPIA for LumaCredit-EU | GDPR Art. 35; EU AI Act Art. 10 | Not confirmed to exist |
| IAM role definitions for SageMaker, Aurora, and S3 feature store | EU AI Act Art. 15; ISO 27001 | Not confirmed to exist |
| Evidence of test-environment PII remediation | EU AI Act Art. 10(6); GDPR Art. 5 | Confirmed absent — live PII in test |
| Model performance monitoring history: Gini, approval rate, bad-debt rate | EU AI Act Art. 72; ISO 42001 Clause 9 | Not confirmed to exist |

---

*This document is part of the Nordhaven–LumaPay AI Risk Taskforce deliverable set. The final mapping will cover FraudShield. All findings feed into the master Framework Applicability Matrix at `04-risk-and-controls/framework-applicability-matrix.md`.*
