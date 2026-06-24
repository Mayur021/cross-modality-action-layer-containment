# Cross-Modality Action-Layer Containment

> Drafted contribution for CoSAI WS4 RFC #113 (Multimodal Agentic Security). Mayur's lane: the
> modality-independent action-layer backstop, complementary to the per-modality input sections.
> Citations verified against released OWASP AISVS v1.0 (C9.2.3 / C9.2.4 / C9.2.10). Source threat
> models adapted from the author's IEEE S&P "Action-Class Authority" paper. NOT a standalone
> multimodal-security paper (that is monshri's RFC); this is the action-layer section only.

The defenses in the preceding sections operate at the input: they decode, scan, and harden each modality before the model reads it. Those defenses are necessary, and they are never complete, because every new modality opens a channel the input scanners were not built to inspect, and the strongest documented attacks succeed precisely by entering through the modality whose coverage is weakest. This section describes the layer that holds when an input defense fails: the action layer, which is the same regardless of which modality carried the injection.

## Attack motivation

The harm in a multimodal agentic exploit does not land in the modality. It lands at the tool layer, through a chain. An injection enters through one modality, and the agent then composes a sequence of individually permitted tool calls that reaches an irreversible outcome. EchoLeak is the canonical multimodal instance: a crafted email coerces the agent, an auto-fetched markdown image provides the egress channel, and the composed chain exfiltrates sensitive context through an allowlisted URL, with every step passing its own authorization. Image-scaling injection is the same shape with a different entry point: an image that is benign at full resolution reveals an instruction after downscaling, and the agent acts on it.

The structural property these share is that authorization is evaluated per step while the danger is a property of the composition. A chain such as read user email (read-only), identify accounts (read-only), initiate password reset (external-reversible), modify credentials (irreversible) is irreversible from the moment the first step executes, not at the final step. Per-step gates, and per-modality scanners, each see only a slice. The same gap appears outside multimodal entirely: OpenAI's Codex agent chained four legitimate operations (enumerate group membership, recognize docker as root-equivalent, construct a bind-mount, write to /etc on the live host) into a system-irreversible result, each operation permitted by the tool authority. The composition failure is identical whether the entry point is an image, an audio clip, or a typed instruction.

A second property compounds it. When the same agent both proposes an action and reasons about its risk, an injection from any modality can cause the agent to mislabel an irreversible action as safe, and a gate that trusts the agent's runtime reasoning will permit it. The injection channel is modality-specific; the failure mode, agent-reasoning-as-boundary, is not. Finally, attribution stops short: a multimodal-to-tool exfiltration chain today traces back to "a model processed an image," not to a real originating principal, which leaves the incident unattributable.

## Defense: a modality-independent action-layer floor

Because the harm is at the action layer, the containment belongs there too, and it does not need to know the modality. Three primitives, all modality-agnostic.

Classify each action by reversibility, declared at design time and trusted by the gate rather than derived from the agent's runtime reasoning, and enforce by that class at execution. OWASP AISVS v1.0 names this as C9.2.3 (a trusted reversibility classification: read-only, reversible, externally reversible, irreversible) and C9.2.4 (runtime enforcement by class). Because the class is set at design time and the agent cannot rewrite it, an injection that corrupts the agent's reasoning through any modality cannot relabel the action to clear its own gate. This is the structural difference from modality-aware guard models, which are valuable above the gate but inherit the same injection surface they are meant to catch.

Gate the composed chain on its worst-case action. AISVS v1.0 C9.2.10 requires that an approval gate for a multi-step or multi-agent chain enforce the highest-impact reversibility class present anywhere in the chain, so a chain that composes individually low-risk steps across modalities into an irreversible end fails the gate at chain start. This is the control that catches EchoLeak-class composition that per-step and per-modality checks miss, and the Tool Design guide's Two-Stage Commit pattern (Principle 4) is the human-approval expression of it for the external-reversible and irreversible classes.

Carry a chain-level audit record so the outcome is attributable. A six-property schema (chain id linking the composed steps, declared worst-case action class at chain start, gate decision and justification, per-step API record, originating principal, and immutability of the originating principal) makes a multimodal-to-tool exfiltration attributable to a real actor rather than stopping at the model. This schema is a joint peer-review contribution with Mallikarjunarao Sunke, currently under CSA Identity and Access Management Working Group review; the per-step API record corresponds to the per-tool immutable audit trail in Principle 5 of the Tool Design guide, and the chain id and worst-case class are the additions the multimodal case requires.

## Relationship to the per-modality sections

These primitives sit one layer beneath the per-tool authorization the Tool Design guide already covers, and they are modality-agnostic, so the same gate decision applies whether the chain composes across image, audio, video, or text. They do not replace the input-side defenses; they are the backstop that holds when an input defense fails, which, given that every new modality is a new channel, it eventually will.
