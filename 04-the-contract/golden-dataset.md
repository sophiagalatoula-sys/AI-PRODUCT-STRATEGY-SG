# Golden Dataset & Reliability Contract

## Golden Dataset Spec

Ten labeled test cases for the credit-decisioning system: the primary scorecard, the plain-language explanation it generates, and the holistic-judgment model that independently checks every decision and flags the ~5% it disagrees with for underwriter review.

Test cases:
  1. Edge: N · Judge: rule, IN: Prime applicant: 6 years of on-time utility, telecom, and existing-loan payments; stable income; low existing debt; €200 purchase over 4 instalments.  → OUT: New scorecard: Approve, score ≥750. Explanation cites the repayment history and low debt ratio as the driving factors.
  2. Edge: N · Judge: rule, IN: Thin-file applicant, no bureau history, no Helios Pay history, income unverifiable from the application alone, no digital-footprint signals collected yet (first-ever session on the device).  → OUT: New scorecard: Decline. Explanation states the file is too thin to score confidently, not a specific negative factor.
  3. Edge: Y · Judge: LLM, IN: Near-prime applicant with a score of 649 — one point below the 650 approve/decline cutoff — otherwise unremarkable profile. → OUT: New scorecard: Decline, but the explanation names the score as marginal and close to the cutoff rather than implying the application was a poor risk.
  4. Edge: N · Judge: rule, IN: Higher-risk-segment applicant (bottom decile): legacy bureau scorecard declines (583/850) on a thin traditional file; new scorecard approves (671/850) on 24 months of on-time utility/telecom payments and stable transaction cadence; holistic-judgment model, reading the same full record, agrees with the new scorecard's approve.  → OUT: Application is auto-decided as Approve. The legacy scorecard's decline is shown to nobody as a review trigger — only as reference context if the case were ever escalated for an unrelated reason.
  5. Edge: Y · Judge: both, IN: Near-prime applicant: legacy scorecard approves (640/850), new scorecard approves (705/850, 81% confidence) on strong repayment history and low debt ratio — but the fuller record (available only to the holistic-judgment model) shows two new BNPL-style accounts opened at other providers in the prior three weeks and a debt-to-income ratio inconsistent with the stated income once those are counted.  → OUT: Holistic-judgment model disagrees with the new scorecard's approve and routes the application to underwriter review, with a justification naming the new external accounts and the revised debt-to-income figure. Both scorecards' verdicts are shown to the underwriter as context.
  6. Edge: Y · Judge: LLM, IN: Repeat applicant, proven on-time Helios Pay repayment history, application submitted within 60 days of a prior Tiresias bureau call already on file — bureau-call-skip path applies.  → OUT: Scorecard and explanation both correctly rely on Helios Pay's own repayment history and the existing bureau record rather than requesting or referencing a fresh bureau call; decision and explanation are unaffected by the skipped call.
  7. Edge: Y · Judge: both, IN: Adversarial — synthetic repayment pattern: an applicant with no prior history opens three small, unrelated purchase accounts and pays all three on time within the 30 days immediately before this application, producing an on-time-payment signal that looks identical to genuine long-term good behavior.  → OUT: New scorecard alone would likely approve on the payment signal; holistic-judgment model, reading the full timeline, flags the payment history as recently and artificially manufactured and routes to underwriter review rather than accepting the signal at face value.
  8. Edge: Y · Judge: rule, IN: Adversarial — shared-identity signal: the device and browser fingerprint on this application already appears on two other applications submitted under different applicant names within the past 48 hours. → OUT: Regardless of the scorecard's output on the stated profile, the application is routed to underwriter review with the shared-fingerprint pattern named explicitly in the justification — this signal overrides an otherwise-approvable score.
  9. Edge: Y · Judge: rule, IN: Adversarial — malformed input: application record has a null income field and a negative existing-debt value (a data-capture error, not a real applicant condition).  → OUT: System declines to auto-decide and routes to underwriter review rather than scoring on corrupted fields or silently defaulting to an approve; explanation states the specific fields that failed validation.
  10. Edge: Y · Judge: LLM, IN: Applicant applying for the fourth time in 90 days after three prior wrongful declines later confirmed as errors (the "reapplication after a wrongful decline" case the Portfolio review model already flags as a characteristic to reweight).  → OUT: New scorecard does not penalize the reapplication frequency itself as a negative factor; decision is based on the applicant's actual profile and history, and the explanation does not cite "multiple recent applications" as a reason for decline.

Dataset health
- Total: 10
- Edge cases: 7 (70.0%)
- Judge mix: 50% rule / 30% LLM / 20% both


## Confidence UX Design

**Approach:** show uncertainty / tiered confidence / human-in-loop trigger

**High confidence (>90%):**
**Medium confidence (70-90%):**
**Low confidence (<70%):**

**User control surface:**

## Reliability Contract

| Metric | Target | Measurement | Alert Threshold |
|--------|--------|-------------|-----------------|
| Accuracy | | | |
| Hallucination rate | | | |
| Latency (p95) | | | |
| Drift velocity | | | |

## HITL Architecture
<!-- When does a human step in? What's the escalation path? -->

## Red-Team Findings
*What failure mode did your partner find that you missed?*
