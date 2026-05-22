# LumaCredit-EU Risks

## 1. High-Risk AI Governance Gap
- Risk: `LumaCredit-EU` is a high-risk credit-decision system, but documentation, model ownership, and approval records are incomplete.
- Why it matters: This creates exposure under the `EU AI Act`, weakens board accountability, and undermines audit readiness.
- Lens: governance
- Lifecycle stage: design, deploy

## 2. Unredacted PII In Test Data
- Risk: customer `PII` and creditworthiness data have been copied into `test` without masking for model validation and troubleshooting.
- Why it matters: This creates direct `GDPR`, `UK GDPR`, confidentiality, and insider-risk exposure.
- Lens: cyber, governance
- Lifecycle stage: data, develop

## 3. Data Quality And Lineage Failure
- Risk: feature lineage, training labels, and external data provenance are not reliably documented.
- Why it matters: poor data quality can lead to inaccurate lending decisions, explainability gaps, and regulatory challenge.
- Lens: operational, governance
- Lifecycle stage: data

## 4. Model Drift In Production
- Risk: approval rates, bad-debt indicators, and feature distributions may drift without timely detection.
- Why it matters: the system can silently degrade and continue making poor decisions at scale.
- Lens: operational
- Lifecycle stage: monitor

## 5. Rules And Model Misalignment
- Risk: the policy rules layer and the predictive model may diverge because updates are made through different change paths.
- Why it matters: customers may receive inconsistent outcomes that are hard to explain or defend.
- Lens: operational, governance
- Lifecycle stage: develop, deploy

## 6. Third-Party Data Dependency
- Risk: bureau, open-banking, or external scoring feeds may fail, degrade, or change without adequate controls.
- Why it matters: underwriting quality and fairness can deteriorate quickly if core input data becomes unreliable.
- Lens: operational
- Lifecycle stage: data, monitor

## 7. Cross-Border Processing Exposure
- Risk: EU and UK decision data may flow into `US-hosted` services or backups without fully controlled transfer logic.
- Why it matters: this raises international-transfer and lawful-processing concerns under `GDPR`.
- Lens: governance, cyber
- Lifecycle stage: data, deploy

## 8. Privileged Access To Sensitive Models And Data
- Risk: developers or analysts may have over-broad access to the model endpoint, feature store, or decision logs.
- Why it matters: misuse or accidental changes could compromise sensitive lending data or alter outcomes.
- Lens: cyber
- Lifecycle stage: deploy, monitor
