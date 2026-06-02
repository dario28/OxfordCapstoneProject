# FraudShield — Framework Mapping
## ISO/IEC 27036 · DORA · NIST CSF 2.0 · GDPR / UK GDPR · EU AI Act (Classification)

**Document status:** Draft v1.0  
**Prepared by:** Nordhaven–LumaPay AI Risk Taskforce  
**Role context:** Amrik Randhawa 
**Date:** 2026-05-29  


---

## 1. Purpose and Scope

This document maps FraudShield against five frameworks. Three were specified; two are added here with explicit justification:

| Framework | Basis for inclusion |
|---|---|
| **ISO/IEC 27036** | Specified. The primary supplier security standard — governs the entire lifecycle of LumaPay's relationship with the FraudShield vendor |
| **DORA** | Specified. LumaPay's EU entity is subject to DORA as a payment-adjacent financial entity; FraudShield is an ICT third-party service provider under Article 28 |
| **NIST CSF 2.0** | Specified. Provides the operational cybersecurity capability model — Identify through Recover — applied to a vendor-integrated AI system |
| **GDPR / UK GDPR** | **Added.** Every FraudShield API call sends customer PII (transaction metadata, device fingerprint, identity signals) to a vendor whose hosting locations, subprocessors, and data-retention practices are unreviewed. This is a live data-processing compliance exposure that cannot be separated from the supply-chain risk analysis |
| **EU AI Act** | **Added.** A formal classification determination must be made before any other compliance decision. FraudShield is an AI system making automated decisions that affect EU customers. Whether it is high-risk or not-high-risk changes the obligation profile materially — but the determination must be documented either way |

The mapping is performed at the three FraudShield component levels defined in the Framework Applicability Matrix:

| Component ID | Description |
|---|---|
| `FS-WRAP` | Lambda decision wrapper — LumaPay-controlled threshold logic, fallback rules, decision routing |
| `FS-VENDOR` | FraudShield vendor API — third-party hosted model, scoring engine, upstream data and model supply chain |
| `FS-REVIEW` | Manual review queue — human fraud analyst escalation path, fallback decision mechanism |

---

## 2. System Snapshot — Why Dependency Is the Defining Risk

FraudShield is structurally different from the other three LumaPay AI systems. LumaAssist Chat, AutoUnderwriter Agent, and LumaCredit-EU all run on LumaPay infrastructure with LumaPay-controlled models. FraudShield does not. The fraud-scoring intelligence is **entirely external**. LumaPay contributes event data and a thin decision wrapper; everything consequential — the model, the training data, the scoring logic, the hosting, the upstream supply chain — belongs to a vendor.

This means the risk profile is dominated by three properties that cannot be engineered away:

| Property | What it means for FraudShield |
|---|---|
| **Dependency** | If the vendor API is unavailable, degraded, or withdrawn, LumaPay's fraud controls fail. There is no internal fallback model |
| **Opacity** | LumaPay cannot inspect the model, audit the training data, validate the scoring logic, or independently verify that scores are accurate and unbiased |
| **Scale asymmetry** | The vendor's decisions about model updates, pricing, data practices, and contract terms affect LumaPay's operations unilaterally — LumaPay has limited leverage to resist changes it does not like |

Four additional facts compound the risk:

| Fact | Consequence |
|---|---|
| **No documented change-of-control clause review** | The Nordhaven acquisition may trigger vendor contract provisions — assignment restrictions, price renegotiations, or termination rights — that could disrupt fraud controls within days of close |
| **No SLA or vendor security assurance obtained** | LumaPay has no contractual visibility into the vendor's availability, incident notification obligations, or security posture |
| **PII sent to vendor on every transaction** | Customer identity signals, transaction metadata, and device fingerprints cross to a third party on every call — without a confirmed DPA, data residency understanding, or subprocessor inventory |
| **No fallback design tested** | If the vendor API fails, the Lambda wrapper's behaviour (fail-open, fail-closed, or queue overflow) is undocumented and untested |

**The board-level statement for FraudShield:** LumaPay's primary fraud defence is a black box owned by a third party, operating under an unreviewed contract, processing customer PII at unknown locations, with no tested fallback. This is simultaneously a supply-chain security risk, an operational resilience risk, a data protection risk, and — pending classification — a potential AI governance risk. It must be treated as a pre-close critical item.

---

## 3. ISO/IEC 27036 Mapping

ISO/IEC 27036 is a four-part series governing information security in supplier relationships. It is the foundational standard for managing FraudShield as a third-party ICT service:

- **27036-1**: Overview and concepts — foundational supplier security principles
- **27036-2**: Requirements — the mandatory controls for the acquirer (LumaPay/Nordhaven)
- **27036-3**: Guidelines for ICT supply chain security — upstream supply chain of the vendor's model and data
- **27036-4**: Guidelines for cloud services — applicable because the vendor API is a cloud-hosted service

---

### 3.1 ISO/IEC 27036-1 — Overview and Concepts

The fundamental principle is that the acquiring organisation (LumaPay, now Nordhaven) remains accountable for the security outcomes of services delivered by third parties. Outsourcing execution does not outsource risk. This principle is the governing logic for everything below.

**Current state:** LumaPay does not operate as if this principle applies. There is no supplier security programme, no vendor risk register, and no evidence that anyone has formally accepted accountability for the security outcomes of FraudShield's operation.

**Required state:** Nordhaven's supplier security programme must be extended to cover FraudShield as a critical ICT third-party service from Day 1 of close.

---

### 3.2 ISO/IEC 27036-2 — Requirements

This part sets the mandatory requirements for the acquirer across the supplier relationship lifecycle: planning, selection, contracting, operation, and exit.

#### Supplier Relationship Planning

