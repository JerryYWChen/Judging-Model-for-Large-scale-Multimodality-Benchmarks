# Judging Model for Large-scale Multimodality Benchmarks

## Overview
This project presents a research-oriented evaluation framework for assessing large multimodal language models (MLLMs) across text, image, audio, and video tasks.  
Rather than relying on single-score accuracy, the framework focuses on reasoning consistency, hallucination detection, and reproducibility through structured, rubric-based evaluation.

The system is designed to serve as a scalable and interpretable alternative to human evaluation for large-scale multimodal benchmarks.

---

## Motivation
Recent advances in MLLMs have significantly expanded model capabilities across modalities, but evaluating these models remains challenging. Existing approaches often suffer from one or more of the following limitations:

- Heavy reliance on expensive and inconsistent human annotation  
- Text-only judges that fail to capture multimodal reasoning errors  
- Static benchmarks with unclear train–test leakage risks  
- Overemphasis on final answers without inspecting reasoning quality  

This project aims to address these gaps by introducing a multimodal-aware judge framework that evaluates both answers and their justifications in a reproducible manner.

---

## System Pipeline
The evaluation pipeline operates as follows:

![Multimodal Evaluation Pipeline](ml_System_Infrastructure.png)

1. Multimodal inputs (text, image, audio, or video) are sampled from held-out evaluation splits with fixed random seeds.  
2. Each tested MLLM generates an answer along with a justification.  
3. A multimodal judge model evaluates the response using the original input, ground-truth references, and task instructions.  
4. The judge outputs a structured evaluation including a numerical score, an error category, and a natural-language explanation.

---

## Evaluation Design
The judge model is explicitly prompted to perform multimodal reasoning and focuses on three complementary objectives:

- **Response Quality**: Whether the final answer matches the ground truth or observable reality.  
- **Reasoning Consistency**: Whether the provided justification logically supports the answer without hallucination.  
- **Diagnostic Feedback**: Identification of specific failure modes rather than binary correctness.

Evaluations are conducted using a Likert-style scoring rubric (0–5), combined with explicit error categorization such as hallucination, false refusal, or reasoning inconsistency.

To ensure reproducibility, all datasets are sampled from clearly specified evaluation splits with fixed random seeds.

---

## Example Output
Instead of producing a single scalar score, the judge returns structured diagnostic feedback.  
A representative output is shown below:

```json
{
  "final_score": 3,
  "error_type": "visual_hallucination",
  "explanation": "The model mentions chart labels that are not present in the image."
}
'''

## Relation to Paper

This repository documents the methodology and research artifacts associated with the paper:

Judging Model for Large-scale Multimodality Benchmarks
(arXiv:2601.06106)

Due to collaborative research constraints and the use of proprietary model APIs, the full implementation is not publicly released.
However, this repository provides a transparent view of the system design, evaluation logic, and experimental principles underlying the study.
