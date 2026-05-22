# LumaPay Company Profile

## Company Overview
LumaPay is a fictional `UK-regulated fintech` that provides embedded `Buy Now, Pay Later (BNPL)` and `SME lending` products. It is the target in Nordhaven’s acquisition of an `80%` ownership stake and represents the less mature AI and control environment in the transaction.

## Corporate And Operating Profile
- Employee count: about `200`
- Headquarters: `London`
- Legal footprint: primary `UK` entity with `EU` operations supporting regional lending and merchant servicing
- Market posture: fast-moving, innovation-first, product-led
- Regulatory profile: `FCA` oversight as a UK credit provider, with obligations under `Consumer Duty`, `UK GDPR`, and `GDPR`
- Data profile: personal, behavioural, and financial data processed across `UK`, `EU`, and `US-hosted cloud` environments

## Products And Revenue Model
- Embedded `BNPL` services integrated into merchant checkout journeys
- `SME lending` products for merchant working capital and growth financing
- Merchant-facing APIs and dashboards for onboarding, settlement, and risk insights
- Customer support channels augmented by AI-enabled assistance

## Workforce Shape
- `100` developers across product, backend, data, and AI-heavy engineering teams
- `5` people on the platform team covering cloud, CI/CD, environments, and core reliability
- No dedicated security team
- No dedicated GRC function focused on AI or cloud governance
- Small risk and compliance capability assumed to sit within legal or operations rather than a mature second line

## Technology And AI Posture
- Heavy use of foundation models, agentic workflows, and third-party APIs
- Two AWS accounts:
- `test` for development, integration, experimentation, and evaluation
- `production` for live customer and decision workloads
- Real customer `PII` has been copied into `test` without redaction or masking
- Likely reliance on manual controls, tribal knowledge, and developer judgment rather than formalized guardrails
- Limited centralized inventory of models, prompts, datasets, and third-party AI dependencies

## Security And Control Posture
- No `CSPM`
- No `DSPM`
- No modern dedicated AI security tooling
- No reliable control preventing production-like sensitive datasets from being used in lower environments
- Partial documentation for models, data lineage, and decision logic
- Limited lifecycle controls across design, data, development, deployment, and monitoring
- Fragmented board-level oversight and weak traceability from policy to control
- Likely shadow AI and undocumented tools outside a formal AI registry

## Key Weaknesses Relevant To The Capstone
- High dependency on key engineers and undocumented institutional knowledge
- Thin platform team relative to the scale and criticality of the AI estate
- Weak separation between experimentation and production-ready governance discipline
- Unredacted `PII` in `test` creates a concrete `GDPR`, `UK GDPR`, confidentiality, and insider-risk issue
- Increased exposure to prompt injection, data leakage, drift, and supplier dependency risk
- Greater chance of orphaned models, unowned pipelines, and inconsistent approvals during integration

## In-Scope AI Systems
- `LumaCredit-EU`
- `LumaAssist Chat`
- `AutoUnderwriter Agent`
- `FraudShield`

## Why LumaPay Matters In The Deal
LumaPay is attractive because its AI-enabled lending and merchant platform capabilities accelerate Nordhaven’s product ambitions. It is also risky because those same capabilities sit on top of immature governance, limited security depth, cross-border data flows, and concentrated engineering knowledge.
