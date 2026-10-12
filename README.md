# Exam writing

An agent skill for writing, reviewing and versioning classroom exams. It turns published research on test items into a workflow your coding agent follows, from planning the exam to reading the results after students take it.

The skill is written in English, and it works for exams in any language.

## Install

```bash
npx skills add danihrndzld/exam-writing
```

The command works with Claude Code, Codex, Cursor and the other agents that the [skills CLI](https://github.com/vercel-labs/skills) supports.

## What it does

- Builds a table of specifications before any item is written, so the exam covers the objectives at the right cognitive level.
- Writes multiple choice, short answer and matching items that follow 31 published item-writing guidelines and the NBME item-writing guide.
- Reviews a draft exam with a checklist of 25 yes/no checks and a blind-solve pass, where a fresh agent takes the exam without the key and reports items with two answers or giveaway cues.
- Makes parallel versions by shuffling items and options, balancing the key letter, and cloning items with the same skill and difficulty.
- Reads item analysis after the exam (difficulty, point-biserial, distractors nobody chose), with caveats for small classes.

## How it works

The agent works through these steps in order:

1. It builds a grid of learning objectives by cognitive level, with the number of items and points in each cell.
2. It writes each item for one cell and tags the item with that cell.
3. It runs the pre-print checklist and lists every failed check with a fix.
4. It hands the exam, without the key, to a fresh subagent, which answers every item and flags ambiguities, missing data and cues. The agent then compares those answers with the key and fixes the items that disagree.
5. If you ask for parallel versions, it shuffles within sections, balances how often each letter is the key, and clones items from a template.
6. After the exam, it computes difficulty and discrimination for each item and tells you which keys to check and which distractors to replace.

You can also use one step at a time, for example "review this quiz before I print it" or "make three versions of this exam".

## Main rules

- Build the table of specifications first, and never write the items first and justify them later.
- Make every stem answerable with the options covered, and write it in positive form.
- Keep options similar in length and of the same kind, and remove absolute terms, grammatical cues and words repeated from the stem.
- Don't use "all of the above", and replace "none of the above" with the concrete action it stands for.
- Use three plausible options rather than four with a filler, and write each distractor from a real student error.
- Write apply and analyze items as scenarios with new data.
- Give every short answer question a verb, a scope and points per part, and grade it with an analytic rubric, blind to the student's name.
- Balance the key letter in each version, because test writers and test takers both favor the middle positions.

## Layout

```
SKILL.md                  the workflow the agent follows
references/
  table-of-specifications.md
  multiple-choice.md
  options-and-distractors.md
  cognitive-level.md
  constructed-response.md
  matching.md
  parallel-versions.md
  item-analysis.md
  checklist.md            25 yes/no checks before printing
  references.md           20 sources in IEEE format
```

## Sources

The rules come from 20 sources, including Haladyna, Downing and Rodriguez's review of item-writing guidelines, the NBME guide to writing test questions, Rodriguez's meta-analysis on the number of options, and studies on item flaws, item order, key position and grading bias. The full list is in [references/references.md](references/references.md). The same file also says which sources were read in full and which only from an abstract or a secondary summary, and the skill keeps those limits when it cites a rule.

## License

MIT. See [LICENSE](LICENSE).
