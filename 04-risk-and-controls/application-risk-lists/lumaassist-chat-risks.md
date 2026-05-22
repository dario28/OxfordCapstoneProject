# LumaAssist Chat Risks

## 1. Prompt Injection Through Customer Input
- Risk: a customer can manipulate prompts to bypass guardrails or force unintended actions.
- Why it matters: this can produce unsafe responses, expose internal logic, or trigger inappropriate tool use.
- Lens: cyber
- Lifecycle stage: deploy, monitor

## 2. PII Leakage Through Traces And Logs
- Risk: prompts, responses, and tool traces may contain live customer `PII`, especially because `test` already contains copied unredacted data.
- Why it matters: this creates privacy exposure in `LangSmith`, logs, and analyst-review workflows.
- Lens: cyber, governance
- Lifecycle stage: data, monitor

## 3. Over-Broad MCP Tool Access
- Risk: the assistant can query internal `MCP` tools for CRM or ticket data with insufficient scope restriction.
- Why it matters: a simple customer chat can become a path to unauthorized data exposure or case manipulation.
- Lens: cyber, governance
- Lifecycle stage: design, deploy

## 4. Hallucinated Or Misleading Customer Guidance
- Risk: the assistant may generate inaccurate responses on payments, BNPL, or lending issues.
- Why it matters: customers can be misled, complaints can rise, and regulatory obligations under `Consumer Duty` can be breached.
- Lens: operational, governance
- Lifecycle stage: monitor

## 5. Knowledge-Base Provenance Weakness
- Risk: retrieval content may be stale, conflicting, or not formally approved.
- Why it matters: even a well-behaved model can produce wrong outputs if the underlying content is poor.
- Lens: operational
- Lifecycle stage: data, monitor

## 6. Lower-Environment Leakage
- Risk: prompt testing and jailbreak exercises in `test` may use copied live `PII`.
- Why it matters: developers and analysts gain access to customer data without a valid lower-environment control model.
- Lens: cyber, governance
- Lifecycle stage: data, develop

## 7. Weak Human Escalation Boundaries
- Risk: the assistant may fail to escalate when confidence is low or when a customer issue is sensitive.
- Why it matters: customer harm can occur because the human-in-the-loop model is inconsistently applied.
- Lens: operational, governance
- Lifecycle stage: design, deploy

## 8. API And Model-Key Misuse
- Risk: exposed or poorly governed credentials for Bedrock, MCP services, or support integrations may be misused.
- Why it matters: this could enable abuse, high-cost usage, or unauthorized data access.
- Lens: cyber
- Lifecycle stage: deploy, monitor