| Requirement | Relevance to FraudShield | Current State | Required State |
|---|---|---|---|
| Define security requirements for supplier relationships | Before or during contracting, LumaPay must define what security obligations FraudShield must meet | Not documented | Supplier security requirements specification: data handling, access controls, incident notification, audit rights, subprocessor controls, penetration test evidence |
| Classify the supplier relationship by criticality | FraudShield is a critical ICT supplier — fraud detection is a core operational control | Not classified | FraudShield formally classified as Critical ICT Supplier; elevated oversight requirements applied |
| Define information security objectives for the relationship | What outcomes must the vendor deliver for LumaPay to be adequately protected | Not documented | Objectives defined: 99.9% API availability, breach notification within 24 hours, annual penetration test report shared, no PII retained beyond transaction processing |

#### Supplier Selection and Due Diligence

| Requirement | Relevance to FraudShield | Current State | Required State |
|---|---|---|---|
| Security assessment prior to selection | Vendor's security posture assessed before the relationship begins | Not confirmed — vendor was selected under LumaPay's pre-governance-maturity environment | Retrospective security due diligence completed: SOC 2 Type II or ISO 27001 certificate obtained; data residency confirmed; known incident history reviewed |
| Right to audit | Contractual right to audit or receive independent audit evidence | Not confirmed | Audit rights clause in contract; minimum: annual SOC 2 Type II report; preferred: right to audit or commission third-party assessment |
| Subprocessor visibility | Identify all subprocessors used by the vendor | Not confirmed | Complete subprocessor list obtained; each subprocessor assessed for adequacy |

#### Contractual Security Requirements

This is the most urgent gap. Without a reviewed contract, none of the downstream controls can be enforced.

| Contractual Requirement | Relevance to FraudShield | Current State | Required State |
|---|---|---|---|
| Security obligations | Vendor contractually obligated to maintain security standards (ISO 27001 or equivalent) | Unknown | Contract includes: security standard commitment, right to request evidence, breach of standard as termination trigger |
| Incident notification | Vendor must notify LumaPay of security incidents within a defined period | Unknown | 24-hour notification for incidents involving LumaPay customer data; 72-hour notification for other material incidents |
| Data handling obligations | How the vendor handles LumaPay customer data: retention, deletion, use restrictions | Unknown | Vendor prohibited from using LumaPay data for model training without explicit consent; data deleted upon contract termination; no secondary use permitted |
| Subprocessor notification | Vendor must notify before adding subprocessors and allow LumaPay to object | Unknown | 30-day advance notification of subprocessor changes; right to object and terminate if change is unacceptable |
| Change notification | Vendor must notify LumaPay of material changes to the service (model updates, infrastructure changes, API changes) | Unknown | Minimum 30-day notice for material changes; API versioning maintained for minimum 6 months |
| **Change-of-control clause** | What happens to the contract if LumaPay is acquired by Nordhaven | **Unknown — pre-close critical risk** | Contract reviewed before close; if change-of-control clause is triggered: Nordhaven negotiates assignment or new contract before close; fallback plan activated if contract cannot be assigned |
| Exit and transition provisions | Procedures for terminating the relationship; data return and deletion; transition assistance | Unknown | Defined exit procedure: data return, deletion confirmation, transition period, replacement service onboarding support |

#### Ongoing Monitoring and Review

| Requirement | Relevance to FraudShield | Current State | Required State |
|---|---|---|---|
| Periodic supplier performance review | Regular review of vendor performance against SLA and security requirements | Not performed | Quarterly vendor performance review: API availability, incident count, false-positive rate trends, contractual compliance |
| Security incident review | Process for reviewing vendor-related security incidents | Not defined | Post-incident review procedure: root cause from vendor, LumaPay impact assessment, control improvement actions |
| Contract currency | Contract remains current and reflects actual service and risk profile | Unknown — contract not recently reviewed | Annual contract review: verify scope, data handling terms, SLAs, and security clauses remain current |

---

### 3.3 ISO/IEC 27036-3 — ICT Supply Chain Security

This part addresses the upstream supply chain behind the vendor's own service — the model training data providers, model hosting infrastructure, upstream fraud-data feeds, and software dependencies that the vendor uses to build and operate FraudShield.

| Supply Chain Risk | Relevance to FraudShield | Current State | Required State |
|---|---|---|---|
| **Vendor's upstream model supply chain** | FraudShield's fraud-scoring model was trained on data from sources LumaPay cannot see; if those sources were compromised, biased, or poisoned, scores are corrupted at source | No visibility into vendor's upstream training data provenance | Contractual right to receive a model provenance attestation: confirmation that training data sources, data governance, and model validation meet defined standards |
| **Vendor's infrastructure supply chain** | The vendor API runs on hosting infrastructure (likely a major cloud provider) with its own supply chain — misconfigurations or compromises upstream affect the service | No visibility into vendor's infrastructure | Vendor to confirm: hosting provider, region, security certifications (ISO 27001, SOC 2), and incident history for hosting infrastructure |
| **Fraud intelligence data feeds** | Many fraud-detection vendors use consortium fraud data or third-party threat intelligence as model inputs — compromise of these feeds can corrupt scores | Unknown whether FraudShield uses shared fraud data feeds | Vendor to disclose all upstream data sources; assess the integrity controls on each |
| **Software dependencies** | The vendor's API code and model inference runtime have software dependencies that may contain vulnerabilities | No visibility | Contractual right to receive annual confirmation that vendor conducts dependency vulnerability scanning |

---

### 3.4 ISO/IEC 27036-4 — Cloud Services

FraudShield is accessed via an API — meaning it is a cloud-hosted service in scope for 27036-4 guidelines.

