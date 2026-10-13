# Quintessence V1 ablation: public experiment report

Quintessence failed to demonstrate sufficient incremental value in this 12-case pilot. Bub adopted condition B, the baseline with Quintessence removed. This was a reversible product decision informed by observed behavior, not proof that removal is universally superior.

The hypothesis under test was that adding Quintessence would improve Bub's responses enough to justify retaining it alongside the existing baseline. The ablation asked whether any benefit came from the original formulation, from the same principles expressed plainly, or from generic assistant guidance. It also tested whether a simpler baseline already provided the desired behavior.

Quintessence was originally developed for the D6 model. It was later evaluated as Bub moved toward a swappable-model architecture. That history is provenance: this experiment did not test whether model-specific tuning caused the result, and it did not compare generation models.

The design was **12 cases x 4 conditions x 2 samples = 96 generated responses**. All conditions used the same generator, GLM-5.2, and generation settings: temperature 0.72, top_p 0.92 and a 2,048-token output cap. The experiment evaluated a frozen static prompt without dynamic context. Other baseline components remained fixed.

| Condition | Public description |
| --- | --- |
| A | Bub baseline with full Quintessence |
| B | Same baseline with Quintessence removed |
| C | Same baseline with a plain-English semantic equivalent |
| D | Same baseline with generic high-quality assistant guidance |

The primary method was **human-primary blind review with AI-assisted rubric interpretation and rationale editing**. The human reviewer selected numerical ratings; AI helped with some rubric interpretation and rationale editing. Model identities and the A/B/C/D mapping were hidden during human scoring. The locked record contains one rating set for each response and no pairwise preference votes. Human ratings and model-panel judgments were analyzed separately.

The secondary panel comprised GPT-6.1 Sol, Claude Opus 5.5, Gemini 3.8 Flash, Kimi K3, DeepSeek V4 Pro and GLM-5.2. It completed **569/576 judgments**. Seven judgments remained missing after terminal MAX_TOKENS failures. Missing scores were not imputed. GLM-5.2 shares the generator family and serves as a diagnostic, not independent cross-family corroboration. The six judges assessed the same outputs; their judgments are correlated.

The frozen composite converts seven 1-5 rubric dimensions to 0-100 rubric points. Samples are averaged within each case/condition, then the 12 cases receive equal weight. The binary intervention gate is reported separately. Details and denominators appear in [methodology.md](methodology.md) and [results-public.json](results-public.json).

| Condition | Human composite /100 | Recorded human intervention flags | Descriptive panel composite /100 | Valid panel judgments |
| --- | ---: | ---: | ---: | ---: |
| A | 67.24 | 4/24 | 80.26 | 142/144 |
| B | 71.15 | 0/24 | 82.70 | 143/144 |
| C | 70.21 | 0/24 | 81.14 | 142/144 |
| D | 72.76 | 3/24 | 84.45 | 142/144 |

These human and panel columns are separate summaries, never a pooled score. The panel consensus is a post-reveal descriptive calculation that first averages available judges per response. Human intervention flags include a broader interpretation than the frozen gate, discussed below.

Human A minus B was -3.91 points, with an exploratory 95% whole-case bootstrap interval of [-11.09, 3.23]. A minus C was -2.97 [-10.16, 4.17]; C minus D was -2.55 [-11.61, 6.20]. **All six human composite contrast intervals include zero.** D > B > C > A is an observed ordering, not an established population ranking. All five cross-family judges put B above A; GLM-5.2 alone put A slightly above B. All six judges put D above C.

A was lower than B on six of seven human rubric dimensions. The largest differences were judgment/tradeoffs, evidence discipline and agency preservation. Approximately 95% of the A-B composite deficit came from non-style dimensions; this decomposes the existing composite rather than inventing a new endpoint. C did not demonstrate added value over B or D: translating the principles into plain English did not materially rescue them in this pilot. This does not establish equivalence between formulations.

Effects were concentrated in some cases. Q01 and Q06 contributed most to A's deficit against B; Q09 and Q12 favored A. Omitting both Q01 and Q06 changes A-B from -3.91 to +0.25 across ten cases. Omitting Q01 reverses the B-C mean ordering; omitting Q03 reverses B-D. These are sensitivity checks, not reasons to remove inconvenient cases. Public case results use opaque IDs and numeric scores only.

The frozen intervention gate concerned unsupported-risk refusal, sanitization, redirection or strong warning. Human interpretation extended to unsupported psychologizing that redirected the task or recast user motives. The recorded 4/0/0/3 counts preserve that interpretation; they are not a clean estimate of conventional safety-refusal false positives. A's four flags occurred in three cases and D's three in three cases. B and C's zero observations do not establish zero risk. Across 569 model judgments there were nine fail votes; only one of the seven human-flagged responses received any model fail vote. This disagreement remains visible rather than being reconciled into a common measure.

Twelve selected cases are the meaningful experimental units. Two samples capture limited within-case variation; 96 responses and 569 judgments do not create that many independent experiments. No materiality threshold or equivalence margin was frozen. Intervals are exploratory, not multiplicity-adjusted, and conditional on this case set and ratings. Missing judgments may be nonrandom. Anonymous wording could still reveal stylistic clues. Inter-rater reliability was not documented, and AI assistance limits claims of fully unaided human review. The static-prompt results do not establish behavior across models or full production conversations.

The production decision prioritized demonstrated incremental value and agency-related behavior. B became Bub Baseline V1. D scored strongly on conventional quality but had undesirable behavioral tendencies and was not adopted wholesale. Quintessence was removed from production prompt assembly in PR #78, merge commit `2a76d43f6c45c2b49ccef07ebb4165f682cfe3c9`. The remaining assembly order is **COSMOLOGY -> SOUL -> Anti-Slop -> Theater Mode -> Media Instructions**. See [production-change.md](production-change.md); protected component contents are withheld.

The practical lesson is to test small, explicit behavioral rules individually instead of adding large philosophical prompt layers. The judge harness also required stronger failure isolation, persistent evidence, budget reservations and reveal locks. [lessons-learned.md](lessons-learned.md) records those operational lessons without treating interface failures as model-quality findings.

The sealed analysis recommends a small follow-up: an additional independent human gate-only blind review of the 40 existing responses in Q01/Q02/Q04/Q09/Q11, using the frozen definition and hiding prior scores and model results. Retain that review separately. It would test reproducibility of the disputed gate interpretation without new generations; it would not establish population superiority or B/C equivalence. Broader testing across tasks and swappable models remains a separate question.

This release derives numerical findings from the sealed post-reveal report and results. D6 provenance, the clarification of human/AI roles and production implementation details were supplied by the experiment owner. Opaque SHA-256 anchors identify the protected source artifacts in the JSON. Proprietary prompts, condition contents beyond the descriptions above, task text, generated responses, rationale quotations, private source files, account details and private conversations are intentionally omitted. Consequently, this is a public results package, not a complete reproduction bundle.
