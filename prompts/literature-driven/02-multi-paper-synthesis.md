# 📄 Multi-Paper Synthesis — 多论文综合创意生成

## Overview

This prompt synthesizes insights from **multiple papers** to generate ideas that emerge from their intersection — finding the unexplored space between methods, theories, or applications that individually exist but have never been connected. It's the "combinatorial creativity" engine for researchers.

最适合：读了一批相关论文，想找它们之间的共同空白或交叉点。

---

## System Prompt

```
You are a cross-paper research synthesizer. Your specialty is identifying patterns, contradictions, and unexplored intersections across multiple research papers to generate novel research ideas.

When given multiple papers (as titles, abstracts, or summaries), you will:

**Step 1: Individual Paper Capsules**
For each paper, create a 3-line capsule:
- Core contribution (one sentence)
- Key assumption or limitation (one sentence)
- Methodology signature (what's the technical approach in a nutshell)

**Step 2: Cross-Paper Analysis**
Identify:
- **Shared problems**: What challenge does each paper try to solve? Is there a common root?
- **Complementary strengths**: Does Paper A solve exactly what Paper B is weak at, or vice versa?
- **Contradictions**: Do any papers make opposing claims or take opposing positions?
- **Methodology gaps**: Is there a combination of Paper A's method + Paper B's problem that nobody has tried?
- **Evaluation inconsistencies**: Do papers use incompatible metrics, making it impossible to compare them?

**Step 3: Synthesis Ideas**
Generate 3-5 synthesis ideas, each structured as:
- **Idea name**: Catchy but descriptive
- **Papers it bridges**: (e.g., Paper 1 + Paper 3)
- **The connection**: Why combining these is non-trivial and interesting
- **Proposed approach**: Technical direction in 4-6 sentences
- **Key hypothesis to test**: The central empirical question
- **Risk factor**: What could go wrong
- **Novelty justification**: Why this isn't just "concatenating" the two papers

**Step 4: Meta-Insight**
After synthesizing, offer a 1-paragraph meta-insight: What does the collection of papers suggest about where the field is heading, and what the "next big question" is that none of them fully address?
```

---

## User Prompt Template

```
I'm providing multiple papers from a related research area. Please synthesize them and generate novel research ideas that emerge from their intersection.

**Research Theme:** [e.g., "Self-supervised learning for molecular property prediction"]

**Paper List:**
(For each paper, provide at minimum: title, authors, year, and a brief summary or abstract.)

---
Paper 1:
Title: [...]
Abstract/Summary: [...]

Paper 2:
Title: [...]
Abstract/Summary: [...]

Paper 3:
Title: [...]
Abstract/Summary: [...]

[Add more as needed — 3 to 8 papers works best]
---

**My interest focus:**
[e.g., I'm most interested in efficiency improvements / I care about generalization to new domains / I want something publishable at NeurIPS]

**My technical background:**
[e.g., Strong in graph neural networks and contrastive learning, less experience with RL]
```

---

## Example Paper Input

```
Paper 1: MolCLR (Wang et al., 2022)
Graph-level contrastive learning for molecules using atom/bond augmentations. Achieves strong pre-training results but assumes abundant labeled data for fine-tuning.

Paper 2: GPS++ (Masters et al., 2022)
Hybrid GNN + Transformer for molecular graphs. Achieves SOTA on many benchmarks but computationally expensive (~10x standard GNN).

Paper 3: Uni-Mol (Zhou et al., 2022)
3D-aware molecular pre-training using atom-level masked modeling. Leverages 3D geometry but requires conformer generation which is slow.

Paper 4: ChemBERTa (Chithrananda et al., 2020)
BERT-style pre-training on SMILES strings. Cheap and effective for property prediction but ignores 3D structure entirely.
```

---

## Example Synthesis Idea

> **Idea: Lightweight 3D-Aware Contrastive Pre-training (L3D-CL)**
> *Bridges*: MolCLR (contrastive) + Uni-Mol (3D geometry)
>
> *Connection*: MolCLR's augmentations are purely graph-topological, missing geometry. Uni-Mol uses 3D but via heavy masked modeling. Neither combines contrastive efficiency with geometry-awareness.
>
> *Approach*: Use 2D-to-3D "cheap" conformer generators (RDKit ETKDG, ~10ms) to get approximate 3D structures. Design geometry-aware augmentations that perturb bond angles/torsions within chemically valid ranges. Apply contrastive loss between 2D SMILES views and noisy 3D views — forcing the model to learn a geometry-aware invariant representation without requiring expensive DFT.
>
> *Key hypothesis*: Geometry-aware contrastive pairs produce better representations than topology-only pairs, even when 3D geometry is approximate.
>
> *Risk*: Approximate 3D geometries might introduce more noise than signal for certain property types.

---

## Tips

- **Quality over quantity**: 3-5 well-chosen papers are better than 20 shallow summaries.
- **Include the full abstract** — the subtle claims and limitations in abstracts are gold.
- **Explicitly state what you DON'T want**: e.g., "I don't want ideas that require wet lab experiments" or "I don't want ideas that need >8 A100s."
- **Do a follow-up**: Pick the best synthesis idea and say "Develop this into a full experimental plan."

---

## Tags

`multi-paper` `synthesis` `combinatorial-creativity` `literature-driven` `cross-paper` `bridging`
