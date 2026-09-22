# My AI Product Strategy

> A living strategy built across 6 sessions. Each module adds one component. By Module 6, this repo IS your strategy — version-controlled, board-ready, portable.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [x] | [`01-the-bet/`](01-the-bet/) |
| **The Moat** | M2 | [x] | [`02-the-moat/`](02-the-moat/) |
| **The Margin** | M3 | [x] | [`03-the-margin/`](03-the-margin/) |
| **The Contract** | M4 | [x] | [`04-the-contract/`](04-the-contract/) |
| **The Guardrails** | M5 | [x] | [`05-the-guardrails/`](05-the-guardrails/) |
| **The Pitch** | M6 | [ ] | [`06-the-pitch/`](06-the-pitch/) |


---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** Helios Pay — a Greek digital lender that was the first BNPL (buy-now-pay-later) provider in the Greek market, now the second-largest after Klarna. This diagnostic covers an initiative to enhance the credit-risk decisioning model with AI/ML and Helios Pay's own data — adding characteristics Tiresias (Greece's credit bureau) doesn't have, and skipping the cost of a bureau call in specific cases where Helios Pay's own data is already sufficient, without dropping the underlying bureau relationship Credit Risk depends on for market-wide credit history — and addressing a higher-risk applicant segment (~10% of monthly originations) defaulting at a rate in the high-20s percent, an estimated €550,000–600,000 in preventable losses per year.
- - **AI Value Archetype:** Copilot
- **Vulnerability Scores:** Moat 2/5 · Data 2/5 · Platform 4/5
- **Top Risk:** Data Advantage (2/5) — the upstream cause behind the eroded Contextual Moat. Helios Pay's own years of BNPL loan-outcome data helped build the bureau's BNPL-specific scorecard, but that value compounds for the bureau, not for Helios Pay, which still can't see inside or correct it.
- **Confidence:** M
- **Prototype:** [Credit Decision Console](https://claude.ai/code/artifact/a63d5335-d609-4a88-b756-920464dc35d7)
- **Kill Criteria:** Before the 90-day live pilot, the model must clear a shadow-mode check against historical applications — at least a 20% projected reduction in the higher-risk segment's default rate — or the pilot doesn't start. Kill the live pilot itself if it doesn't cut the higher-risk segment's default rate by at least a third, if underwriters overturn more than half of routed decisions, or if overall approval rate drops more than a couple of points versus baseline.


→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:** 7/20
- **Weakest Loop:** Domain Context (1/5) — BNPL applications still run against a bureau template built for a different kind of lending, blind to purchase amount and category as real risk signals.
- **Competitive Position:** Trailing Klarna, Greece's BNPL leader, which already runs independent bureau-free underwriting live today. Also exposed to Revolut's platform-encroachment threat (global transactional data, Greek BNPL launch unconfirmed, ~30-40% of value at risk) and Hellas Direct's adjacent expansion (its own credit licence pending, ~12 months out, ~20-25% of value at risk).
- **Encroachment Defense:** Resolve the build-vs-buy decision toward Helios Pay building its own AI-enhancement layer on top of the bureau relationship — weighting Helios Pay's own transaction and repayment history above bureau-wide signal, and giving new or previously-declined customers a real path to prove themselves on a smaller first purchase.
- **Vendor Portability:** Partial


→ Details: [`02-the-moat/`](02-the-moat/)

---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):** -66.7% (-$5.60/user)
- **Gross Margin (AI-adjusted):** ~-53% (~-€61,300/month), up from ~-67% (~-€72,800/month) — margin stays negative but improves ~14 points as approval rate rises to 69% and the higher-risk segment's default rate falls from ~28% to ~19%
- **Pricing Model:** Outcome-based, without a price change — flat ~4% merchant commission plus ~€4 fixed fee, unchanged; value is captured through volume and reduced credit losses rather than a new AI fee
- **Cascading Strategy:** A small triage model generates every decision's plain-language explanation; a frontier-tier holistic-judgment model independently reviews every application and routes ~5% (where it disagrees with the scorecard) to underwriter review
- **Break-even at:** Not reachable through this initiative alone — even eliminating defaults entirely in the higher-risk segment caps avoided losses at ~€50,500/month, ~€10,800 short of closing the AI-enhanced scenario's ~-€61,300/month gap; a real breakeven target requires extending default-rate improvement well beyond the ~10% higher-risk segment (see `cost-curve.md`)


