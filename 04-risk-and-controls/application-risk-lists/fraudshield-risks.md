# FraudShield Risks

## 1. Third-Party Model Dependency
- Risk: LumaPay depends on a vendor-hosted fraud model it does not fully control.
- Why it matters: a vendor outage, degradation, or strategic change can immediately weaken fraud defenses.
- Lens: operational
- Lifecycle stage: deploy, monitor

## 2. Change-of-Control And Licence Risk
- Risk: the acquisition may trigger change-of-control clauses, non-assignable rights, or contract renegotiation pressure.
- Why it matters: FraudShield access could be disrupted within days of close.
- Lens: governance, operational
- Lifecycle stage: design, deploy

## 3. Third-Party Data Processing Exposure
- Risk: transaction and identity signals are sent to a vendor whose hosting, subprocessors, or support locations may not be fully understood.
- Why it matters: this raises `GDPR`, `UK GDPR`, supplier-risk, and contractual assurance issues.
- Lens: governance, cyber
- Lifecycle stage: data, deploy

## 4. Vendor Model Opacity
- Risk: the fraud score and reason indicators may not be sufficiently transparent for internal challenge or review.
- Why it matters: business teams may be relying on a black box without strong explainability or tuning control.
- Lens: governance
- Lifecycle stage: design, monitor

## 5. Weak Fallback Design
- Risk: if the vendor API is unavailable, the local wrapper may fail open, fail closed, or route too many cases to manual review.
- Why it matters: fraud losses or customer friction can increase abruptly during disruptions.
- Lens: operational
- Lifecycle stage: deploy, monitor

## 6. Supply-Chain Security Exposure
- Risk: compromise of the vendor or its upstream model/data chain could poison scores or expose sensitive data.
- Why it matters: this is a classic third-party cyber and integrity risk with direct business impact.
- Lens: cyber
- Lifecycle stage: deploy, monitor

## 7. Threshold Tuning Error
- Risk: local decision thresholds may be badly tuned relative to vendor score behavior.
- Why it matters: false positives can damage customer experience, while false negatives can raise fraud losses.
- Lens: operational
- Lifecycle stage: develop, monitor

## 8. Downstream Agent Consumption Risk
- Risk: FraudShield outputs may later be consumed by internal agents or MCP-connected workflows without sufficient provenance checks.
- Why it matters: weakly governed vendor output can contaminate downstream automated decisions.
- Lens: governance, operational
- Lifecycle stage: data, monitor
