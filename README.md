# BUB × IFEval — public evaluation summary

Published September 30, 2026 as a public-safe evaluation artifact.

This is an aggregate evaluation of 540 valid responses from all 541 attempted IFEval prompts. It is not presented as a complete official 541-response IFEval score because one provider request ended in a preserved transport failure and was never retried.

## What was tested and why it matters

This evaluation tested BUB's instruction following on IFEval's 541 benchmark prompts, covering 834 instruction instances across 25 instruction types. Instructions include output format, word and sentence counts, required or forbidden words, capitalization, and response language. Following these constraints matters when people and downstream software rely on a response having a usable form.

The evaluated assistant used one frozen configuration. This result measures BUB with its underlying model; it does not isolate the "bare model" (the underlying model without BUB's private conditioning/workflow layer) or establish comparative superiority. BUB's private profile/conditioning text is withheld and is not part of the public export.

The provider was **DeepInfra**, using model **`zai-org/GLM-5.2`**, temperature **0.72**, `top_p` **0.92**, reasoning **none**, and a maximum output of **2048 tokens**. These are the public evaluation settings; other proprietary configuration content is withheld.

## Benchmark provenance

The reference implementation and dataset were pinned to Google Research commit `e6890f85757dd84e27ca6df2dd30651dafad28e0`. The local bundle label `ifeval-v1` is not an official upstream release number. See [the pinned upstream source](https://github.com/google-research/google-research/tree/e6890f85757dd84e27ca6df2dd30651dafad28e0/instruction_following_eval) and `provenance.json` for the dataset hash and citation to Zhou et al. (2023), *Instruction-Following Evaluation for Large Language Models*.

## Execution and measurement

All 541 prompts were attempted once across three preserved execution packages. There were no retries or replacement cases. Of these, 540 produced valid responses, covering 833 instruction instances. Response coverage was **99.8152%**; zero prompts remain unattempted.

The first pinned reference-scorer process remains primary:

| Measure | Passed / scored | Result |
|---|---:|---:|
| Strict prompt | 441 / 540 | 81.67% |
| Strict instruction | 722 / 833 | 86.67% |
| Loose prompt | 463 / 540 | 85.74% |
| Loose instruction | 750 / 833 | 90.04% |

A prompt passes only when all of its checked instructions pass. Instruction-level results count individual instructions. Strict scoring checks the saved response; loose scoring also considers the reference scorer's permitted response transformations. The original saved responses remain unchanged.

## What failed

The primary scorer recorded 99 strict prompt failures and 111 strict instruction failures, versus 77 loose prompt failures and 83 loose instruction failures. The largest strict instruction failure counts were forbidden words (13/49), sentence counts (12/52), letter frequency (10/33), and word counts (9/51). These counts have different denominators and are not a ranking of intrinsic task difficulty. All 25 instruction types are detailed in `instruction-failures.csv`.

Six responses ended normally at the output-token limit. Their exact returned text was scored as a model/configuration outcome, including any failures caused by truncation. They were not retried or excluded.

One separate operational failure, **ifeval-1251**, ended in an incomplete transport stream. Its partial evidence was preserved, it was never retried, and it was excluded from scoring. The underlying transport cause is not established by the retained evidence.

## Scorer variability

Five existing runs of the unchanged reference scorer checked the same saved responses. Strict prompt passes ranged from 439–441, strict instruction passes from 720–722, loose prompt passes from 463–464, and loose instruction passes from 750–751. Scorer variability means these repeated checks differed slightly because some reference checks use random behavior without a fixed starting seed. Observed changes affected letter-frequency and language-related checks. The first scorer execution is retained as primary without selecting a better repeat. These observations concern scorer variability, not model response variability. A loose failure count can exceed its strict counterpart for an individual instruction type under these checks.

## Interpretation and limitations

Most scored responses satisfied every checked instruction, while measurable weaknesses remained in precise lexical and length constraints. These results measure this frozen assistant configuration on this benchmark; they do not establish general reasoning ability, factual accuracy, safety, or performance on other workloads. Prompt-level scores use 540 valid/scorable responses; instruction-level scores use 833 scored instructions; coverage is 540 valid responses from 541 attempted benchmark prompts. Single attempts do not measure generation variability, and five scorer runs do not guarantee identical results. Withheld private conditioning and responses limit independent end-to-end reproduction from this public summary alone.

The evaluation process demonstrates explicit coverage accounting, separate treatment of operational failures and model outcomes, preservation of original evidence, and disclosure of scorer variability. Hash verification supports evidence consistency; it is not independent certification. No new generation or scoring was performed during finalization.

The public export contains only this summary, aggregate results, aggregate instruction failure counts, the public provenance and evaluation settings listed above, and checksums. No prompts, responses, private profile/conditioning text, other proprietary configuration content, runtime material, credentials, or proprietary source are included.
