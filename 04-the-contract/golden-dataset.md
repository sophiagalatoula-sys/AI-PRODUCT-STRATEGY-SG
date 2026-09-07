# Golden Dataset & Reliability Contract

## Golden Dataset Spec

Ten labeled test cases for the credit-decisioning system: the primary scorecard, the plain-language explanation it generates, and the holistic-judgment model that independently checks every decision and flags the ~5% it disagrees with for underwriter review.

 | # | Input | Expected Output | Edge Case? | Judge Type |
|---|-------|----------------|-----------|-----------|
| 1 | Prime applicant: 6 years of on-time utility, telecom, and existing-loan payments; stable income; low existing debt; €200 purchase over 4 instalments. | New scorecard: Approve, score ≥750. Explanation cites the repayment history and low debt ratio as the driving factors. | N | Rule |
| 2 | Thin-file applicant, no bureau history, no Helios Pay history, income unverifiable from the application alone, no digital-footprint signals collected yet (first-ever session on the device). | New scorecard: Decline. Explanation states the file is too thin to score confidently, not a specific negative factor. | N | Rule |
| 3 | Near-prime applicant with a score of 649 — one point below the 650 approve/decline cutoff — otherwise unremarkable profile. | New scorecard: Decline, but the explanation names the score as marginal and close to the cutoff rather than implying the application was a poor risk. | Y | LLM |
| 4 | Higher-risk-segment applicant (bottom decile): legacy bureau scorecard declines (583/850) on a thin traditional file; new scorecard approves (671/850) on 24 months of on-time utility/telecom payments and stable transaction cadence; holistic-judgment model, reading the same full record, agrees with the new scorecard's approve. | Application is auto-decided as Approve. The legacy scorecard's decline is shown to nobody as a review trigger — only as reference context if the case were ever escalated for an unrelated reason. | N | Rule |
| 5 | Near-prime applicant: legacy scorecard approves (640/850), new scorecard approves (705/850, 81% confidence) on strong repayment history and low debt ratio — but the fuller record (available only to the holistic-judgment model) shows two new BNPL-style accounts opened at other providers in the prior three weeks and a debt-to-income ratio inconsistent with the stated income once those are counted. | Holistic-judgment model disagrees with the new scorecard's approve and routes the application to underwriter review, with a justification naming the new external accounts and the revised debt-to-income figure. Both scorecards' verdicts are shown to the underwriter as context. | Y | Both |
| 6 | Repeat applicant, proven on-time Helios Pay repayment history, application submitted within 60 days of a prior Tiresias bureau call already on file — bureau-call-skip path applies. | Scorecard and explanation both correctly rely on Helios Pay's own repayment history and the existing bureau record rather than requesting or referencing a fresh bureau call; decision and explanation are unaffected by the skipped call. | Y | LLM |
| 7 | Adversarial — synthetic repayment pattern: an applicant with no prior history opens three small, unrelated purchase accounts and pays all three on time within the 30 days immediately before this application, producing an on-time-payment signal that looks identical to genuine long-term good behavior. | New scorecard alone would likely approve on the payment signal; holistic-judgment model, reading the full timeline, flags the payment history as recently and artificially manufactured and routes to underwriter review rather than accepting the signal at face value. | Y | Both |
| 8 | Adversarial — shared-identity signal: the device and browser fingerprint on this application already appears on two other applications submitted under different applicant names within the past 48 hours. | Regardless of the scorecard's output on the stated profile, the application is routed to underwriter review with the shared-fingerprint pattern named explicitly in the justification — this signal overrides an otherwise-approvable score. | Y | Rule |
| 9 | Adversarial — malformed input: application record has a null income field and a negative existing-debt value (a data-capture error, not a real applicant condition). | System declines to auto-decide and routes to underwriter review rather than scoring on corrupted fields or silently defaulting to an approve; explanation states the specific fields that failed validation. | Y | Rule |
| 10 | Applicant applying for the fourth time in 90 days after three prior wrongful declines later confirmed as errors. | New scorecard does not penalize the reapplication frequency itself as a negative factor; decision is based on the applicant's actual profile and history, and the explanation does not cite "multiple recent applications" as a reason for decline. | Y | LLM |

Dataset health
- Total: 10
- Edge cases: 7 (70.0%)
- Judge mix: 50% rule / 30% LLM / 20% both

