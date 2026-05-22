# LumaPay Architecture Baseline

## Core Assumptions For This Draft
- Two AWS accounts:
- `test` for development, integration, evaluation, and pre-production validation
- `production` for live regulated workloads
- Unredacted production `PII` has been copied into the `test` account
- Mixed infrastructure and suppliers during the `12–18 month` transition window
- Data and model dependencies across `UK`, `EU`, and `US-hosted cloud regions`
- No dedicated security engineering function inside LumaPay

## Team And Control Reality
- `100` developers can introduce or modify application and AI workloads quickly
- Only `5` platform engineers support cloud foundations, environments, CI/CD, and reliability
- Security responsibilities are distributed informally across engineering and platform staff
- Cloud and AI risk management is likely reactive rather than policy-driven

## Architecture Themes To Reflect In Drafts
- Credit-decisioning workload with high-risk AI implications
- LLM and agentic components exposed to prompt and tool-use risk
- Third-party fraud-detection dependency with supplier and change-of-control concerns
- Cross-border data transfer and privacy constraints
- Transitional dual-running and duplicated attack surfaces
- Limited ability to continuously validate posture due to lack of `CSPM`, `DSPM`, and AI-native tooling

## Likely Current-State Gaps
- No automated cloud posture management
- No automated data security posture visibility
- No modern AI security controls for prompt, model, or agent monitoring
- Incomplete asset inventory for models, datasets, prompts, and model-connected APIs
- No enforced masking or tokenization standard for lower environments
- Inadequate segregation between production-sensitive data and development workflows
- Weak formal review gates between `test` and `production`
- Thin evidence trail for audit logs, model approvals, and data lineage

## Baseline Control Areas We Should Design Around
- IAM and role separation across `test` and `production`
- Data lineage, data quality, and retention controls
- Model inventory, registry, and ownership assignment
- Deployment approvals and stage-gate reviews
- Monitoring, drift detection, and incident escalation
- Vendor and API dependency management
- Audit logging and evidence retention

## Integration Implications
- Nordhaven’s control stack is materially stronger than LumaPay’s
- Tooling uplift will likely be part of the `100-day` plan rather than available at close
- During the transition, duplicated platforms and inconsistent controls create exploitable seams
- The presence of unredacted `PII` in `test` should be treated as an immediate red flag for due diligence and early remediation
- The architecture write-up should make ownership, exceptions, and escalation paths explicit

## Drafting Notes
- Every system design should explicitly identify `Design`, `Data`, `Develop`, `Deploy`, and `Monitor` touchpoints.
- Every system design should call out governance, operational, and cyber controls.
- Every system design should make transitional ownership and escalation assumptions visible.
