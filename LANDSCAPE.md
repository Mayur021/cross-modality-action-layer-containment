# Multimodal Agentic Security: Landscape Index

A curated, cited index of the public multimodal-agentic-security landscape (2025-2026), compiled as context for the action-layer contribution in this repo. The authoritative community treatment is the **CoSAI WS4 [RFC] Multimodal Agentic Security (#113)** by Shriti Priya; this index is a reference, not a substitute.

## Attack surfaces by modality

![Figure 2: Multimodal attack surfaces across image, audio, and video, sharing four embedding families and converging on the action-layer gate.](figures/fig2-multimodal-attack-surfaces.png)

*Figure 2. Multimodal Attack Surfaces (image / audio / video).*

- **Image**: visually embedded text (typographic), steganographic payloads, adversarial perturbations on the vision encoder, and preprocessing/image-scaling exploits. Provenance ambiguity (trusted instruction vs content-in-an-image).
- **Video**: rendered text in frames, single-frame/temporal hiding, embedded audio track, adversarial perturbations.
- **Audio**: text-filter bypass via transcription, psychoacoustic/hidden-voice commands, physical-world delivery (DolphinAttack/ultrasonic), transient/unverifiable payloads, speaker/identity confusion.
- **Location / geospatial, document/file (OCR), code/structured-data**: underdeveloped in current public work; named here as open surfaces.

## Embedding-technique taxonomy (four families)
Typographic, steganographic, adversarial perturbation, preprocessing exploit. A defense for one offers little protection against another. See `ATTACK_AND_DEFENSE_TAXONOMY.md`.

## Documented incidents
- **EchoLeak (CVE-2025-32711, Microsoft 365 Copilot)**: zero-click data exfiltration; auto-fetched markdown images, allowlisted-proxy egress, link-redaction bypass.
- **Cursor IDE Mermaid exfiltration (CVE-2025-54132)**: secrets encoded into a Mermaid diagram image URL; fixed v1.3 by stripping remote images (later bypasses found).
- **Image-scaling prompt injection (Trail of Bits, 2025)**: benign at full resolution, malicious after downscale; Calendar-data exfiltration demonstrated.

## Benchmarks
- **MM-SafetyBench** (image+text), **JailBreakV-28K** (cross-modal transfer), **Arondight** (automated red-teaming), **Omni-SafetyBench** (text+image+audio, cross-modal consistency / "shortest plank").

## Mitigation tiers
1. **Input-side (per modality):** decode-then-scan (OCR/transcribe), validate the processed artifact, input transformation, adversarial robustness, query-aware sanitized descriptions.
2. **Model-side:** alignment/RL to ignore embedded instructions, modality-aware guard models.
3. **Architectural/agentic:** provenance and trust labeling, prompt partitioning, egress control, cross-agent isolation.
4. **Least-privilege and HITL:** narrow credentials, approval for high-impact actions, content-security policy on reachable domains.
5. **Action-layer floor (the backstop, this repo's contribution):** action-class gating + worst-case chain rule + chain-level audit. Modality-independent; holds when tiers 1-4 leak. See `SECTION_cross_modality_action_layer_containment.md`.

## Resource exhaustion
MCP tool arguments as a resource-abuse surface across modalities (IBM, "Preventing Multimodal Cross-Domain Resource Abuse in MCP Tools").

## Key references
- CSA Image-Based Prompt Injection note / arXiv 2603.03637
- EchoLeak CVE-2025-32711 ; Cursor CVE-2025-54132 (GHSA-43wj-mwcc-x93p)
- MM-SafetyBench (2311.17600), JailBreakV-28K (2404.03027), Omni-SafetyBench
- OWASP AISVS v1.0 ; OWASP LLM Top 10 (2025) ; CSA AICM ; CSA Agentic Trust Framework ; NIST AI RMF + SP 800-53 ; MITRE ATLAS
