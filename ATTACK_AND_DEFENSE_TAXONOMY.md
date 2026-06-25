# Attack and Defense Taxonomy

The multimodal injection-to-exfiltration attack is the product of two independent choices: how the instruction is embedded, and how the data leaves. Filtering one ingress family or patching one egress channel leaves every other combination open.

## Attack taxonomy

![Figure 2: Multimodal attack surfaces across image, audio, and video, sharing four embedding families and converging on the action-layer gate.](figures/fig2-multimodal-attack-surfaces.png)

*Figure 2. Multimodal Attack Surfaces (image / audio / video).*


### Axis A: how the instruction is embedded (ingress)
| Technique | How it hides | Catches it / what does not |
|---|---|---|
| Typographic / visible-text | readable text in pixels (low-contrast, tiny font, blended; segmentation + adaptive-font + background-aware rendering per the CSA note) | OCR catches; the human reviewer misses |
| Steganographic | payload in pixel/sample data, not visible text | needs steganalysis; OCR misses |
| Adversarial perturbation | gradient-crafted noise targeting the vision/audio encoder, no readable text | input transformation / robustness; OCR misses |
| Preprocessing exploit (image-scaling) | payload appears only after downscale/transcode | scan the processed artifact; full-resolution scan misses |

The CSA research note (arXiv 2603.03637) reports up to 64% attack success under stealth constraints, so ingress filtering is leaky by design.

### Axis B: how the data leaves (egress)
| Channel | Example |
|---|---|
| Auto-fetched remote image (Mermaid / markdown image URL) | Cursor (CVE-2025-54132), EchoLeak |
| Allowlisted-proxy egress | EchoLeak (Teams URL); the `*.azure.net` logging-endpoint bypass |
| Tool-call egress (send email / API with embedded data) | image-scaling to Calendar exfil |
| Reference-style markdown / link-redaction bypass | EchoLeak |

The attack = (one Axis-A technique) x (one Axis-B channel).

## Defense taxonomy

![Figure 1: Cross-modality action-layer containment. Ingress filtering is leaky; the action-layer gate (AISVS v1.0 C9.2.3, C9.2.4, C9.2.10) is the modality-independent chokepoint.](figures/fig1-action-layer-containment.png)

*Figure 1. Cross-Modality Action-Layer Containment.*

| Layer | Controls | Catches | Leaks |
|---|---|---|---|
| 1. Ingress filtering | OCR decode-then-scan; steganalysis; input transformation (re-encode/blur/resample); scan the post-downscale artifact; query-aware sanitized image descriptions | the technique each is tuned for | no single filter covers all four families; ~64% stealth success |
| 2. Model-side | alignment/RL to ignore embedded instructions; modality-aware guard models | many cases | guard models inherit the same injection surface they screen |
| 3. Egress control | strip remote images before render (Cursor v1.3); egress allowlist; CSP; output secret/PII scan | the specific channel patched | whack-a-mole; Cursor's fix had bypasses; allowlists break on broad domains (`*.azure.net`) |
| 4. Action-layer floor (modality-independent) | classify external data egress as a gated action class (external-reversible / irreversible); worst-case chain gate; HITL for non-allowlisted egress | any ingress x any egress, because it gates the action not the channel | requires design-time action-class declaration |

## The load-bearing conclusion
You cannot fully filter the ingress: OCR catches only typographic text, steganographic and perturbation payloads carry no readable text, and stealth success stays high. Egress patches are per-channel whack-a-mole. The durable control is at the egress/action layer: treat "send data to a destination the policy did not pre-approve" as a high-impact action class, gated regardless of which modality or channel triggered it. Once external exfiltration is classified external-reversible / irreversible and the chain is gated on its worst case, it does not matter whether the instruction arrived as visible text, a steganographic payload, or a perturbation, nor whether the channel is a Mermaid URL, a markdown image, or a tool call. The text-modality filter is necessary but leaky; the egress action gate is the one that holds.

## Sources
- CSA Image-Based Prompt Injection note / arXiv 2603.03637
- Cursor Mermaid exfiltration, CVE-2025-54132 (advisory GHSA-43wj-mwcc-x93p)
- EchoLeak, CVE-2025-32711
