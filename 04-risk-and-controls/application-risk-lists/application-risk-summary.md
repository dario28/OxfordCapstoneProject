# Application Risk Summary

## LumaCredit-EU
Strongest themes:
- high-risk AI governance and conformity gaps
- unredacted `PII` in `test`
- data quality and lineage weakness
- production drift and explainability issues

## LumaAssist Chat
Strongest themes:
- prompt injection
- `PII` leakage through prompts, traces, and logs
- over-broad `MCP` tool access
- weak escalation and knowledge governance

## AutoUnderwriter Agent
Strongest themes:
- excessive autonomy
- over-privileged `MCP` tools
- prompt injection through documents
- weak recommendation traceability
- copied live `PII` in `test`

## FraudShield
Strongest themes:
- third-party dependency
- change-of-control and licence disruption
- supply-chain exposure
- vendor opacity
- weak fallback design

## Best Candidates For The Formal 10–12 Register
- Unredacted `PII` in `test` environments
- Prompt injection against customer-facing or internal AI systems
- Over-broad `MCP` tool permissions
- High-risk AI governance gap in `LumaCredit-EU`
- Model drift in `LumaCredit-EU`
- Recommendation traceability gap in `AutoUnderwriter Agent`
- Change-of-control disruption for `FraudShield`
- Third-party data-transfer and supplier-assurance gap
- Shadow AI or undocumented tools outside the AI registry
- Talent flight and orphaned models
- Governance misalignment between Nordhaven and LumaPay
- Cross-border logging and trace-retention exposure
