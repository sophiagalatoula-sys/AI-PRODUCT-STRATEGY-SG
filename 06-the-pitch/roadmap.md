# Three-Horizon Roadmap & Board Pitch

## Roadmap

### Horizon 1 — Now (0-3 months)
*Quick wins. Ship with existing capabilities.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Resolve the Art. 10 bias-review decision with Legal — whether age, gender, and marital status stay direct scoring inputs | Documented Credit Risk + Legal decision on record | H |
| Assemble the historical applications-and-outcomes dataset for the higher-risk segment, ready for shadow-mode scoring | Dataset covering ≥12 months of the segment's applications and outcomes | H |
| Document which live scorecard characteristics are bureau-sourced vs. Helios-Pay-collected and confirm re-weighting latitude | Characteristic-source map delivered to Credit Risk | H |


### Horizon 2 — Next (3-9 months)
*Bets. Requires new capabilities or integrations.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Build the in-house scoring model and shadow-score it against the historical dataset — no live applicants affected yet | ≥1/3 projected default-rate reduction on the higher-risk segment in shadow mode | M |
| Pilot the new scorecard live on a defined applicant slice via Provenir's existing routing rules | Higher-risk segment default rate cut ≥1/3 vs. baseline; underwriter overturn rate <50% of routed cases | M |
| Grow the golden dataset past its current 10 rows via the weekly gold-set audit and confirm accuracy in production | ≥97% accuracy sustained across 4 consecutive weekly runs | M |
| Define and instrument the defensibility KPI — lift on Helios Pay-owned repeat-purchase risk calibration vs. bureau baseline, stratified by cohort and purchase category/amount — then lock that lift into incremental repayment-performance labeling with cohort-specific priors | KPI tracked and reported monthly by cohort/category; positive lift sustained through the pilot | M |



### Horizon 3 — Bet (9-18 months)
*Moonshots. High uncertainty, high potential.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Assess dropping Tiresias for BNPL entirely (the Klarna model) vs. the narrower "call it less often" step | A modeled cost/risk recommendation delivered to Credit Risk and the business | L |
| Build the missing merchant-risk network-intelligence loop — aggregating fraud/dispute/early-default patterns across the merchant network | A working aggregation feeding real scorecard-candidate signals | L |


## Board Pitch

**Thesis (1 sentence):**
This is a share-defense play, not a new bet: we already own the data and the bureau relationship that could fix the approval-rate gap sending our declined customers straight to Klarna, and every quarter we don't build on it is a quarter that gap compounds against us for free.

**The case:**
1. Why now: We're not choosing to act — a deadline just got forced on us. Statistical Decisions Hellas, the one independent firm we used to sanity-check our own scorecard, became a Tiresias subsidiary this year, so the bureau now sits on both sides of every review we'd otherwise trust. Separately, the bureau finally built a BNPL-specific scorecard using market data collected since 2021 — proof this problem is solvable with data we've had access to the whole time, we just haven't built it ourselves. And the cost of waiting is quantified, not theoretical: ~€550–600K/year in preventable losses sitting in a segment that's 10% of originations.
2. What's defensible: Be direct — nothing yet. Data Flywheel scores 7/20, and the weakest loop is the one Klarna is already exploiting live, today, not on some future timeline. "Weight our own data more" is not, by itself, a moat — any bureau-integrated competitor with engineering time and similar internal data could copy it. What we're actually proposing is to go build the moat: instrument a specific KPI (lift on our own repeat-purchase risk calibration vs. the bureau baseline, by cohort and purchase category) and prove it holds over 90 days. If it doesn't hold, we don't have a moat — we have a temporary catch-up, and that changes the recommendation.
3. The economics: One number: this narrows our loss by ~€11,500/month (~16%), from -€72,800 to -€61,300. That's real. But even the best case for this specific segment — zero defaults in the higher-risk 10% — caps out ~€10,800/month short of breakeven. This is loss reduction and share defense, not a profitability plan. If the ask here is "does this make money," the honest answer is no, not on its own.

**The risks:**
1. Trust / failure modes: The front-page scenario is a wrongful decline tied to a protected characteristic, or an auto-decision nobody can explain. Two things catch it, and one thing doesn't yet: a golden test set with adversarial cases (manufactured repayment patterns, fraud signals) and a rubric-checked <2% hallucination rate on every explanation catch known failure modes; a human reviews every case the model disagrees with itself on, plus every hard fraud rule. What doesn't yet catch it: the Art. 10 bias review — whether age, gender, and marital status stay direct scoring inputs — is still an open decision with Legal, not resolved. That has to close before this goes live, not run in parallel with it.
2. Scale / governance: AI cost isn't the 10x risk — it's ~€0.05/application and stays trivial even under a 3x cost shock. The real 10x risk is underwriter capacity: our own stress test shows that if the highest-risk segment doubles, the disagreement-routed share roughly doubles too, straight onto a team that's a rotating on-call rotation, not a scaled function. Separately, 3 of our 5 compounding feedback loops generate recommendations nobody's required to act on — we've built a fix (a forced monthly decision), but it hasn't run yet, so "does this actually compound over time" is unproven, not confirmed.
3. Competitive: The kill scenario is already written down, in two stages. If shadow-mode testing doesn't show a 20% projected default-rate improvement by week 8, we stop before a single live applicant is touched. If it clears that and the defensibility KPI still shows no sustained lift over the bureau baseline by day 90, that's confirmation this was never a moat, and the recommendation flips to reconsider the build entirely rather than keep funding it.

**The ask:**
Not defined in what's in front of you today — that's a real gap, not an oversight I'm papering over. What this needs, minimum: a named owner inside Credit Risk, dedicated data science resourcing for one quarter, and a decision from Legal on Art. 10 before anything ships live. I don't have visibility into what else is competing for that same team's time, so I can't tell you what pauses to fund this — that's the one question I need this room to help answer, not one I'm bringing pre-solved.

## M1 Baseline vs. Now
*Your 3-sentence AI strategy from Module 1 vs. what you'd say now:*

**M1 baseline:**

**Now:**
