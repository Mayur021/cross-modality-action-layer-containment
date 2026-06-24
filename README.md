# Cross-Modality Action-Layer Containment

A verification-side reference for the **modality-independent action layer** in multimodal agentic AI security.

## What this is
When an AI agent perceives and acts across text, images, audio, and video, each modality opens an input attack surface that text defenses do not see. Per-modality input filtering is necessary and never complete. This reference documents the layer that holds when an input defense fails: the **action layer**, which is the same regardless of which modality carried the injection.

It anchors on three primitives, all modality-agnostic:
- **Action-class gating** by reversibility (OWASP AISVS v1.0 **C9.2.3** + **C9.2.4**)
- **Worst-case chain rule** for composed multi-step chains (OWASP AISVS v1.0 **C9.2.10**)
- **Chain-level audit** for attribution (six-property schema, joint peer-review work with Mallikarjunarao Sunke, under CSA IAM WG review)

## What this is NOT
- **Not** a multimodal-security standard or guide. The community RFC for that is **CoSAI WS4 [RFC] Multimodal Agentic Security (#113)** by Shriti Priya. This reference is the **action-layer section / companion** to that work, complementary to its per-modality input defenses, not a replacement.
- Not a vendor product specification.

## Landscape
A cited index of the full multimodal-agentic-security landscape (attack surfaces, incidents, benchmarks, mitigation tiers) is in `LANDSCAPE.md`. The action-layer floor is tier 5 / the backstop.

## Contents
- `SECTION_cross_modality_action_layer_containment.md` — the drafted action-layer section (attack motivation + defense).
- `ATTACK_AND_DEFENSE_TAXONOMY.md` — two-axis attack taxonomy (embedding technique x egress channel) and four-layer defense taxonomy.
- `LANDSCAPE.md` — cited index of the full public landscape (attack surfaces, incidents, benchmarks, mitigations).
- `STANDARDS_CROSSWALK.md` — mapping to OWASP, CSA, NIST, MITRE ATLAS.
- `figures/` — original diagrams (CC BY 4.0).

## Citation discipline
AISVS controls are cited at their **released v1.0 numbers** (C9.2.3 / C9.2.4 / C9.2.10, C9 Orchestration & Agentic Security chapter). The CSA NHI six-property chain-audit schema is a v2.0-targeted joint contribution **under CSA IAM WG review**; the v1.0 anchor is the four-element attribution at paragraph 222.

## License
Creative Commons Attribution 4.0 (CC BY 4.0).
