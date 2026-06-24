# Standards Cross-Walk: Multimodal Action Layer

Attack to defense, mapped across OWASP, CSA, NIST, and MITRE ATLAS. AISVS controls are the released v1.0 numbers.

| Concern (attack -> defense) | OWASP | CSA | NIST | MITRE ATLAS |
|---|---|---|---|---|
| Multimodal prompt injection (image/audio/video carries the instruction) | LLM01 Prompt Injection (LLM Top 10 2025); AISVS C2 input validation | Image-Based Prompt Injection note (Mar 2026); AICM TVM domain | AI RMF GenAI Profile (AI 600-1); SP 800-53 SI-10 | AML.T0051 LLM Prompt Injection |
| Cross-modality composition / chained exfil (each step permitted, chain irreversible) | LLM06 Excessive Agency + LLM02 Sensitive Info Disclosure | Agentic Trust Framework (action boundaries) | SP 800-53 AC-3 / AC-4 | Exfiltration tactic (verify exact AML id) |
| Agent self-classification (injection relabels the action) | AISVS C9.2.3 (trusted, not agent-asserted) | Agentic Trust Framework (governed actor) | AI RMF MAP / MEASURE | AML.T0099 AI Agent Tool Data Poisoning |
| Action gating by reversibility (defense) | AISVS C9.2.3 + C9.2.4 | Agentic Trust Framework S-2 Action Boundaries | SP 800-53 AC family | -- |
| Worst-case chain gate (defense) | AISVS C9.2.10 | (CSAI Foundation AARM worst-case, adjacent) | -- | -- |
| Chain-level audit / attribution (defense) | AISVS C9.4 (agent identity, non-repudiation) | CSA NHI four-element attribution (v1.0 anchor, para 222) + six-property chain audit (v2.0 target, under CSA IAM WG review; joint Mallikarjunarao Sunke) | SP 800-53 AU family | -- |
| HITL / Two-Stage Commit for irreversible (defense) | AISVS C9.2.1 + C9.2.2 | Agentic Trust Framework; WS4 Tool Design guide Principle 4 | AI RMF human oversight; EU AI Act Art 14 | -- |
| Input provenance / trust labeling (defense) | AISVS C9.5 (delegation context) | CSA NHI four-element (delegator / agent / intent / actions) | AI RMF GOVERN (provenance) | -- |

## What the cross-walk reveals
1. Per-modality input attacks are well covered across all bodies.
2. The composition / worst-case-chain row has exactly one normative anchor: OWASP AISVS v1.0 C9.2.10. No NIST or CSA control names "the chain is gated by its worst-case action." Multimodal makes that gap acute.
3. The CSA note itself flags that AICM has no dedicated multimodal-input-validation control category, recommending the adversarial-robustness controls be read to include typographic, steganographic, and perturbation image injection.
