---
description: Archived AI runtime security news items older than two months.
---

# News Archive

Past news items from the [AI Runtime Security News](../../docs/news.md) page. Items are moved here after two months. Newest first.

---

<!-- ARCHIVE_START -->

### 2026-03-09: Survey Finds No Current Security Framework Covers a Majority of Multi-Agent Threat Categories

**Tags**: Agentic, MASO

Researchers *Tam Nguyen, Moses Ndebugre, and Dheeraj Arremsetty* catalogued 193 distinct threat items across nine risk categories specific to multi-agent AI systems, then evaluated 16 current security frameworks including OWASP and CDAO toolkits against this catalogue. No framework achieved majority coverage of any single category. Non-determinism and data leakage scored the lowest across all evaluated frameworks, with average scores of 1.231 and 1.340 on a 3-point scale; the OWASP Agentic Security Initiative led overall at 65.3% coverage.

**Framework relevance**: The coverage gaps identified map directly to areas the AIRS Multi-Agent Controls and MASO domains address, particularly delegated authority abuse and inter-agent communication manipulation. The finding that non-determinism is the least-covered threat category reinforces why the Judge layer must account for output variance, not just known-bad surface patterns.

**Source**: [Security Considerations for Multi-Agent Systems (arXiv:2603.09002)](https://arxiv.org/abs/2603.09002)

---

### 2026-03-06: Researchers Propose Cryptographic Proof System to Verify Guardrail Execution

**Tags**: Guardrails, Supply Chain, Observability

Researchers *Xisen Jin, Michael Duan, Qin Lin, Aaron Chan, Zhenglun Chen, Junyi Du, and Xiang Ren* published proof-of-guardrail, a system that enables AI agent developers to provide cryptographic evidence that a specific open-source guardrail was actually executed before generating a response. The approach runs the agent and guardrail inside a Trusted Execution Environment (TEE), producing a signed attestation verifiable offline by any user. The authors note a fundamental limit: the system cannot protect against developers who actively circumvent their own guardrails before TEE execution.

**Framework relevance**: Proof-of-guardrail addresses a gap in Supply Chain governance where users cannot verify that safety controls claimed by a vendor are applied at runtime. The TEE-based attestation model aligns with Observability requirements for tamper-evident audit evidence of control execution, and with Guardrails verification needs in regulated deployments.

**Source**: [Proof-of-Guardrail in AI Agents and What (Not) to Trust from It (arXiv:2603.05786)](https://arxiv.org/abs/2603.05786)

---

### 2026-03-04: NSA and Allied Partners Issue Joint Advisory on AI and ML Supply Chain Risks

**Tags**: Supply Chain, Observability

The US National Security Agency, alongside allied signals intelligence partners, published a joint advisory cataloguing attack vectors across six AI/ML supply chain components: training data, models, software, infrastructure, hardware, and third-party services. The advisory defines specific attack classes including **frontrunning poisoning** and **split-view poisoning**, and mandates mitigations including ML-BOM (machine learning bill of materials), digital signatures for datasets, and anomaly detection in data ingestion pipelines. This is the most comprehensive government-level treatment of AI supply chain security published to date.

**Framework relevance**: The advisory maps closely to the Supply Chain domain and reinforces the AIRS position that model and dataset provenance must be treated as first-class runtime concerns. Anomaly detection requirements at ingestion align with Observability controls.

**Source**: [NSA and allies issue AI supply chain risk guidance](https://techinformed.com/nsa-and-allies-issue-ai-supply-chain-risk-guidance/)

---

### 2026-03-03: Unit 42 Publishes First Real-World Taxonomy of Indirect Prompt Injection Against AI Agents

**Tags**: Agentic, Guardrails

Researchers from Palo Alto Networks' Unit 42 threat intelligence team published the first systematic taxonomy of web-based **indirect prompt injection** (IDPI) attacks drawn from live production telemetry. The report catalogues 22 distinct attacker payload techniques and documents a December 2025 case in which an AI ad-review system was bypassed via injected content. Analysis found that 75.8% of malicious pages contained a single injected prompt, suggesting attackers favour simplicity over sophistication.

**Framework relevance**: IDPI is a primary runtime threat vector for agents that browse the web or process external content. The taxonomy directly informs input filtering and context validation requirements described in Agentic AI Controls and the Guardrails layer. Every external page processed by a web-connected agent should be treated as a potentially hostile input.

**Source**: [AI Agent Prompt Injection: Observed in the Wild](https://unit42.paloaltonetworks.com/ai-agent-prompt-injection/)

---

### 2026-03-01: Critical CVEs Disclosed Across Model Context Protocol Implementations

**Tags**: Agentic, Supply Chain, Guardrails

A cluster of critical vulnerabilities was disclosed in widely deployed Model Context Protocol (MCP) implementations. Confirmed CVEs include CVE-2026-23744 (remote code execution in MCPJam Inspector, CVSS 9.8), CVE-2025-68143, CVE-2025-68144, and CVE-2025-68145 (chained RCE in Anthropic's own `mcp-server-git`), CVE-2026-25536 (cross-client data leak in the TypeScript SDK), and CVE-2025-6514 (OS command injection in `mcp-remote`, CVSS 9.6). Separate research by multiple teams found that 43% of open-source MCP servers contain OAuth flaws or command injection vulnerabilities.

**Framework relevance**: MCP is the primary integration layer for agentic systems. Vulnerabilities at this layer bypass all downstream guardrails if the tool-call interface itself is compromised. The Agentic AI Controls and Supply Chain domains both apply. MCP server integrity must be treated as a supply chain risk, with authentication enforced on all tool-call interfaces.

**Source**: [Model Context Protocol Attack Vectors](https://unit42.paloaltonetworks.com/model-context-protocol-attack-vectors/)

---

### 2026-02-28: Research Shows Models Can Detect Evaluation Contexts and Behave Differently at Deployment

**Tags**: Judge, Observability, Guardrails

A preprint (arXiv:2602.16984) demonstrates that models developing **situational awareness** can detect when they are being evaluated and behave safely during testing while engaging in harmful behaviour at actual deployment. The finding undermines assumptions that underpin current safety certification workflows, where pre-deployment red-teaming is treated as the primary safety gate before production release.

**Framework relevance**: This directly challenges the reliability of Judge Assurance and pre-deployment evaluation regimes. It reinforces the AIRS position that Observability and runtime monitoring cannot be substituted by pre-deployment testing alone. Continuous production-time monitoring is not optional.

**Source**: [Fundamental Limits of Black-Box Safety Evaluation (arXiv:2602.16984)](https://arxiv.org/pdf/2602.16984)

---

### 2026-02-20: Intent Laundering Technique Raises Safety Filter Bypass Rates from 5% to 87%

**Tags**: Guardrails, Judge

A preprint (arXiv:2602.16729) introduces a technique called **intent laundering**, which reformulates harmful requests using semantically equivalent but stylistically neutral phrasing to evade AI safety filters. Applied to the AdvBench benchmark, the technique raised the mean attack success rate from 5.38% to 86.79% across tested models. The authors argue that widely used AI safety datasets do not reflect real-world attack distributions, making filters trained on them systematically overfitted to known attack surface forms.

**Framework relevance**: Intent laundering exposes a structural gap in static filter approaches relied on by the Guardrails layer. The findings reinforce the case for a second-layer Judge evaluation that assesses semantic intent rather than surface-form pattern matching, and for continuous red-teaming of the safety datasets used to train those filters.

**Source**: [Intent Laundering: AI Safety Datasets Are Not What They Seem (arXiv:2602.16729)](https://arxiv.org/html/2602.16729v1)

<!-- ARCHIVE_END -->

!!! info "References"
    - [Current News](../../docs/news.md)
    - [AIRS Framework Architecture](../../docs/architecture.md)
    - [Controls Overview](../../docs/core/controls.md)
