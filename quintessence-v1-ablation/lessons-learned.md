# Lessons learned

Quintessence failed to demonstrate sufficient incremental value. Condition A had the lowest human composite and four recorded intervention flags. Condition B became the production baseline. This decision simplifies the prompt on the evidence available; it does not establish that Quintessence is universally harmful.

Condition C showed that translating the same principles into plain English did not materially rescue them in this pilot. C did not demonstrate added value over B or D. Retaining a large layer simply by rewriting its language was not justified by these results. Semantic equivalence and population-level equivalence between conditions remain unproven.

Condition D scored strongly on conventional quality measures, leading both the human composite and descriptive panel consensus. It nevertheless showed undesirable behavioral tendencies, including unsupported interpretations of user motives and unnecessary intervention. Its three human flags mattered to the product decision, so D was not adopted wholesale. A high composite cannot substitute for an explicit decision about agency-related behavior.

Composite differences were concentrated in some cases. Q01 and Q06 drove much of A's deficit against B; Q09 and Q12 showed localized strengths for A. B-C and B-D mean orderings reverse under particular single-case omissions. Case-level reporting and sensitivity checks are necessary to keep a small pilot's headline average in proportion. These checks are not grounds to discard cases.

Intervention-gate interpretation became broader than the frozen definition. The reviewer included unsupported psychologizing and motive substitution, not only conventional unsupported-risk refusal or warning. The recorded flags remain useful diagnostic evidence, but that interpretive expansion must remain a methodology caveat. Future studies should freeze operational examples and separate distinct failure categories before scoring.

Human-primary scoring should be separated from later AI rationale assistance in future runs. Here, the human selected numerical ratings and AI helped with some rubric interpretation and rationale editing. A future record should distinguish locked human scores, contemporaneous reasoning, later edits and AI contributions. Do not describe this run as fully unaided human review or infer inter-rater reliability that was not measured.

Model-judge harness integration exposed provider-specific reasoning/token accounting, MAX_TOKENS behavior, HTTP 429 handling, request hangs, endpoint differences and the need for resumable model-local failure handling. Those are integration findings. Judge-interface failures are not proof of poor model quality. Excluded models and failed attempts should remain in the private audit trail without being converted into low quality scores.

The engineering requirements that emerged were:

- Hard wall-clock timeouts that bound actual requests, including hangs.
- Persistent evidence for attempts, outcomes, costs and uncertain billing.
- Per-model quarantine so one incompatible or failing model does not prevent unrelated work from progressing.
- Resumable model-local failure handling that preserves successful judgments and avoids replaying terminal attempts.
- Explicit budget reservations, including enlarged recovery attempts and unknown billing.
- Immutable review/reveal locks and integrity checks that prevent premature disclosure or evidence replacement.

These requirements describe lessons from operating the harness, not a claim that every earlier execution already implemented the final design. Seven terminal MAX_TOKENS failures remained missing in the completed panel: 569/576 valid judgments. The report preserves those absences instead of filling them in or calling the panel complete without qualification.

Future behavioral rules should be small, explicit and individually tested rather than added as large philosophical prompt layers. Start with a concrete failure, state the desired behavior, and test that rule across relevant cases and model choices. D6 provenance motivates checking portability as Bub adopts swappable models; this experiment does not establish that model-specific tuning explains the observed outcome.

The smallest proposed next step is an independent blind gate-only review of the 40 existing responses from Q01/Q02/Q04/Q09/Q11, with prior judgments hidden and the frozen gate enforced. Keep it separate from the original review. It can assess reproducibility of the disputed interpretation without new generations; broader generalization requires a separately designed study.
