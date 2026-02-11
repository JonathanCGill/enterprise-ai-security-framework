# Enterprise AI Security Framework

A practical guide to securing AI systems that can't be fully tested before deployment.

![Enterprise AI Security — Control Architecture](/images/control-architecture.svg)

---

## The Problem

Traditional software assurance assumes you can prove correctness before shipping. Write code, test it, deploy it.

AI breaks this. The same input produces different outputs. Behaviour emerges that no test suite predicted. Users find edge cases you never imagined. And the model you evaluated last month may not be the model running today.

You can't fully test a non-deterministic system. So how do you know it's working correctly?

---

## The Answer

**Runtime behavioral monitoring.** Instead of proving correctness at design time, continuously verify behaviour in production.

| Layer | Function | Timing |
|-------|----------|--------|
| **Guardrails** | Prevent known-bad inputs and outputs | Real-time (~10ms) |
| **LLM-as-Judge** | Detect unknown-bad via model evaluation | Async (~500ms–5s) |
| **Human Oversight** | Decide edge cases, remain accountable | As needed |

Guardrails prevent. The Judge detects. Humans decide.

This pattern already exists in production at scale. What's been missing is a clear explanation of *why* it's necessary and *how* to implement it proportionate to risk — including its limits.

---

## Before You Start

> **[The First Control: Choosing the Right Tool](/insights/the-first-control.md)**
>
> The most effective way to reduce AI risk is to not use AI where it doesn't belong. Before guardrails, judges, or human oversight — ask whether AI is the right tool for this problem.

Everything in this framework assumes you've already answered "yes."

---

## Core Content

The foundation. Start here.

| Document | Purpose |
|----------|---------|
| [Risk Tiers](/core/risk-tiers.md) | Classify your system by deployment context, determine control requirements |
| [Controls](/core/controls.md) | Guardrails, Judge, Human Oversight — the three-layer pattern |
| [Agentic](/core/agentic.md) | Additional controls for single-agent AI systems |
| [Multi-Agent Controls](/core/multi-agent-controls.md) | Delegation, identity propagation, circuit breakers for agent-to-agent systems |
| [Judge Assurance](/core/judge-assurance.md) | Measuring and maintaining the accuracy of your LLM-as-Judge |
| [Multimodal Controls](/core/multimodal-controls.md) | Extending text-based controls to image, audio, video, and document inputs |
| [Memory and Context](/core/memory-and-context.md) | Session isolation, persistent memory, accumulated context risks |
| [Streaming Controls](/core/streaming-controls.md) | Buffer-and-release, post-hoc evaluation, non-streaming patterns |
| [Reasoning Model Controls](/core/reasoning-model-controls.md) | Controls for chain-of-thought and extended thinking models |
| [Emerging Controls](/core/emerging-controls.md) | Research-stage controls not yet ready for production guidance |
| [Checklist](/core/checklist.md) | Track your implementation |

---

## Extensions

Reference material for specific needs.

### Technical

| Document | Purpose |
|----------|---------|
| [SOC Integration](/extensions/technical/soc-integration.md) | Alert taxonomy, identity correlation, SIEM rules, triage procedures |
| [RAG Security](/extensions/technical/rag-security.md) | Ingestion controls, retrieval filtering, indirect injection mitigation |
| [Supply Chain](/extensions/technical/supply-chain.md) | Model provenance, dependency scanning, AI-BOM, shadow AI discovery |
| [NHI Lifecycle](/extensions/technical/nhi-lifecycle.md) | Agent identity provisioning, authentication, access review, deprovisioning |
| [Anomaly Detection Ops](/extensions/technical/anomaly-detection-ops.md) | Baselines, detection rules, alert routing, false positive management |
| [Cost and Latency](/extensions/technical/cost-and-latency.md) | Sampling strategies, latency budgets, making the Judge affordable at scale |
| [Bypass Prevention](/extensions/technical/bypass-prevention.md) | Preventing guardrail and judge circumvention |
| [Infrastructure](/extensions/technical/infrastructure.md) | Deployment architecture and network controls |
| [Metrics](/extensions/technical/metrics.md) | What to measure and how |
| [Current Solutions](/extensions/technical/current-solutions.md) | Industry tools — guardrails, evaluators, safety models |

### Regulatory

| Document | Purpose |
|----------|---------|
| [ISO 42001 Mapping](/extensions/regulatory) | Control mapping to AI management system standard |
| [EU AI Act](/extensions/regulatory) | Compliance alignment |

### Templates

| Document | Purpose |
|----------|---------|
| [Incident Playbook](/extensions/templates/incident-playbook.md) | When AI alerts become incidents |
| [Threat Model Template](/extensions/templates/threat-model-template.md) | Structured AI threat modelling |
| [Testing Guidance](/extensions/templates/testing-guidance.md) | How to test your controls |

### Examples

| Document | Purpose |
|----------|---------|
| [Worked Examples](/extensions/examples) | Implementation by use case |

---

## Insights

Articles explaining the thinking behind the framework. The [insights directory](/insights) has a full index with reading order by audience.

### Why This Pattern?