**Adversarial rows included:** 3 (rows 7, 8, 9) — a manufactured repayment pattern, a shared-device-fingerprint fraud signal, and malformed input.

## Confidence UX Design

The user here is the underwriter, not the applicant: applicants only ever see a decision and a plain-language reason, with no confidence indicator and no control surface, so the three tiers below describe what the underwriter's review queue shows for a case once it has already been routed to them.

**Approach:** show uncertainty / tiered confidence / human-in-loop trigger
Tiered confidence, surfaced inside the underwriter review queue, with a human-in-the-loop trigger built into which cases ever reach that queue at all.

**Confident (>90%):** The scorecard's decision is auto-applied and the case never enters the underwriter queue — there is nothing to review, so no confidence UI is shown to anyone at this tier.

**Uncertain (50-90%):** The case appears in the queue with both scorecards' verdicts and the holistic-judgment model's reasoning shown side by side. No recommendation is pre-filled; the case is framed as worth a look rather than a clear call, and the underwriter works from the full record.

**Not confident (<50%):** The case appears in the queue with no recommendation offered at all. This covers both genuinely low-confidence model output and cases routed by a hard rule (a fraud signal, a data-validation failure) that never had a confidence-scored recommendation to begin with. The screen is labeled as informational context only, and the underwriter reviews the case from scratch.


**User control surface:**
- Users adjust the confidence threshold: No — thresholds are set by the credit risk team as policy, not by individual underwriters.
- Users see AI reasoning / drivers: Yes — both scorecards' verdicts and the holistic-judgment model's justification are shown in full for every case that reaches the queue.
- Users correct & override outputs: Yes — every decision an underwriter makes on a routed case is itself the override; there is no separate override action because reviewing and deciding is the underwriter's whole job on these cases.
- Corrections feed back into the model / dataset: Yes — underwriter decisions are logged as labeled training data and feed the recurring scorecard and holistic-judgment model retraining directly.


## Reliability Contract

Before the new scorecard replaces the legacy one in production, this same golden-dataset accuracy run also serves as a one-time pre-launch validation gate: the pipeline has to clear the accuracy target on a dedicated validation pass — confirming it scores applications correctly against the agreed scorecard, not just against its own prior behavior — before go-live, separate from the weekly cadence it moves to afterward.

| Metric | Target | Measurement | Alert Threshold |
|--------|--------|-------------|-----------------|
| Accuracy | ≥97% | Weekly, full golden dataset, each row scored against its own Judge Type (Rule / LLM-as-Judge / Both) | <94% → pages the on-call underwriting lead; auto-decide is paused for new applications until root-caused |
| Hallucination rate | <2% | Same weekly run, applied only to the explanation and holistic-judgment justification text — a faithfulness rubric checks whether every cited factor is actually present in the applicant's record | >5% → rolls back the responsible component — the explanation model or the holistic-judgment model, whichever produced the flagged text — to its last known-good version |
| Latency (p95) | <3 seconds | Continuous production monitoring of the full pipeline: scorecard, explanation model, and holistic-judgment check | Sustained above 5 seconds for 5 minutes → pages on-call engineering; applications show a "decision pending" state rather than timing out silently |
| Drift velocity | <1%/month | The monthly Portfolio review model's comparison of decisioning outcomes against applicant characteristics | Decline exceeds 2% in a single review cycle → triggers an off-cycle golden-dataset audit and a scorecard reweighting review by Credit Risk |


## HITL Architecture
<!-- When does a human step in? What's the escalation path? -->

**Trigger:** The holistic-judgment model disagrees with the new scorecard's decision (roughly 5% of applications), or a hard rule fires regardless of the scorecard's own confidence — a shared-device-fingerprint match or a data-validation failure on a required field. Separately, an applicant can bring an already auto-decided case back into review after the fact by contacting customer support, which is how an applicant who wants an explanation or contests a decision reaches a human today.

**Reviewer:** A rotating on-call underwriter.

**Feedback loop:** Every underwriter decision and justification is logged as a labeled example. A weekly gold-set audit samples routed cases — confirmed decisions become new golden dataset rows, overturned ones flag a miss in the scorecard or the holistic-judgment model — and the results feed the monthly Portfolio review model's characteristic-reweighting recommendations.