| Cloud Service Requirement | Relevance to FraudShield | Current State | Required State |
|---|---|---|---|
| **Cloud service agreement adequacy** | The terms governing use of the cloud-delivered fraud API must cover security, availability, and data handling | Contract not reviewed | Cloud service agreement reviewed against 27036-4 minimum requirements: data location, portability, deletion, security controls, availability SLA |
| **Data location and jurisdiction** | Where customer data sent to the vendor is processed and stored | Unknown | Confirmed: data processed in EU/UK regions only, OR appropriate GDPR transfer mechanism in place |
| **Portability and exit** | Ability to retrieve data and switch to a different provider | Unknown | Contractual data portability rights confirmed; exit assistance obligations defined |
| **API credential security** | Credentials used to authenticate to the vendor API are managed securely | API credentials noted as stored in Secrets Manager | Credential rotation policy defined; access restricted to Lambda execution role only; rotation triggered immediately on any suspected compromise |

---

## 4. DORA Mapping

The Digital Operational Resilience Act (Regulation (EU) 2022/2554) applies to EU financial entities. LumaPay operates an EU legal entity as part of its cross-border lending and merchant-servicing operations. FraudShield is an ICT third-party service provider under DORA. The obligations apply to LumaPay's EU entity as the **financial entity** (the regulated party) — DORA does not directly regulate the vendor, but it mandates that the financial entity governs the relationship adequately.

**Important Nordhaven context:** Nordhaven, as the acquiring entity with its own EU financial services footprint, will inherit and amplify LumaPay's DORA obligations. The combined entity's ICT third-party risk register must include FraudShield from Day 1 of close.

---

### 4.1 Article 3 and Article 6 — ICT Risk Management Framework

DORA requires financial entities to maintain a comprehensive, documented ICT risk management framework. FraudShield sits within this framework as a critical third-party dependency.

| Requirement | Relevance to FraudShield | Current State | Required State |
|---|---|---|---|
| ICT risk management framework covers third-party ICT services | FraudShield must be within scope of LumaPay's ICT risk management framework, not treated as outside it | No ICT risk management framework at LumaPay | FraudShield included in LumaPay EU entity's ICT risk management framework; risk owner assigned |
| ICT assets mapped and classified | FraudShield API dependency mapped as a critical ICT asset | Not mapped | FraudShield API mapped in asset inventory; classified as Critical ICT Third-Party Service |
| ICT continuity policy covers third-party dependencies | Business continuity for fraud operations explicitly addresses vendor unavailability | Not documented | ICT continuity policy: FraudShield outage scenario included; fallback procedures defined and tested |

---

### 4.2 Article 28 — General Principles for ICT Third-Party Risk Management

This is the core DORA article for FraudShield. It requires financial entities to manage ICT third-party risk as an integral part of their ICT risk management framework.

| Article 28 Obligation | Requirement | Current State | Required State |
|---|---|---|---|
| 28.1(a) — Written policy | Written ICT third-party risk policy covering the selection, monitoring, and exit of ICT third-party service providers | Absent | ICT third-party risk policy published; FraudShield governed under it as a Critical provider |
| 28.1(b) — Pre-engagement assessment | Due diligence before using an ICT third-party service | Not confirmed (vendor was selected under pre-maturity environment) | Retrospective due diligence completed and documented; forward: pre-engagement assessment required for any new critical ICT service |
| 28.2 — Critical or important functions | Assess whether FraudShield supports a critical or important function | Not assessed | Formal assessment: fraud detection directly supports payment processing and onboarding — **critical or important function under DORA** |
| 28.3 — Concentration risk | Assess whether reliance on FraudShield creates ICT concentration risk | Not assessed | Concentration risk assessment: single-vendor fraud detection with no alternative; rated as concentration risk; treatment plan defined |
| 28.4 — Register of ICT arrangements | FraudShield included in formal register of information on ICT third-party arrangements | Not confirmed | Register maintained per Article 28(3) / Article 28(6) RTS requirements; submitted to competent authority if requested |
| 28.6 — Ongoing monitoring | Financial entity continuously monitors performance and security of ICT third-party service | Not performed | Continuous monitoring programme: API availability, incident notifications, SLA performance, contractual compliance reviewed quarterly |

---

### 4.3 Article 30 — Key Contractual Provisions

DORA Article 30 mandates minimum contractual content for ICT third-party service arrangements supporting critical or important functions. These are not optional — they are legal requirements for LumaPay's EU entity.

| Article 30 Provision | Requirement | Current State |
|---|---|---|
| 30.2(a) — Full description of services | Clear description of all services and functions provided, including subcontracted activities | Unknown — contract not reviewed |
| 30.2(b) — Locations | Data and service processing locations, including where data is stored | Unknown — critical gap for GDPR alignment |
| 30.2(c) — Data provisions | Provisions on data availability, integrity, confidentiality, and security | Unknown |
| 30.2(d) — Accessibility and recovery | Service availability commitments, recovery time and recovery point objectives | Unknown — no SLA confirmed |
| 30.2(e) — Full assistance by ICT third party | Vendor must cooperate with LumaPay's competent authority during incidents and investigations | Unknown |
| 30.2(f) — Termination rights | LumaPay's right to terminate and transition, including minimum notice periods and transition support | Unknown |
| 30.2(g) — Participation in security programmes | Vendor participates in LumaPay's security awareness and testing programmes | Unknown |
| 30.2(h) — Sub-ICT third-party service providers | Vendor discloses and controls its own ICT subcontractors | Unknown |
| 30.3 — Exit strategies | Financial entity maintains documented exit strategy for critical ICT services | **Absent — confirmed** |
| 30.4 — Change-of-control notification | Contract provisions addressing changes in ownership of the ICT third-party provider | Unknown — and the inverse (LumaPay being acquired) also matters |

**Gap assessment:** The FraudShield contract, as far as can be determined from the project materials, does not contain the mandatory Article 30 provisions. This is a legal compliance gap for LumaPay's EU entity that requires immediate remediation — either through contract amendment, or through a formal risk acceptance and remediation timeline submitted to the competent authority.

---

### 4.4 Article 24 and Article 26 — Testing and Operational Resilience

