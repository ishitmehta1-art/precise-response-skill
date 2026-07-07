# precise-response

A Claude Skill that stops Claude from padding simple answers. It calibrates response length to what the question actually needs — concise by default, fully elaborate only when the task genuinely requires it — and enforces that clarifying questions are asked one at a time, in plain language, with no pop-up/multiple-choice widgets.

## Why

Ask a closed or simple question and you often get a paragraph of preamble, restated context, and a summary at the end, even when a sentence would do. This skill makes Claude answer directly for closed/simple/comparison/estimation questions, and reserves full explanations for cases that are genuinely open-ended or complex.

## What it does

- **Concise by default** — direct answers, no preamble, no re-summarizing, minimal formatting for short answers
- **Smart elaboration** — expands automatically when a short answer would be incomplete or misleading (not based on a fixed topic list)
- **User toggles** — say "KISS" / "concise mode on" to lock in short answers for the session; say "explain" / "walk me through" for one full-length reply that then reverts
- **Never compresses** — code, scripts, creative writing, legal/financial drafting, or anything you'll copy and use directly
- **Clarifying questions, done right** — one question at a time, plain language, no pop-up/button widgets, ever — even during complex scoping work

## Illustrative token savings

Five representative closed/simple questions, written both as a typical unconstrained answer and as this skill would answer them, counted with an approximate English tokenizer (~1.3 tokens/word):

| Question type | Unconstrained | With skill | Reduction |
|---|---|---|---|
| Yes/no | 150 | 3 | 98.0% |
| Closed factual | 150 | 13 | 91.3% |
| Estimation | 135 | 26 | 80.7% |
| Comparison | 164 | 13 | 92.1% |
| Follow-up | 94 | 12 | 87.2% |
| **Total** | **693** | **67** | **90.3%** |

**Read this honestly, not as a universal number:**
- These are the question types the skill is *designed* to compress (MODE 1). It intentionally does **not** compress genuinely complex or open-ended tasks (MODE 2) — those come out roughly the same length either way, by design.
- Real savings across a full conversation depend on the mix of simple vs. complex turns. A planning session that's mostly quick decisions and estimates will land closer to the ~90% end; one dominated by requests for full write-ups or code will see much less.
- The tokenizer above is a standard word-based approximation (not an exact BPE count), used because this environment couldn't reach the real tokenizer's remote vocab file. Treat the percentages as directionally accurate, not exact.

## Install

**Claude.ai / Claude Cowork:** Customize → Skills → "+" → Create skill → upload a ZIP of the `precise-response/` folder (the ZIP's root must be the skill folder itself, not a wrapper folder).

**Claude Code:**
```bash
git clone https://github.com/<your-username>/precise-response-skill.git
cp -r precise-response-skill/precise-response ~/.claude/skills/
```
Start a new session and the skill loads automatically.

## Contributing

PRs welcome — especially more before/after examples, edge cases the concise/elaborate judgment gets wrong, or refinements to the clarifying-question rules.

## License

MIT — see [LICENSE](LICENSE).
