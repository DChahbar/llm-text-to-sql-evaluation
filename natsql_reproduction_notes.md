# NatSQL Reproduction and Evaluation Notes

## Scope
These notes document my individual contribution to a team-based research project
focused on evaluating NatSQL, a simplified SQL intermediate representation, when
used with modern large language models (LLMs).

The goal of this work was to assess whether NatSQL improves Text-to-SQL performance
in a zero-shot LLM setting and to analyze failure modes relative to standard SQL
generation.

---

## Evaluation Setup
- Dataset: Spider (development split)
- Number of questions evaluated: 250
- Model usage: Zero-shot prompting with a modern LLM
- Training: No fine-tuning or adapters applied
- NatSQL enforcement: Prompt-level instructions only
- Evaluation focus: Correctness and structural validity of generated queries

NatSQL queries were manually constructed following the rules defined in the original
NatSQL paper and compared against standard SQL outputs generated under the same
zero-shot conditions.

---

## Key Results
Standard SQL significantly outperformed NatSQL in the zero-shot setting.

- Standard SQL accuracy: ~84%
- NatSQL accuracy: ~53%

This outcome contrasts with the original NatSQL paper, which reports improvements
when models are trained or fine-tuned to generate NatSQL.

The results indicate that NatSQL does not provide immediate benefits when used
without targeted supervision.

---

## Observed Failure Modes
NatSQL failures were more frequent and structurally severe than SQL failures.
Common error patterns included:

- Incorrect or missing join inference due to the removal of explicit JOIN clauses
- Reintroduction of disallowed SQL constructs (GROUP BY, HAVING, nested SELECTs)
- Loss of structural cues needed for aggregation and grouping logic
- Schema inference failures and incorrect table/column associations
- Improper flattening of nested semantics

By contrast, standard SQL failures were typically limited to ambiguous joins or
occasional hallucinated schema elements.

---

## Interpretation
The results suggest that modern LLMs rely heavily on structural patterns learned from
standard SQL during pretraining. Removing these cues, as NatSQL does, negatively
impacts zero-shot reasoning.

NatSQL’s advantages appear to depend on:
- Explicit training on the NatSQL representation, or
- Strong few-shot demonstrations that expose the model to NatSQL syntax and semantics

Without this exposure, NatSQL simplifies the query space in a way that removes
important reasoning anchors for the model.

---

## Limitations
- No fine-tuning or supervised training was performed
- Evaluation was limited to a zero-shot prompting setting
- Compute and tooling constraints prevented large-scale training experiments
- Results focus on relative behavior rather than absolute state-of-the-art performance

---

## Future Work
Potential extensions to improve NatSQL performance include:

- Few-shot NatSQL prompting with high-quality demonstrations
- Hybrid pipelines combining SQL generation with NatSQL post-processing
- Schema-aware retrieval or schema linking to support join inference
- Lightweight fine-tuning or adapter-based approaches for NatSQL exposure

---

## Summary
This reproduction demonstrates that NatSQL does not outperform standard SQL in
zero-shot LLM settings, highlighting the importance of representation familiarity and
training distribution when designing Text-to-SQL systems.