| Requirement | Relevance to FraudShield | Current State | Required State |
|---|---|---|---|
| Art. 24 — ICT system testing | LumaPay must test the resilience of its ICT systems, including testing behaviour under vendor unavailability | Not confirmed for FraudShield | Annual fallback test: simulate vendor API unavailability and verify that FS-WRAP fails safely, FS-REVIEW queue handles load, and fraud loss exposure is within acceptable limits |
| Art. 26 — Advanced testing (TLPT) | Financial entities identified by competent authorities must conduct Threat-Led Penetration Testing | Not in scope for LumaPay currently (TLPT applies to significant entities); relevant for Nordhaven group | Nordhaven to assess whether combined entity meets TLPT threshold post-acquisition; FraudShield integration included in scope if TLPT required |
| Fallback mode testing | Lambda wrapper fallback logic tested under vendor outage, degraded response, and timeout scenarios | Not confirmed — fallback noted as weak in risk register | Documented fallback test results: fail-safe mode confirmed, manual review queue capacity validated, customer impact assessed |

---

### 4.5 Articles 17–23 — ICT Incident Reporting

DORA creates mandatory ICT-related incident classification and reporting obligations for financial entities. Vendor-caused incidents must be within scope.

| Requirement | Relevance to FraudShield | Current State | Required State |
|---|---|---|---|
| Art. 17 — Incident classification | ICT-related incidents (including vendor outages or security breaches) classified by severity | No AI/vendor incident classification scheme | Incident classification scheme includes vendor-caused events: FraudShield API outage, vendor security breach, score drift incident, change-of-control disruption |
| Art. 18 — Major incident reporting | Major ICT-related incidents reported to competent authority within defined timeframes | No DORA-compliant incident reporting process | Major incident reporting process: FraudShield API outage exceeding defined duration → major incident → report to EU national competent authority |
| Art. 19 — Harmonised reporting | Incident reports in harmonised format | Not in place | Incident report template aligned to DORA RTS harmonised format |
| Art. 23 — Significant cyber threats | Significant threats (not just incidents) reported where appropriate | Not in place | Threat monitoring programme includes vendor threat intelligence; significant threats reported as required |

---

## 5. NIST CSF 2.0 Mapping

The NIST CSF 2.0 provides the operational cybersecurity capability model for FraudShield. Applied to a vendor-integrated AI system, the framework's value is in translating the ISO 27036 and DORA obligations into concrete technical and operational controls.

---

### GV — Govern

| Subcategory | Requirement for FraudShield | Current State | Required State |
|---|---|---|---|
| GV.OC-05 — Legal and regulatory requirements | DORA, GDPR, ISO 27036 obligations for FraudShield understood and owned | Not documented | Regulatory obligations mapped to FraudShield; owner assigned (Head of Fraud) |
| GV.RM-01 — Risk management strategy | Risk appetite for third-party AI fraud service defined | Not defined | Risk appetite statement: acceptable vendor outage duration, acceptable false-positive/negative rate shift, acceptable data-handling deviation |
| GV.RM-06 — Third-party risk policy | Written policy governing FraudShield as a critical third-party service | Absent | ICT third-party risk policy published per DORA Article 28 |
| GV.SC-01 — Supply chain risk management | FraudShield supply chain risks managed as part of organisational risk management | Not managed | FraudShield in ICT third-party risk register; quarterly review; board-level visibility |
| GV.SC-06 — Procurement requirements | Security requirements applied in vendor procurement and contract renewal | Not applied | Security requirements specification for FraudShield contract; aligned to ISO 27036-2 and DORA Article 30 |

**Gap assessment:** There is no governance infrastructure for FraudShield as a third-party AI service. The Head of Fraud is named as executive owner in the HLD but has no documented accountability, no risk appetite to operate against, and no supplier risk management process to follow.

---

### ID — Identify

| Subcategory | Requirement for FraudShield | Current State | Required State |
|---|---|---|---|
| ID.AM-01 — Asset inventory | FraudShield API dependency, Lambda wrapper, API credentials, and data flows inventoried | Not inventoried as a managed asset | FraudShield API classified as Critical ICT Asset in unified AI/ICT asset registry |
| ID.AM-07 — Data asset classification | Customer PII, transaction data, and device fingerprints sent to vendor classified | Not classified | All data categories sent to FraudShield API classified; retention and handling at vendor mapped |
| ID.RA-01 — Vulnerability identification | Vulnerabilities in the Lambda wrapper, API credential management, and vendor integration identified | Not performed | Annual vulnerability assessment of FS-WRAP Lambda code and API integration; penetration test of the wrapper endpoint |
| ID.RA-05 — Risk prioritisation | FraudShield risks prioritised in the organisational risk register | Partial — risk list exists; not formally prioritised | Risk register entries for FraudShield: change-of-control, vendor outage, supply-chain compromise, data exposure — prioritised and owned |
| ID.SC-02 — Supplier inventory | All ICT suppliers and their services inventoried | Not confirmed | Supplier inventory includes FraudShield vendor with: contract reference, data processed, criticality rating, review cadence, and DORA Article 28 assessment status |
| ID.SC-04 — Supplier performance monitoring | Supplier performance monitored against defined requirements | Not performed | Quarterly vendor performance review: availability, incident rate, score quality, contractual compliance |

---

### PR — Protect

