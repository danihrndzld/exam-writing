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
- Writes multiple choice, short answer and matching items that follow 31 published item-writing guidelines [1] and the NBME item-writing guide [2].
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

- Build the table of specifications first, and never write the items first and justify them later [1], [18].
- Make every stem answerable with the options covered, and write it in positive form [1], [2].
- Keep options similar in length and of the same kind, and remove absolute terms, grammatical cues and words repeated from the stem [1], [2].
- Don't use "all of the above", and replace "none of the above" with the concrete action it stands for [1], [2].
- Use three plausible options rather than four with a filler, and write each distractor from a real student error [1], [3], [4].
- Write apply and analyze items as scenarios with new data [2], [10].
- Give every short answer question a verb, a scope and points per part, and grade it with an analytic rubric [11], blind to the student's name [12].
- Balance the key letter in each version, because test writers and test takers both favor the middle positions [15].

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

## References

The rules come from these 20 sources, in IEEE format. [references/references.md](references/references.md) also says which sources were read in full and which only from an abstract or a secondary summary, and the skill keeps those limits when it cites a rule.

[1] T. M. Haladyna, S. M. Downing, and M. C. Rodriguez, "A review of multiple-choice item-writing guidelines for classroom assessment," *Applied Measurement in Education*, vol. 15, no. 3, pp. 309-333, 2002, doi: 10.1207/s15324818ame1503_5.

[2] M. A. Paniagua and K. A. Swygert, Eds., *Constructing Written Test Questions for the Basic and Clinical Sciences*, 4th ed. Philadelphia, PA, USA: National Board of Medical Examiners, 2016.

[3] M. C. Rodriguez, "Three options are optimal for multiple-choice items: A meta-analysis of 80 years of research," *Educational Measurement: Issues and Practice*, vol. 24, no. 2, pp. 3-13, 2005, doi: 10.1111/j.1745-3992.2005.00006.x.

[4] M. Tarrant, J. Ware, and A. M. Mohammed, "An assessment of functioning and non-functioning distractors in multiple-choice questions: A descriptive analysis," *BMC Medical Education*, vol. 9, Art. no. 40, 2009, doi: 10.1186/1472-6920-9-40.

[5] M. J. Gierl, O. Bulut, Q. Guo, and X. Zhang, "Developing, analyzing, and using distractors for multiple-choice tests in education: A comprehensive review," *Review of Educational Research*, vol. 87, no. 6, pp. 1082-1116, 2017, doi: 10.3102/0034654317726529.

[6] S. M. Downing, "The effects of violating standard item writing principles on tests and students: The consequences of using flawed test items on achievement examinations in medical education," *Advances in Health Sciences Education*, vol. 10, no. 2, pp. 133-143, 2005, doi: 10.1007/s10459-004-4019-5.

[7] M. Tarrant and J. Ware, "Impact of item-writing flaws in multiple-choice questions on student achievement in high-stakes nursing assessments," *Medical Education*, vol. 42, no. 2, pp. 198-206, 2008, doi: 10.1111/j.1365-2923.2007.02957.x.

[8] L. W. Anderson and D. R. Krathwohl, Eds., *A Taxonomy for Learning, Teaching, and Assessing: A Revision of Bloom's Taxonomy of Educational Objectives*. New York, NY, USA: Longman, 2001.

[9] D. R. Krathwohl, "A revision of Bloom's taxonomy: An overview," *Theory Into Practice*, vol. 41, no. 4, pp. 212-218, 2002, doi: 10.1207/s15430421tip4104_2.

[10] D. Scully, "Constructing multiple-choice items to measure higher-order thinking," *Practical Assessment, Research, and Evaluation*, vol. 22, Art. no. 4, 2017, doi: 10.7275/swgt-rj52.

[11] A. Jonsson and G. Svingby, "The use of scoring rubrics: Reliability, validity and educational consequences," *Educational Research Review*, vol. 2, no. 2, pp. 130-144, 2007, doi: 10.1016/j.edurev.2007.05.002.

[12] J. M. Malouff and E. B. Thorsteinsson, "Bias in grading: A meta-analysis of experimental research findings," *Australian Journal of Education*, vol. 60, no. 3, pp. 245-256, 2016, doi: 10.1177/0004944116664618.

[13] P. Yeates, M. Moreau, and K. Eva, "Are examiners' judgments in OSCE-style assessments influenced by contrast effects?," *Academic Medicine*, vol. 90, no. 7, pp. 975-980, 2015, doi: 10.1097/ACM.0000000000000650.

[14] S. N. Şad, "Does difficulty-based item order matter in multiple-choice exams? (Empirical evidence from university students)," *Studies in Educational Evaluation*, vol. 64, Art. no. 100812, 2020, doi: 10.1016/j.stueduc.2019.100812.

[15] Y. Attali and M. Bar-Hillel, "Guess where: The position of correct answers in multiple-choice test items as a psychometric variable," *Journal of Educational Measurement*, vol. 40, no. 2, pp. 109-128, 2003, doi: 10.1111/j.1745-3984.2003.tb01099.x.

[16] M. J. Gierl, H. Lai, and S. R. Turner, "Using automatic item generation to create multiple-choice test items," *Medical Education*, vol. 46, no. 8, pp. 757-765, 2012, doi: 10.1111/j.1365-2923.2012.04289.x.

[17] M. J. Kolen and R. L. Brennan, *Test Equating, Scaling, and Linking: Methods and Practices*, 3rd ed. New York, NY, USA: Springer, 2014.

[18] H. Fives and N. DiDonato-Barnes, "Classroom test construction: The power of a table of specifications," *Practical Assessment, Research, and Evaluation*, vol. 18, Art. no. 3, 2013, doi: 10.7275/cztt-7109.

[19] T. M. Haladyna and M. C. Rodriguez, *Developing and Validating Test Items*. New York, NY, USA: Routledge, 2013.

[20] T. L. Kelley, "The selection of upper and lower groups for the validation of test items," *Journal of Educational Psychology*, vol. 30, no. 1, pp. 17-24, 1939.

## License

MIT. See [LICENSE](LICENSE).
