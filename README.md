# Claim-Verified Multi-Hop RAG: Measuring Hallucination Propagation Across Retrieval Steps

This repository contains a class project for DATASCI 266 (UC Berkeley) studying how unsupported intermediate reasoning in multi-hop Retrieval-Augmented Generation (RAG) affects final QA correctness.

## Project Goal

We evaluate whether hallucinations at intermediate hops propagate into downstream retrieval/generation errors, and whether verifier-guided intervention can reduce this failure mode.

## Pipelines

1. **Pipeline 1: Naive Single-Pass RAG**
   - One retrieval step, direct answer generation.
   - Baseline for comparison.

2. **Pipeline 2: Multi-Hop RAG**
   - Question decomposition into sequential sub-questions.
   - Hop-wise retrieval and chained generation.
   - Post-hoc grounding analysis using a calibrated verifier.

3. **Pipeline 3: Verifier-Guided Multi-Hop RAG**
   - Same multi-hop backbone as Pipeline 2.
   - Per-hop verification and targeted intervention on unsupported hops.

## Key Files

- `Claim-Verified-Multi-Hop RAG-Measuring-Hallucination-Propagation-Across-Retrieval-Steps.pdf` (Final Report)
- `Pipeline_1_Naive_Single_Pass_RAG_(Baseline).ipynb`
- `Pipeline_2_Multi_Hop_RAG.ipynb`
- `Pipeline_3_Claim_Verified_Multi_Hop_RAG.ipynb`

## Report

The final project report is available here: [Claim-Verified Multi-Hop RAG: Measuring Hallucination Propagation Across Retrieval Steps](Claim-Verified-Multi-Hop%20RAG-Measuring-Hallucination-Propagation-Across-Retrieval-Steps.pdf)

## Data and Evaluation

- Dataset: **HotpotQA distractor setting**, restricted to bridge questions.
- Shared evaluation subset: **2,000 examples** (seeded sampling).
- Core metrics:
  - Exact Match (EM), Token-F1
  - Retrieval Recall@k (soft/strict)
  - Abstention rate
  - Hop-level grounding diagnostics (Pipelines 2/3)

## Summary of Findings

- **Multi-hop Success:** Decomposition significantly improves strict retrieval recall (from 46.1% to 69.5%) and final-answer accuracy over the single-pass baseline.
- **The Grounding Gap:** Unsupported intermediate reasoning is prevalent. In the multi-hop baseline, **60.9% of correct answers** relied on at least one unsupported hop, demonstrating a frequent tendency to be "right for the wrong reason."
- **Parametric Resilience:** The "propagation penalty" for early hallucinations is limited (+0.0313 EM drop). This suggests models often fallback to internal parametric knowledge to rescue answers when the evidence chain is broken.
- **Verification as Reliability:** Verifier-guided intervention successfully shifts the system toward higher faithfulness by significantly reducing ungrounded reasoning steps, proving that per-hop auditing is a vital reliability mechanism even when end-task accuracy gains are modest.

## Reproducibility Notes

- Notebooks were developed in Google Colab.
- Some cells expect mounted Google Drive paths and saved artifacts.
- API-backed generation and model downloads may require credentials and environment setup.

## GenAI Citation
Portions of writing revision (Gemini Flash 3), Latex formatting support (Gemini Flash 3), and code debugging (Claude Sonnet 4.6 and Codex 5.3) were assisted by generative AI tools. All experimental design decisions, implementation choices, result interpretation, and final manuscript content were created by the author.