| Subcategory | Requirement for FraudShield | Current State | Required State |
|---|---|---|---|
| PR.AA-02 — Identity management | API credentials used to authenticate to FraudShield managed and protected | Credentials in Secrets Manager — described in HLD | Credential rotation policy: minimum annual rotation; immediate rotation on any compromise; access restricted to Lambda execution role only; no developer access to production credentials |
| PR.AA-05 — Access permissions | Principle of least privilege applied to FraudShield integration | Not confirmed | Lambda execution role has only the permissions needed to call the vendor API and write to Aurora — no broader IAM permissions |
| PR.DS-02 — Data in transit | Data sent to FraudShield vendor API protected in transit | TLS likely — not confirmed | TLS 1.2+ confirmed for all calls to vendor API; vendor TLS certificate pinned or validated |
| PR.DS-10 — Data minimisation | Only the minimum necessary data sent to the vendor on each API call | Not confirmed | Data minimisation review: every field sent to FraudShield API justified; fields not required for scoring removed from the API call |
| PR.IR-01 — Incident response covers vendor scenarios | Incident response plan covers FraudShield vendor outage and security breach | Not documented | Playbooks published for: vendor API outage, vendor security breach, score drift incident, change-of-control disruption |
| PR.PS-01 — Configuration management | Lambda wrapper configuration managed and hardened | Not confirmed | Configuration baseline defined for Lambda wrapper; infrastructure-as-code enforced; no manual production configuration changes |

---

### DE — Detect

| Subcategory | Requirement for FraudShield | Current State | Required State |
|---|---|---|---|
| DE.AE-02 — Anomalous activity detected | Anomalous vendor behaviour (unusual scores, latency spikes, error surges) detected | CloudWatch and Datadog in place; no FraudShield-specific detection rules | Detection rules configured: API error rate threshold, response latency p99 alert, fraud score distribution shift alert, unusual false-positive rate trend |
| DE.CM-06 — External service provider monitoring | FraudShield vendor activity and service quality continuously monitored | Not performed | Vendor monitoring dashboard: API availability, error rate, score distribution, latency — reviewed weekly by Platform Integrations Manager |
| DE.AE-06 — Event correlation | FraudShield events correlated with internal fraud-loss data | Not confirmed | Correlation rule: score distribution shift + fraud loss rate increase → combined alert → escalation to Head of Fraud |
| DE.AE-07 — Threat intelligence | Threat intelligence about the FraudShield vendor (known vulnerabilities, security incidents) monitored | Not performed | Vendor security advisories subscribed to; CVE monitoring for known vendor components; DORA significant threat reporting process |

---

### RS — Respond

| Subcategory | Requirement for FraudShield | Current State | Required State |
|---|---|---|---|
| RS.MA-01 — Incident response plan | Response plan for FraudShield-specific incidents | Not documented | Incident playbooks for: vendor API outage (< 1 hour, > 1 hour, > 4 hours), vendor security breach, score quality degradation, change-of-control event |
| RS.CO-02 — Regulatory notification | DORA major incident reporting triggered when FraudShield incident meets severity threshold | Not defined | DORA incident reporting decision tree: FraudShield outage duration and customer impact mapped to reporting obligations; EU national competent authority contact details maintained |
| RS.AN-03 — Root cause analysis | Root cause analysis performed after FraudShield incidents | Not defined | Post-incident review template: vendor root cause (obtained contractually), LumaPay impact assessment, control improvement actions |
| RS.MI-02 — Incident containment | FraudShield incident contained without full service disruption | Not documented | Containment procedure: route all transactions to manual review queue or apply static rule-based fallback while vendor issue is investigated |

---

### RC — Recover

| Subcategory | Requirement for FraudShield | Current State | Required State |
|---|---|---|---|
| RC.RP-01 — Recovery plan | Recovery plan for FraudShield unavailability | **Absent — confirmed gap** | Recovery runbook: step-by-step procedure for restoring normal FraudShield operation after vendor outage; tested annually |
| RC.RP-02 — Recovery objectives | RTO and RPO defined for FraudShield integration | Not defined | RTO: maximum time FraudShield can be unavailable before fallback is activated (suggested: 15 minutes for full outage); RPO: not applicable (stateless API) |
| RC.RP-04 — Alternative processing | Alternative fraud-detection mechanism available during vendor outage | **Not designed — critical gap** | Alternative mechanism defined: static rule-based fraud scoring or simplified scoring model for use during vendor outage; capacity and effectiveness validated |
| RC.RP-05 — Vendor exit strategy | Plan to replace FraudShield if relationship terminates | **Absent** | Exit strategy documented: alternative vendor shortlist, contract transition requirements, data migration plan, minimum 90-day parallel-run period |

**Gap assessment:** The Recover function has the most critical gaps of any CSF function for FraudShield. There is no recovery plan, no tested fallback, and no exit strategy. If the change-of-control event disrupts vendor access, LumaPay has no fraud detection capability and no plan to restore it.

---

## 6. GDPR / UK GDPR Mapping

**Why this framework was added:** On every FraudShield API call, LumaPay transmits customer personal data — identity signals, transaction metadata, device fingerprints, and behavioural indicators — to a third-party vendor. This is personal data processing by a processor (the vendor) on behalf of a controller (LumaPay). The GDPR and UK GDPR create specific obligations for this relationship that run in parallel with and reinforce the ISO 27036 and DORA supply-chain requirements.

---

### Controller–Processor Relationship

| Obligation | Requirement | Current State | Required State |
|---|---|---|---|
| **Article 28 — Data Processing Agreement** | LumaPay must have a written DPA with the FraudShield vendor covering: processing instructions, data security, subprocessor control, audit rights, deletion, and assistance with data subject rights | **Not confirmed to exist** | DPA executed before continued processing; DPA includes all Article 28(3) mandatory clauses |
| **Article 28(2) — Subprocessor control** | Vendor may not engage subprocessors without LumaPay's prior authorisation; existing subprocessors must be listed | Subprocessors unknown | Subprocessor list obtained; each subprocessor assessed for adequacy; DPA flow-down confirmed |
| **Article 28(3)(g) — Deletion / return** | Vendor must delete or return all LumaPay data on termination | Unknown | Deletion/return obligation in DPA; confirmation of deletion obtained on contract termination |

---

### International Data Transfers

