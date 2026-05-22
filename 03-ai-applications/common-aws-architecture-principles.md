# Common AWS Architecture Principles

These principles keep the four system HLDs consistent and simple enough for control mapping.

## Core Platform Pattern
- `AWS test account` for build, integration testing, prompt evaluation, and pre-production validation
- `AWS production account` for live workloads
- `Amazon API Gateway` as the main external entry point for application APIs
- `AWS Lambda`, `Amazon ECS`, or `AWS Step Functions` for application and orchestration logic
- `MCP` servers hosted on `Amazon ECS` for tool access from LLM and agent workflows where applicable
- `Amazon S3` for document, feature, and model artefacts
- `Amazon Aurora PostgreSQL` or `Amazon RDS PostgreSQL` for transactional data
- `Amazon SQS` and `Amazon EventBridge` for decoupled processing

## Observability And AI Tracing
- `Amazon CloudWatch` for baseline logs and metrics
- `Datadog` for centralized dashboards, alerting, and service monitoring
- `LangSmith` for LLM prompt traces, evaluation runs, and agent execution records where applicable

## Security Basics Assumed
- `AWS IAM` roles with separation between `test` and `production`
- `AWS KMS` for key management
- `AWS Secrets Manager` for API keys and service secrets
- `AWS CloudTrail` for control-plane logging
- Network segmentation using VPCs, private subnets, and controlled egress where feasible

## MCP-Specific Assumptions
- `MCP` servers expose internal tools such as CRM lookup, document retrieval, policy search, affordability calculators, and ticket actions
- Separate `test` and `production` MCP endpoints should exist, but LumaPay’s governance maturity means environment separation and tool scoping may be weak
- MCP tool permissions should be treated as a first-class risk area because an agent can turn model misuse into direct system action
- Copied unredacted `PII` in `test` increases the impact of MCP misuse because lower-environment tools may expose live customer records and documents

## Data Handling Assumptions
- Card or payment data should be tokenized by a payment processor and not exposed to LLM workflows
- PII and financial decision data should remain within defined service boundaries
- Cross-border data flows to `US-hosted` services must be made visible for `GDPR` and `UK GDPR` analysis
- Current-state exception for the capstone: LumaPay has copied unredacted `PII` into `test`, so lower-environment data handling must be treated as a known control failure rather than a hypothetical risk

## Why This Is Enough For The Capstone
These designs are intentionally high-level. They provide enough structure to map:
- `NIST AI RMF`
- `NIST CSF`
- `ISO/IEC 42001`
- `ISO/IEC 27001`
- `PCI DSS`
- `GDPR` and `UK GDPR`
- `EU AI Act`
