# LLM-Based Text-to-SQL Evaluation

This repository contains a team-based academic research project that investigates
how modern Large Language Models (LLMs) translate natural language questions into
SQL queries (Text-to-SQL).

The project focuses on recent LLM-based approaches, evaluation benchmarks, and
representation choices that impact correctness, robustness, and reliability in
real-world database querying scenarios.

---

## Team Project Notice

This repository contains a **team-based university research project**.  
All group members contributed to the final report.

**My primary contributions** focused on the **NatSQL evaluation and analysis**
section, including:
- Designing a zero-shot evaluation comparing NatSQL and standard SQL
- Manually constructing NatSQL equivalents for benchmark queries
- Analyzing structural failure modes and error patterns
- Interpreting discrepancies between published results and zero-shot behavior
- Proposing practical extensions to improve NatSQL reliability

---

## Project Scope

The project explores:
- LLM-based Text-to-SQL systems and recent research directions
- Prompt-based vs fine-tuned approaches
- Evaluation benchmarks such as Spider and robustness-oriented variants
- Representation choices including standard SQL and NatSQL
- Failure modes involving joins, aggregation, schema linking, and nesting

The work combines **literature review**, **partial reproduction**, and
**critical analysis** rather than production deployment.

---

## NatSQL Evaluation (My Focus)

A key component of this project evaluates **NatSQL**, a simplified SQL
intermediate representation designed to better align with natural language.

### Key Finding
In a **zero-shot LLM setting**, standard SQL significantly outperformed NatSQL.
This contrasts with the original NatSQL paper, which reports gains when models
are trained or fine-tuned specifically on the NatSQL representation.

The results suggest that:
- Modern LLMs rely heavily on structural patterns learned from standard SQL
- Removing these cues without targeted supervision harms zero-shot reasoning
- NatSQL benefits primarily from explicit training or few-shot exposure

Detailed evaluation notes are provided in:
- `natsql_reproduction_notes.md`

---

## Repository Contents

- `compiled.pdf`  
  The full compiled research paper (primary artifact for readers)

- `report.tex`  
  LaTeX source used to generate the report

- `natsql_reproduction_notes.md`  
  Individual reproduction notes documenting setup, results, failure modes,
  limitations, and future work for the NatSQL evaluation

- `.gitignore`  
  LaTeX build artifact exclusions

---

## Notes on Reproduction

This project includes **partial reproduction and evaluation**, not full-scale
model training. Limitations include:
- Zero-shot prompting only (no fine-tuning)
- Limited compute and tooling
- Focus on comparative behavior rather than state-of-the-art performance

These constraints are documented intentionally to reflect realistic evaluation
conditions and trade-offs.

---

## Technologies & Topics

- Large Language Models (LLMs)
- Text-to-SQL
- NatSQL
- Prompt engineering
- Evaluation benchmarks (Spider)
- Error analysis and robustness
- LaTeX-based technical writing

---

## How to Read This Repository

If you are short on time:
1. Open `compiled.pdf`
2. Skim the NatSQL section and results
3. Review `natsql_reproduction_notes.md` for detailed analysis

---

## License

This repository is intended for educational and research demonstration purposes.