| Obligation | Requirement | Current State | Required State |
|---|---|---|---|
| **Articles 44–49 — Transfer mechanism** | If the vendor hosts or processes data outside the UK/EU (e.g., in the US), an appropriate transfer mechanism must be in place: adequacy decision, Standard Contractual Clauses, or Binding Corporate Rules | Vendor hosting location unknown | Vendor data locations confirmed; if outside UK/EU: appropriate transfer mechanism executed (EU SCCs or UK IDTA); Transfer Impact Assessment completed if required |
| **UK GDPR — IDTA** | For UK entity: International Data Transfer Agreement executed for any non-UK transfers | Not confirmed | UK entity: IDTA executed where required; UK data residency or adequate transfer mechanism confirmed |

---

### Data Minimisation and Purpose Limitation

| Obligation | Requirement | Current State | Required State |
|---|---|---|---|
| **Article 5(1)(b) — Purpose limitation** | Data sent to the vendor may only be used for the stated fraud-detection purpose; vendor cannot use it for model training, product development, or other purposes without a separate legal basis | Vendor data-use terms unknown | DPA explicitly prohibits vendor from using LumaPay data for any purpose other than providing the contracted fraud-detection service |
| **Article 5(1)(c) — Data minimisation** | Only the minimum necessary data fields are sent to the vendor for each API call | Not confirmed | Data minimisation review completed; every field in the API call payload justified; unjustified fields removed |
| **Article 5(1)(e) — Storage limitation** | Data is not retained by the vendor beyond what is necessary | Vendor retention unknown | Vendor retention period confirmed and time-limited; DPA specifies maximum retention period |

---

### Individual Rights and Transparency

| Obligation | Requirement | Current State | Required State |
|---|---|---|---|
| **Article 13/14 — Transparency** | Customers must be informed that their data is shared with a third-party fraud detection service | Not confirmed | Privacy notice updated to disclose FraudShield as a data processor; processing purpose and legal basis stated |
| **Article 22 — Automated decision-making** | Where FraudShield output contributes to a decision with significant effect (transaction block, onboarding refusal), Article 22 safeguards must apply | Not assessed | Legal basis for automated fraud decisions documented; significant decisions (not just low-risk score-routing) include human review capability |

---

## 7. EU AI Act — Classification Analysis

**Why this framework was added:** FraudShield is an AI system making automated decisions that affect EU customers (transaction blocks, onboarding refusals). Before any other AI governance obligation is applied, a formal classification determination under the EU AI Act must be made. The determination changes the obligation profile materially.

---

### Classification Determination

**Step 1 — Is FraudShield within scope of the EU AI Act?**

