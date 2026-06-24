# References

Sources drawn on in this reference. Research papers are cited where their findings are used; standards are cited at released or current-draft status.

## Research papers (arXiv / venues)
- **Image-based Prompt Injection: Hijacking Multimodal LLMs through Visually Embedded Adversarial Instructions**: arXiv:2603.03637 (CSA research note; segmentation-based region selection, adaptive font scaling, background-aware rendering; up to 64% stealth success). Primary source for the embedding-technique taxonomy.
- **MM-SafetyBench**: arXiv:2311.17600 (image+text safety baseline).
- **JailBreakV-28K**: arXiv:2404.03027 (cross-modal jailbreak transfer).
- **AJailBench**: arXiv:2505.15406 (audio jailbreak).
- **SACRED-Bench / SALMONN-Guard**: arXiv:2511.10222.
- **MULTI-AUDIOJAIL**: arXiv:2504.01094 (multilingual/multi-accent audio).
- **Omni-SafetyBench**: text+image+audio, cross-modal consistency / "shortest plank."
- **"Beyond Text" multimodal jailbreak transformations**: arXiv:2510.20223.
- **CASA (Robust Multimodal Safety via Conditional Decoding)**: ResearchGate 403428962.
- **Cross-Agent Multimodal Provenance-Aware Defense Framework**: arXiv:2512.23557.
- **Multi-Agent LLM Defense Pipeline**: arXiv:2509.14285.
- **EchoLeak case study**: arXiv:2509.10540.
- **Preventing Multimodal Cross-Domain Resource Abuse in MCP Tools**: IBM Research.

## Documented incidents / CVEs
- **EchoLeak**: CVE-2025-32711 (Microsoft 365 Copilot zero-click exfiltration).
- **Cursor IDE Mermaid exfiltration**: CVE-2025-54132 (advisory GHSA-xw2x-252g-97w2; fixed v1.3).
- **Image-scaling prompt injection**: Trail of Bits (2025).
- **OpenClaw "Claw Chain"**: Cyera; **OWASP GenAI Exploit Round-up Q1 2026**; **Mindgard** audio jailbreaks.

## Standards and frameworks
- **OWASP AISVS v1.0** (released June 2026): C9 Orchestration & Agentic Security: C9.2.1/C9.2.2 (approval gate + canonical params), C9.2.3/C9.2.4 (trusted reversibility classification + runtime enforcement), C9.2.10 (worst-case chain rule), C9.4 (agent identity), C9.5 (authorization/enforcement); C2 (input validation).
- **OWASP LLM Top 10 (2025)**: LLM01 Prompt Injection, LLM02 Sensitive Information Disclosure, LLM06 Excessive Agency.
- **CSA**: Image-Based Prompt Injection research note (Mar 2026); AI Controls Matrix (AICM); Agentic Trust Framework (Public Review Draft); NHI four-element attribution (CSA IAM WG; v1.0 anchor para 222) and six-property chain-audit schema (v2.0 target, under review; joint Mallikarjunarao Sunke).
- **NIST**: AI RMF 1.0 (AI 100-1); Generative AI Profile (AI 600-1); SP 800-53 Rev. 5 (AC, AU, SI families, SI-10); SP 800-207 (Zero Trust Architecture).
- **MITRE ATLAS**: AML.T0051 (LLM Prompt Injection), AML.T0099 (AI Agent Tool Data Poisoning).
- **EU AI Act**: Article 14 (human oversight).
- **CoSAI WS4**: Tool Design for Secure Agentic Systems (Donadei, Goodman, Molloy, Kale), Principle 4 (Secure Agentic Patterns / Two-Stage Commit) and Principle 5 (per-tool immutable audit trail); [RFC] Multimodal Agentic Security #113 (Shriti Priya).

## Author's prior work (this contribution builds on)
- **Action-Class Authority: A Verification-Layer Pattern for Agentic AI Security** (Mayur Agnihotri, IEEE S&P magazine draft): threat models (Codex, Meta IG, Red Hat npm) and the action-class / worst-case-chain pattern.
- Action-Class Authority whitepaper; Reachability Is Only Half the Blast Radius (Agentic Zero Trust).

> Citation discipline: AISVS at released v1.0 numbers; CSA NHI six-property schema marked v2.0-targeted/under-review; MITRE ATLAS ids verified except where flagged in STANDARDS_CROSSWALK.md.