| Article | Summary |
|---------|---------|
| [The First Control](/insights/the-first-control.md) | Design thinking before technology selection |
| [Why Guardrails Aren't Enough](/insights/why-guardrails-arent-enough.md) | You need detection for unknown-bad |
| [The Judge Detects. It Doesn't Decide.](/insights/judge-detects-not-decides.md) | Async evaluation for nuance |
| [Infrastructure Beats Instructions](/insights/infrastructure-beats-instructions.md) | Prompts alone can't secure systems |
| [Risk Tier Is Use Case](/insights/risk-tier-is-use-case.md) | Classification by deployment, not capability |
| [Humans Remain Accountable](/insights/humans-remain-accountable.md) | AI assists; humans own outcomes |

### Emerging Challenges

| Article | Summary |
|---------|---------|
| [The Verification Gap](/insights/the-verification-gap.md) | Ground truth is hard |
| [Behavioral Anomaly Detection](/insights/behavioral-anomaly-detection.md) | Detecting drift from normal |
| [Multimodal Breaks Guardrails](/insights/multimodal-breaks-guardrails.md) | Non-text inputs bypass text controls |
| [When AI Thinks](/insights/when-ai-thinks.md) | Reasoning models need new controls |
| [When Agents Talk to Agents](/insights/when-agents-talk-to-agents.md) | Multi-agent accountability gaps |
| [The Memory Problem](/insights/the-memory-problem.md) | Persistent context risks |
| [You Can't Validate Unfinished](/insights/you-cant-validate-unfinished.md) | Streaming breaks the validation model |

### Operational Gaps

| Article | Summary |
|---------|---------|
| [The Supply Chain Problem](/insights/the-supply-chain-problem.md) | You don't control the model you deploy |
| [RAG Is Your Biggest Attack Surface](/insights/rag-is-your-biggest-attack-surface.md) | Retrieval pipelines bypass access controls |

---

## The Pattern in Practice

This isn't theory. These platforms implement variants of the three-layer pattern today:

| Platform | Implementation |
|----------|---------------|
| [NVIDIA NeMo Guardrails](https://github.com/NVIDIA/NeMo-Guardrails) | 5 rail types: input, dialog, retrieval, execution, output |
| [LangChain](https://docs.langchain.com/) | Middleware + human-in-the-loop |
| [Guardrails AI](https://www.guardrailsai.com/) | Open-source validator framework |
| [Galileo](https://www.rungalileo.io/) | Eval-to-guardrail lifecycle |
| [DeepEval](https://github.com/confident-ai/deepeval) | LLM-as-judge evaluation framework |
| AWS Bedrock Guardrails | Managed input/output filtering |
| Azure AI Content Safety | Content filtering and moderation |

And these standards describe the risks the pattern addresses:

| Standard | Focus |
|----------|-------|
| [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/) | Security vulnerabilities in LLM applications |
| [OWASP Top 10 for Agentic Applications](https://genai.owasp.org/) | Risks specific to autonomous AI agents |
| [NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework) | Risk management framework |
| [ISO 42001](https://www.iso.org/standard/81230.html) | AI management system standard |

---

## Architecture Diagrams

Visual references for the control architecture and key patterns.

| Diagram | Shows |
|---------|-------|
| [Control Architecture](/images/control-architecture.svg) | Full three-column view: Runtime, Pipeline, and Assurance controls |
| [RAG Attack Surface](/images/rag-attack-surface.svg) | RAG pipeline with six attack vectors mapped |
| [Multi-Agent Topologies](/images/multi-agent-topologies.svg) | Orchestrator, Peer-to-Peer, Hierarchical with risk profiles |
| [SOC Integration Flow](/images/soc-integration-flow.svg) | Telemetry sources through correlation to severity routing |
| [Streaming Patterns](/images/streaming-patterns.svg) | Three streaming control patterns with latency timelines |
| [Supply Chain Boundaries](/images/supply-chain-boundaries.svg) | What you control vs. what you don't |
| [AI Security Tube Map](/images/ai-security-tube-map.svg) | Navigational overview of the full framework |

---

## Scope

**In scope:** Custom LLM applications, RAG pipelines, AI decision support, document processing, agentic and multi-agent systems, AI supply chain governance.

**Out of scope:** Vendor AI products (Copilot, Gemini, etc.) — use vendor controls. Model training — see MLOps security guidance. Pre-deployment testing — this guide is about production monitoring.

This guide is operationally focused — deployment through incident response.

---

## Quick Start

| Need | Go To |
|------|-------|
| Conceptual overview in 30 minutes | [Quick Start](/QUICK_START.md) |
| Working code, copy and adapt | [Implementation Guide](/IMPLEMENTATION_GUIDE.md) |
| Classify a system | [Risk Tiers](/core/risk-tiers.md) |
| Implement controls | [Controls](/core/controls.md) |
| Deploy an agent | [Agentic](/core/agentic.md) |
| Secure a RAG pipeline | [RAG Security](/extensions/technical/rag-security.md) |
| Integrate with your SOC | [SOC Integration](/extensions/technical/soc-integration.md) |
| Threat model an AI system | [Threat Model Template](/extensions/templates/threat-model-template.md) |
| Map to ISO 42001 | [Regulatory Extensions](/extensions/regulatory) |
| Understand the thinking | [Insights](/insights) |

---

## Status

This is a practical guide, not a standard. It combines existing patterns with implementation guidance and honest assessments of what doesn't work yet. Feedback welcome — see [CONTRIBUTING.md](/CONTRIBUTING.md).

---

## License

[MIT](/LICENSE)
