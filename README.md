# precise-response

A Claude Skill for people on the free tier who keep hitting their usage limit — because most AI answers turn a one-word question into a paragraph.

I'm not a developer. I built this in my first weeks of using Claude, after noticing my daily limit kept running out on things that should've taken one sentence to answer. This isn't a polished engineering tool — it's the fix a beginner built for a beginner's problem.

## Who this is for

- First-time or free-tier users who hit their usage limit before it resets
- People using Claude mostly for planning, decisions, and back-and-forth conversation — not heavy coding
- Anyone tired of scrolling three paragraphs to find the actual "yes" or "no"

**Not for you if:** most of your usage goes into writing or debugging code. Read the caveat below — this skill won't save you anything there.

## Why I built this

On the free tier, I noticed most of my daily limit was going to simple questions — "is X possible?", "which one should I pick?" — coming back as full essays instead of a straight answer. Nothing here is clever engineering. It's just an instruction that tells Claude to match the length of its answer to what the question actually needs, instead of defaulting to "elaborate."

## What it does

- **Concise by default** — direct answers, no preamble, no re-summarizing at the end
- **Smart elaboration** — expands automatically when a short answer would be incomplete or misleading (not based on a fixed list of "complex topics")
- **User toggles** — say "KISS" or "concise mode on" to lock in short answers for the session; say "explain" or "walk me through" for one full-length reply that then reverts
- **Never compresses** — code, scripts, creative writing, legal or financial drafting, or anything you're going to copy and use directly
- **Clarifying questions, done right** — one at a time, plain language, no pop-up or multiple-choice widgets, even during complex scoping work

## ⚠️ Does this save tokens on coding? No.

This skill only shortens *conversational* padding — the chat-style answers you get during planning, discussion, and quick decisions. It does not touch code, scripts, or anything meant to be copied and run; that output stays exactly as long as it needs to be.

If your free-tier limit is mostly getting eaten by coding work, this skill won't move the needle for you. It's built for the planning and discussion side of using Claude — which, in my experience, is where beginners on the free tier lose the most usage to padded answers nobody asked for.

## Illustrative token savings (chat/planning questions only)

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
- These are the question types the skill is *designed* to compress. It intentionally does **not** compress genuinely complex, open-ended, or coding tasks — those come out roughly the same length either way, by design.
- Real savings depend on how much of your usage is quick Q&A versus code or long-form writing. A free-tier user mostly asking planning questions will land closer to the ~90% end; a coding-heavy session will see close to 0% difference.
- The tokenizer above is a standard word-based approximation, not an exact BPE count, because this environment couldn't reach the real tokenizer's remote vocab file. Treat the percentages as directionally accurate, not exact.

## Example

**Without the skill:**
> **Q: Is it possible to build this in React?**
> Yes, it is definitely possible to build this in React! React is a very popular JavaScript library for building user interfaces, and it's well-suited for a wide variety of applications. Depending on your specific requirements, you might also want to consider using additional libraries or frameworks alongside React, such as Redux for state management or React Router for navigation. Let me know if you'd like more details on any particular aspect!

**With the skill:**
> **Q: Is it possible to build this in React?**
> Yes.

---

**Without the skill:**
> **Q: PostgreSQL or MongoDB for this?**
> Both PostgreSQL and MongoDB are excellent database choices, and the right one really depends on your specific use case. PostgreSQL is a relational database that's great for structured data with clear relationships between entities, while MongoDB offers more flexibility for unstructured or rapidly evolving schemas. It also depends on your team's familiarity, scaling needs, and query patterns. Let me know more about your use case and I can give a more tailored recommendation!

**With the skill:**
> **Q: PostgreSQL or MongoDB for this?**
> PostgreSQL — structured data with relations suits it better.

## Install

**Claude.ai / Claude Cowork:** Customize → Skills → "+" → Create skill → upload a ZIP of the `precise-response/` folder (the ZIP's root must be the skill folder itself, not a wrapper folder).

**Claude Code:**
```bash
git clone https://github.com/<your-username>/precise-response-skill.git
cp -r precise-response-skill/precise-response ~/.claude/skills/
```
Start a new session and the skill loads automatically.

## Contributing

PRs welcome — especially more before/after examples, edge cases where the concise/elaborate judgment gets it wrong, or refinements to the clarifying-question rules.

## License

MIT — see [LICENSE](LICENSE).
