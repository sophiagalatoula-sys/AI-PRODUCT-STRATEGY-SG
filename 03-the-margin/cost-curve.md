# Cost Curve & Pricing Strategy

## Packaging Decision — Leader, Filler, Killer

**Leader:** The blended credit-decisioning scorecard — bureau-sourced characteristics combined with Helios Pay's own digital-footprint and transactional signals into a single scoring engine. Every BNPL application runs through it; it's the core intelligence the entire product depends on.

**Filler:** The plain-language decision explanation generated from that same score, shown to the reviewing analyst and to the applicant. Cheap to produce on top of a score that already exists, and it applies to essentially every decision the system makes — it's what turns a number into something a person can actually act on or trust.

**Killer:** Underwriter review for the cases where a holistic-judgment model — reading the applicant's full record and both scorecards' own outputs — disagrees with the new model's own decision. This is the one step that consumes real, expensive human time rather than automated compute, and it's deliberately reserved for a minority of applications rather than run on every one.

**Percentage of users hitting the Killer:** Roughly 5% of applications (an illustrative estimate for how often the holistic-judgment model disagrees with the new scorecard's own decision — no pilot has run yet to confirm the real figure). Comfortably under the 70% threshold at which a feature should be folded into the standard flow rather than gated.

**Bundle-or-add-on decision:** Gate it. Scoring and explanation run on every application as the standard, bundled flow; underwriter review stays reserved for the disagreement-routed minority. Extending it to every application would recreate the underwriting-capacity bottleneck this design exists to solve in the first place.


## Cost Model

Basis: roughly 13,000 applications assessed per month, one scoring decision per application, a roughly 65% approval rate, and roughly 92% of approvals actually disbursed (around 7,800 funded loans per month, roughly 60% of applications) on an average ticket of roughly €250.

## Inputs
- Avg requests/user/month: 1
- Blended cost/request: $0.05
- Revenue/user/month: $8.4
- Non-AI COGS/user/month: $13.95

## Current Margin
- AI COGS/user: $0.05
- Total COGS/user: $14.00
- Gross margin: -66.7% ($-5.60/user)

## Stress Test
| Scenario | AI COGS | Margin |
|----------|---------|--------|
| 3x Cost  | $0.15 | -67.9% ($-5.70) |
| 2x Usage | $0.10 | -67.3% ($-5.65) |


## Cascading Strategy
<!-- Cheap model → frontier model routing logic -->
The credit-decisioning score itself has nothing to cascade — it's a scorecard calculation, not a generative model, and that's why it's already priced at effectively zero in the Cost Model above. The real tiering decision sits one layer up, with two distinct generative jobs running on top of the score: a small model that turns the score into a plain-language explanation, and a separate, frontier-tier holistic-judgment model that independently reads the full applicant record and decides whether it agrees with the new score's decision at all.

**Triage model:** A small, low-cost model generates the standard plain-language explanation from the score and its reason codes for every decision. This is the version a customer sees on request and the version that feeds business analysis of rejection drivers — a straightforward translation task that doesn't need frontier-level reasoning.

**Frontier model:** A frontier-tier holistic-judgment model that reads everything available for an applicant — raw profile, transaction history, digital-footprint signals, repayment history — together with the new scorecard's own score and decision, and forms an independent judgment on every application, not just a routed subset. When it agrees with the new model's decision (the large majority of cases), nothing further happens — the decision is applied automatically. When it disagrees, it additionally produces a justification for the underwriter: what it saw in the fuller record that the new scorecard's fixed weights didn't capture. This is a genuinely harder task than translating a score into words: it has to form its own independent view from the complete data picture, not simply describe one that already exists..

**Routing rule:** Every decision gets the small-tier explanation by default. Only the applications where the frontier model's own read disagrees with the new scorecard's decision get routed to underwriter review, together with that model's justification. The legacy bureau scorecard's verdict is shown to the underwriter as reference context on every routed case, but it does not itself determine whether a case is routed.

**Expected cascade ratio:** ~95% auto-decided / ~5% routed to underwriter, reflecting how often the frontier model disagrees with the new scorecard's own decision. The frontier model itself runs on every application regardless of this ratio, since it has to in order to know when to flag one — so a meaningful share of this layer's cost does not scale with the routed percentage; see the Cost Model above and the Stress Tests below.

A third AI feature sits outside this per-application cascade entirely: a monthly, portfolio-level scorecard-review model that combines two signals — how often underwriters confirm or overturn the frontier model's flags (a fast signal, available as soon as routed cases are reviewed) and actual repayment outcomes once loans mature (a slower signal, but the ground truth) — to flag candidates for the underwriting policy's next review: a characteristic worth adding, one worth dropping, or a weight worth reconsidering. It runs once a month across the whole portfolio rather than once per application, so its cost is negligible regardless of tier — the tier choice here is about task fit, not economics. It uses a frontier-tier model rather than the standard small tier: synthesizing a month of both signals into a specific, defensible recommendation that feeds Credit Risk's formal review process carries real weight and real room to be subtly wrong, unlike the routine per-decision explanation above. The model's output is a suggestion only — any adopted change still goes through Credit Risk's existing review process, and the live scorecard itself doesn't change in between.


## Pricing Model

**Current pricing:** A flat, risk-undifferentiated structure: roughly 4% merchant commission on the purchase amount plus a roughly €4 fixed fee per application, both identical regardless of which scoring model approved the application.

**Proposed AI pricing:** Unchanged. The AI-enhanced decisioning capability is not separately priced or charged to merchants or customers. Introducing a new fee here would work against the competitive reason this initiative exists in the first place — closing an approval-rate gap against rivals such as Klarna that already approve more of the same applicant pool. The value this capability creates is captured through volume and cost, not price: more approved-and-funded transactions at the existing commission and fee, and materially fewer defaults reducing the credit-losses line that already dominates this product's cost stack.

**Model:** seat-based / usage-based / outcome-based / hybrid
Outcome-based, without a price change. The entire case for this capability rests on two outcomes — a higher approval rate and a lower default rate in the higher-risk segment — but neither outcome is metered or billed per unit; both are monetized automatically through the existing flat commission and fee as approved volume grows and losses fall. This is a deliberate decision to hold price fixed and compete on decisioning quality instead of introducing a new charge.

## Alternatives Considered

**Commission renegotiation:** Considered and set aside for now. Merchants already compare Helios Pay's approval rate unfavorably against Klarna at similar commission levels — raising commission today would likely push more merchants toward Klarna rather than fund this initiative, not defend against it. This isn't a permanently closed door: it may become viable to revisit once the approval-rate gap has actually closed and merchants have evidence of the improvement, but it isn't available as a lever today.

**Attacking Non-AI COGS directly:** Reviewed across its components, not left unexamined. Funding cost was checked and no cheaper source of capital was found. Acquisition cost has already been reduced as far as identified — marketing spend was cut, with no further reduction found. Of the remaining Non-AI COGS components, credit losses is the one lever still open, and it's the one this bet directly targets: cutting the higher-risk segment's default rate from ~28% to ~19%. Within Non-AI COGS specifically, this initiative isn't one option among several untested ones — it's the remaining lever after the others were checked and ruled out.



## Board One-Pager
<!-- Before/After: Old SaaS revenue vs. AI usage revenue for your product -->

**Before (legacy scorecard, today):** On the full 13,000-application monthly book at a 65% approval rate (~7,800 funded loans), revenue runs ~€109,200/month against ~€182,000/month in total cost — a gross margin of ~-€72,800/month, ~-67%.

**After (AI-enhanced model):** The same 13,000 applications/month, now approved at 69% (~8,250 funded loans) instead of 65%, plus the cost of risk avoided by cutting the higher-risk segment's default rate from ~28% to ~19%. Revenue rises to ~€115,500/month (+~5.8%) on the extra funded volume. Total cost, despite that extra volume, actually falls slightly to ~€176,800/month, because the ~€16,250/month in avoided defaults outweighs the added cost of funding ~450 more loans. Gross margin improves to ~-€61,300/month, ~-53%.

**Net margin shift:** ~-67% to ~-53% — margin stays negative, but improves by roughly 14 percentage points, and the monthly loss narrows by ~€11,500 (~16%) in absolute terms while revenue simultaneously grows. This product doesn't reach profitability on decisioning quality alone — Non-AI COGS is still the dominant, unsolved problem — but the AI-enhanced model is unambiguously accretive: it grows the top line and shrinks the loss at the same time, which is the more complete version of the "margin percentage isn't the whole story" argument, since here both the percentage and the absolute euros move in the right direction together. 
What this doesn't capture: an underwriting layer precise enough to price by segment, ticket size, and repeat behavior is also the prerequisite for expanding into merchant categories and higher-ticket purchases the current scorecard's blanket conservatism keeps out of reach today, and for capturing repeat-purchase lift from customers the model now has real evidence to trust. None of that is quantified here — it depends on a validated model and live pilot results this initiative hasn't produced yet — but it's a reason this margin math likely understates the initiative's long-run value, not a claim this analysis is already pricing in.