→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:** ≥97% accuracy (weekly) · <2% hallucination rate · <3s p95 latency · <1%/month drift velocity
- **Golden Dataset:** 10 rows, 3 adversarial (rows 7-9: a manufactured repayment pattern, a shared-device-fingerprint fraud signal, malformed input)
- **Confidence UX:** Tiered confidence surfaced in the underwriter review queue — auto-applied above 90%, both scorecards' verdicts shown side by side at 50-90%, no recommendation offered below 50%
- **HITL Architecture:** Triggered by holistic-judgment disagreement (~5% of applications) or a hard rule (shared-fingerprint match, data-validation failure); reviewed by a rotating on-call underwriter; every decision feeds back into the golden dataset via a weekly audit
- **Failure Mode Coverage:** 70% of the golden dataset's rows are edge cases, spanning thin-file applicants, a marginal near-cutoff score, synthetic/manufactured repayment history, shared-device fraud signals, malformed input, and reapplication-frequency bias


→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)

**What breaks when this scales — and what compounds.**

- **Compounding System:** 5 feedback loops identified — 1 active (fraud device/browser-fingerprint network intelligence), 3 broken by the same root cause (recursive learning, cross-domain signal transfer, and segment-calibration network intelligence all generate recommendations that Credit Risk isn't required to act on), 1 missing (merchant-risk network intelligence). Fix: every flagged candidate now gets a required adopt/defer/reject decision each monthly cycle, with a named accountable owner and an overdue-candidate count tracked in the existing audit cadence.
- **Governance Posture:** High-risk under the EU AI Act (Art. 6(2), Annex III(5)(b)). Fully or substantially met: risk management (Art. 9), record-keeping (Art. 12), accuracy/robustness (Art. 15), right to explanation (Art. 86), human oversight (Art. 14). Real gaps: data governance/bias review (Art. 10), transparency to deployers (Art. 13), and deployer obligations/applicant notice (Art. 26).
- **Shadow AI Status:** 6 tools found, 3 triaged as build candidates, 1 partner candidate, 2 flagged ignore + monitor
- **Agent Boundaries:** No agents shipped in this version — every AI component is a single-inference classifier or generator that returns one output and stops; none chains tool calls or picks its own actions.
- **Regulatory Exposure:** High-risk under the EU AI Act, plus GDPR Article 22 (no decision based solely on automated processing without recourse) and the EU Consumer Credit Directive's requirement to state a genuine decline reason.


→ Details: [`05-the-guardrails/`](05-the-guardrails/)

---

## The Pitch (M6)

**How you get this funded, shipped, and adopted.**

- **Horizon 1 (Now):** Close the immediate decision gaps — the Art. 10 bias-review call with Legal, the historical dataset for shadow-mode testing, and the scorecard characteristic-source map — all shippable with existing capabilities
- **Horizon 2 (Next):** Build and shadow-score the in-house model, pilot it live on a defined slice, grow the golden dataset past 10 rows, and instrument the defensibility KPI that proves (or disproves) the moat
- **Horizon 3 (Bet):** Assess dropping Tiresias for BNPL entirely, and build the missing merchant-risk network-intelligence loop
- **Board Narrative:** This is a share-defense play, not a new bet — Helios Pay already owns the data and the bureau relationship that could fix the approval-rate gap sending declined customers to Klarna, and every quarter without building on it is a quarter that gap compounds for free
- **Key Metric:** Higher-risk segment default rate — 28% baseline, ≥1/3 reduction required by the 90-day pilot's kill criteria


→ Details: [`06-the-pitch/`](06-the-pitch/)