| Criterion | Assessment |
|---|---|
| Is FraudShield an AI system? | Yes — it is a vendor-hosted ML model that generates fraud scores and reason indicators from input data |
| Is it placed on the EU market or put into service in the EU? | Yes — LumaPay uses it in its EU lending and payment operations |
| Is it used by a provider or deployer subject to EU AI Act? | LumaPay is a **deployer** (it uses the vendor's AI system in its operations, not as the provider) |

**Step 2 — Is FraudShield a high-risk AI system under Annex III?**

The most relevant Annex III categories to assess:

| Annex III Category | Assessment for FraudShield |
|---|---|
| **Section 5(b) — Creditworthiness / credit scoring** | The clause states: *"with the exception of AI systems used for the purpose of detecting financial fraud."* FraudShield is explicitly a fraud-detection system. **This exception appears to apply.** FraudShield is likely excluded from high-risk classification under Section 5(b) |
| **Section 1 — Biometric categorisation** | FraudShield uses device fingerprinting and behavioural signals. If any feature constitutes biometric data processing (e.g., behavioural biometrics), Section 1 obligations may apply | Requires further legal analysis |
| **Section 6 — Law enforcement** | Not applicable — FraudShield is used by a private financial entity, not a law enforcement authority |

**Preliminary verdict:** FraudShield is likely **not classified as high-risk** under EU AI Act Annex III, primarily because Section 5(b) explicitly excludes fraud-detection AI from the credit-scoring high-risk classification. However:

1. **This determination must be formally documented.** A preliminary assessment that is not documented provides no legal protection.
2. **The biometric signal question must be resolved.** If FraudShield uses behavioural biometrics, a separate Section 1 analysis is required.
3. **Deployer obligations still apply regardless of high-risk status.** Article 26 (deployer obligations) applies to all AI systems, not only high-risk ones.

---

### Article 26 — Deployer Obligations (All AI Systems)

Even if FraudShield is not high-risk, LumaPay as deployer has obligations under Article 26:

| Article 26 Obligation | Requirement | Current State | Required State |
|---|---|---|---|
| 26.1 — Use in accordance with instructions | LumaPay must use FraudShield in accordance with the vendor's instructions and intended purpose | Vendor use instructions not confirmed received | Vendor instructions obtained and documented; LumaPay use of FraudShield confirmed within intended purpose |
| 26.2 — Qualified persons | Natural persons assigned to oversee high-impact AI systems have necessary competence | Not confirmed | Fraud operations staff with oversight responsibility trained on FraudShield capabilities, limitations, and override procedures |
| 26.5 — Fundamental rights impact | Deployers of AI systems used in certain contexts must conduct a fundamental rights impact assessment | Not conducted | Fundamental rights impact assessment for FraudShield: assess whether fraud-blocking decisions disproportionately affect protected groups |
| 26.6 — Inform affected persons | Where required, inform individuals that they are subject to an AI system's output | Not confirmed | Review whether disclosure obligation applies to transaction-blocking or onboarding-refusal decisions; update customer communications if required |

---

### GPAI Considerations

If FraudShield is built on a general-purpose AI model (GPAI model) as its underlying foundation, the vendor has obligations under Articles 51–56. LumaPay should:
- Ask the vendor whether FraudShield is built on a GPAI model
- If yes, obtain the vendor's technical documentation demonstrating GPAI compliance
- Include GPAI status in the supplier security assessment

---

## 8. Cross-Framework Risk Summary

The table below integrates all five frameworks. Risks appearing across multiple frameworks simultaneously are the highest-priority items for the board pack and the 100-day plan.

| Risk | ISO 27036 | DORA | NIST CSF | GDPR/UK GDPR | EU AI Act | Components | Severity |
|---|---|---|---|---|---|---|---|
| Change-of-control clause unknown — contract may be disrupted at close | 27036-2 contracting | Art. 28, Art. 30 | GV.SC-06, RC.RP-05 | Art. 28 DPA | Art. 26 | `FS-VENDOR` | **Critical** |
| No DPA with vendor — PII sent to vendor without lawful processing basis | 27036-2 | Art. 30.2(c) | PR.DS | Art. 28 | Art. 26 | `FS-VENDOR` | **Critical** |
| No fallback design — vendor outage leaves LumaPay without fraud detection | 27036-2 exit | Art. 28.1, Art. 30.2(d) | RC.RP-04 | — | — | `FS-WRAP` `FS-REVIEW` | **Critical** |
| No exit strategy — cannot replace vendor if relationship terminates | 27036-2 exit | Art. 30.3 | RC.RP-05 | — | — | `FS-VENDOR` | **Critical** |
| Vendor data location unknown — GDPR transfer basis unconfirmed | 27036-4 | Art. 30.2(b) | ID.AM-07 | Art. 44–49 | — | `FS-VENDOR` | **Critical** |
| Vendor contract does not contain DORA Article 30 mandatory provisions | 27036-2 | Art. 30 | GV.SC-06 | Art. 28 | — | `FS-VENDOR` | **Critical** |
| No SLA — vendor availability and RTO obligations uncontracted | 27036-2 | Art. 30.2(d) | ID.SC-04, DE.CM-06 | — | — | `FS-VENDOR` | **High** |
| No incident notification clause — vendor breach or outage may go unreported | 27036-2 | Art. 17–19 | RS.CO-02 | Art. 28(3)(f) | — | `FS-VENDOR` | **High** |
| No audit rights — cannot verify vendor security posture | 27036-2 | Art. 30, Art. 28.6 | ID.SC-02 | Art. 28(3)(h) | Art. 26 | `FS-VENDOR` | **High** |
| Vendor model opacity — scores cannot be challenged or explained | 27036-3 | Art. 28.1 | ID.RA-05 | Art. 22 | Art. 26 | `FS-VENDOR` | **High** |
| Supply-chain compromise — vendor or upstream data feed contaminated | 27036-3 | Art. 28.1 | DE.AE-02, RS.MI-02 | Art. 28 | — | `FS-VENDOR` | **High** |
| Threshold tuning error — wrapper logic not validated against vendor score behaviour | — | Art. 24 (testing) | DE.AE-02, PR.PS-01 | — | Art. 26 | `FS-WRAP` | **Medium** |
| Downstream agent contamination — FraudShield outputs consumed by agents without provenance check | — | — | DE.AE-06 | — | — | `FS-VENDOR` `FS-WRAP` | **Medium** |
| EU AI Act classification not formally documented | — | — | GV.OC-05 | — | Annex III | `FS-VENDOR` | **Medium** |

---

## 9. Priority Actions (First 100 Days)

### Pre-Close Critical (Day 0–5)

| Action | Rationale | Owner |
|---|---|---|
| Obtain and review the FraudShield vendor contract in full — specifically change-of-control clauses, assignment rights, and termination provisions | If the acquisition triggers a contract clause, LumaPay could lose fraud detection capability immediately after close | Legal + Head of Fraud |
| If a change-of-control clause exists: negotiate assignment to Nordhaven before close, or activate contingency planning for an alternative service | Pre-close critical — cannot be deferred | Legal + CTO |
| Confirm whether a DPA with the vendor exists; if not, halt new personal data flows until a DPA is in place or obtain emergency legal opinion on interim basis | Live GDPR Article 28 obligation | DPO + Legal |
| Brief the Nordhaven Group Risk Committee on FraudShield as a pre-close critical dependency risk | Board-level visibility required before close | CRO + Head of Fraud |

### Day 1–30

| Action | Rationale | Owner |
|---|---|---|
| Execute DPA with FraudShield vendor per GDPR Article 28 / UK GDPR; include all mandatory clauses | Legal obligation; unblocks compliant operation | DPO + Legal |
| Confirm vendor data locations; establish EU SCCs or UK IDTA for any non-UK/EU processing | GDPR Article 44–49; required for lawful processing | DPO + Legal |
| Conduct data minimisation review: audit every field in the FraudShield API call payload; remove unjustified fields | GDPR Article 5(1)(c); also reduces attack surface | Engineering + DPO |
| Obtain vendor SLA, security certifications (SOC 2 Type II or ISO 27001), and incident history | ISO 27036-2; DORA Article 30.2(d) | Head of Fraud + GRC |
| Design and document the FraudShield fallback procedure: fail-safe rules, manual review queue capacity, escalation triggers | DORA Article 28; NIST CSF RC.RP-04; most urgent operational gap | Platform Engineering |
| Complete EU AI Act classification analysis and document the determination | Deployer obligation; required before other AI governance decisions can be made | Legal + Head of Fraud |

### Day 31–60

| Action | Rationale | Owner |
|---|---|---|
| Negotiate DORA Article 30 mandatory contract provisions into FraudShield contract at next renewal or via amendment | DORA legal obligation for EU entity; cannot be deferred indefinitely | Legal + Head of Fraud |
| Obtain subprocessor list from vendor; assess each subprocessor for data handling adequacy and GDPR compliance | GDPR Article 28(2); ISO 27036-2 | DPO + GRC |
| Implement FraudShield monitoring in Datadog and CloudWatch: API availability, error rate, score distribution shift, latency p99 | NIST CSF DE.AE-02; DORA Article 17 (incident detection) | Platform Engineering |
| Conduct first quarterly vendor performance review: availability, incident log, contractual compliance, score quality | ISO 27036-2 ongoing monitoring; DORA Article 28.6 | Head of Fraud |
| Credential rotation: rotate FraudShield API credentials; confirm restricted access to Lambda execution role only | NIST CSF PR.AA-02; ISO 27036-2 | Platform Engineering |
| Register FraudShield in Nordhaven ICT third-party risk register and DORA Article 28 register of arrangements | DORA Article 28; ISO 27036-2; governance visibility | GRC |

### Day 61–100

| Action | Rationale | Owner |
|---|---|---|
| Conduct and document fallback test: simulate vendor API unavailability; verify fail-safe behaviour; measure manual review queue performance | DORA Article 24; NIST CSF RC.RP-01 | Platform Engineering + Head of Fraud |
| Document exit strategy: alternative vendor shortlist, data migration plan, minimum parallel-run period | DORA Article 30.3; ISO 27036-2 exit planning | Head of Fraud + Legal |
| Assess FraudShield for biometric data content (behavioural biometrics in device fingerprint signals); complete GPAI assessment | EU AI Act classification completeness | Legal + Data Science |
| Publish vendor oversight policy for FraudShield: review cadence, escalation triggers, renewal assessment requirements | ISO 27036-2; DORA Article 28.1; GV.SC-01 | GRC + Head of Fraud |
| Integrate FraudShield incident scenarios into DORA ICT incident reporting process; confirm major incident thresholds and notification contacts | DORA Articles 17–19 | CISO + GRC |

---

## 10. Matrix Feed — Framework Applicability Matrix Cells

### GDPR Risk Themes — FraudShield Components

| GDPR Theme | FS-WRAP | FS-VENDOR | FS-REVIEW |
|---|---|---|---|
| 1. Lawful basis, purpose limitation, or fairness unclear | ~ | ✓ | |
| 2. Data minimisation weak | ✓ | ✓ | |
| 3. Live PII copied into test or lower environments | ~ | | |
| 4. International transfer controls weak | | ✓ | |
| 5. DPIA or privacy risk assessment missing | ✓ | ✓ | |
| 6. Security of processing insufficient | ~ | ✓ | |
| 7. Logging, retention, or deletion controls weak | ~ | ✓ | |
| 8. Data subject rights support weak | ~ | ✓ | |
| 9. Processor / subprocessor governance weak | | ✓ | |
| 10. Profiling / automated decision-making safeguards weak | ~ | ✓ | ✓ |

### ISO Risk Themes — FraudShield Components

| ISO Theme | FS-WRAP | FS-VENDOR | FS-REVIEW |
|---|---|---|---|
| 1. AI management system not defined (ISO 42001) | ~ | ✓ | |
| 2. Information security controls weak (ISO 27001) | ~ | ✓ | |
| 3. AI risk treatment not formalised (ISO 23894) | ✓ | ✓ | |
| 4. Data quality management weak (ISO 5259) | | ✓ | |
| 5. Supplier governance weak (ISO 27036) | ✓ | ✓ | |
| 6. Environment segregation weak (ISO 27001) | ~ | | |
| 7. Change control weak (ISO 42001 / 27001) | ✓ | ~ | |
| 8. Monitoring and improvement loops weak (ISO 42001) | ✓ | ✓ | ~ |
| 9. Traceability and auditability weak (ISO 42001) | ✓ | ✓ | ~ |
| 10. Business continuity and fallback not defined (ISO 27001 / 27036) | ✓ | ✓ | ✓ |

### NIST CSF Functions — FraudShield Components

| NIST CSF Function | FS-WRAP | FS-VENDOR | FS-REVIEW |
|---|---|---|---|
| GV — Govern | ✓ | ✓ | ~ |
| ID — Identify | ✓ | ✓ | ~ |
| PR — Protect | ✓ | ✓ | |
| DE — Detect | ✓ | ✓ | ~ |
| RS — Respond | ✓ | ✓ | ✓ |
| RC — Recover | ✓ | ✓ | ✓ |

---

## 11. Artefacts Required for Due Diligence

| Artefact | Framework Relevance | Status |
|---|---|---|
| FraudShield vendor contract — full text including change-of-control, assignment, and termination clauses | ISO 27036-2; DORA Art. 30 | **Pre-close critical — must be reviewed before close** |
| Data Processing Agreement with FraudShield vendor | GDPR Art. 28; UK GDPR | Not confirmed to exist |
| Vendor data location confirmation (processing and storage regions) | GDPR Art. 44–49; DORA Art. 30.2(b) | Not confirmed |
| Vendor subprocessor list | GDPR Art. 28(2); ISO 27036-2 | Not confirmed |
| Vendor SLA: availability commitments, RTO, incident notification timeframes | DORA Art. 30.2(d); ISO 27036-2 | Not confirmed |
| Vendor security certifications: SOC 2 Type II or ISO 27001 | ISO 27036-2; DORA Art. 30 | Not confirmed |
| Vendor incident history: last 24 months of material security and availability incidents | ISO 27036-2; DORA Art. 28 | Not confirmed |
| FraudShield fallback procedure and test results | DORA Art. 24; NIST CSF RC.RP-04 | Not confirmed to exist |
| Exit strategy documentation | DORA Art. 30.3; ISO 27036-2 | Not confirmed to exist |
| EU AI Act classification determination | EU AI Act; Art. 26 deployer obligations | Not confirmed to exist |
| FraudShield incident playbooks | DORA Art. 17–19; NIST CSF RS.MA-01 | Not confirmed to exist |
| API credential management policy and rotation records | ISO 27036-4; NIST CSF PR.AA-02 | Not confirmed to exist |

---

*This document completes the framework mapping series for all four LumaPay AI applications. All four mappings feed into the master Framework Applicability Matrix at `04-risk-and-controls/framework-applicability-matrix.md`. The next phase is to populate the matrix tables using the Matrix Feed cells from each mapping document.*
