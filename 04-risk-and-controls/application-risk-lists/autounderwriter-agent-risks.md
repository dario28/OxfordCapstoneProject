# AutoUnderwriter Agent Risks

## 1. Excessive Agent Autonomy
- Risk: the agent can chain multiple tool calls and generate underwriting recommendations with insufficient control boundaries.
- Why it matters: unsafe automation may influence high-impact credit decisions in ways that are hard to explain.
- Lens: governance, operational
- Lifecycle stage: design, deploy

## 2. MCP Tool Permission Overreach
- Risk: the agent has access to broad `MCP` tools for affordability, policy, fraud, and document retrieval.
- Why it matters: prompt misuse or workflow failure can turn model behavior into direct access to sensitive systems and records.
- Lens: cyber
- Lifecycle stage: develop, deploy

## 3. Prompt Injection Through Uploaded Documents
- Risk: malicious or malformed uploaded documents can influence the agent’s tool behavior or recommendation logic.
- Why it matters: the underwriting workflow becomes vulnerable through the document ingestion path.
- Lens: cyber, operational
- Lifecycle stage: data, monitor

## 4. Unredacted PII In Test Agent Runs
- Risk: copied live `PII` is present in `test`, where agent-permission testing and adversarial exercises take place.
- Why it matters: lower-environment experimentation amplifies privacy and confidentiality risk.
- Lens: cyber, governance
- Lifecycle stage: data, develop

## 5. Recommendation Traceability Gap
- Risk: the recommendation pack may not clearly show which tool outputs, prompts, and rules produced the final advice.
- Why it matters: accountability is weak when underwriters, auditors, or regulators ask why a recommendation was made.
- Lens: governance
- Lifecycle stage: monitor

## 6. Human Override Fatigue
- Risk: underwriters may over-trust the agent or rubber-stamp recommendations when volume is high.
- Why it matters: human-in-the-loop becomes nominal rather than effective.
- Lens: governance, operational
- Lifecycle stage: deploy, monitor

## 7. Tool-Chain Dependency Failure
- Risk: affordability, identity, fraud, or document tools may fail or return inconsistent data.
- Why it matters: the agent can generate partial or misleading recommendations without obvious errors.
- Lens: operational
- Lifecycle stage: data, monitor

## 8. Cross-Border And Trace Retention Exposure
- Risk: prompts, traces, and tool outputs may cross boundaries into `US-hosted` services or be retained longer than intended.
- Why it matters: this creates transfer and retention risk for highly sensitive financial and document data.
- Lens: governance, cyber
- Lifecycle stage: data, monitor

## 9. Emergent Capability Creep
- Risk: incremental additions to tools and prompts can expand the agent’s real authority beyond the original design.
- Why it matters: governance can lag behind actual agent behavior and business dependence.
- Lens: governance
- Lifecycle stage: design, develop, monitor
