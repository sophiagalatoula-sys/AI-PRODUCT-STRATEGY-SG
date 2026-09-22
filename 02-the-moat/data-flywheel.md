# Data Flywheel Map

> Score each loop 1-5. Your weakest loop is where competitors attack first.
> The four loops below are the M2 starting point - adapt if your product has 2 or 6 loops instead of 4.

## Flywheel Loops

### Correction Loop - 2/5
**What you capture today:** Above a specific score band, applications already go to an underwriter for manual review and a decision, so some correction signal exists today — but it doesn't retrain anything automatically. An underwriter's call is relayed to Statistical Decisions Hellas — the independent analytics firm Helios Pay itself retains to review and adjust its own scorecard, the one actually driving Helios Pay's decisions today — which decides whether and how to adjust it; any resulting change is then deployed through the Provenir credit-decisioning engine. The underlying bureau credit score itself cannot be corrected this way at all — it's built from data pooled across every lending company in the market, not just Helios Pay, so Helios Pay has no real lever over it, and no visibility into how it's actually constructed in the first place. There's also no mechanism to catch the model's own mistakes at the individual level: the scorecard already counts an applicant's recent rejections and recent applications against them, so a customer who was wrongly declined and reasonably retries — believing the decision was wrong — is scored as if the retry itself were the risk, with nothing in the process able to recognize that the model, not the customer, was the problem. 

**How it compounds:** Slowly, manually, and only partially — and only for the one layer Helios Pay has any influence over. There's no automated retraining loop — every correction depends on an external company acting on relayed feedback on its own schedule, and even a successful correction only ever reaches the scorecard layer Helios Pay pays for, never the pooled, opaque bureau score a meaningful part of the overall assessment still rests on. Worse, nothing today distinguishes a false decline from genuine risk, so a bad decision doesn't just fail to get corrected — it actively compounds against the customer it was wrong about. The new model is designed to bring this in-house and make it direct: the same underwriter decisions that go to an external party today would instead retrain a model Helios Pay owns and understands outright, with no layer permanently placed off-limits or unexplainable, and with a real path to tell a wrongful decline apart from a genuine risk pattern. 

### Preference Loop - 2/5
**What you capture today:** Repayment history is already a factor — but it's weighted the wrong way. Because the assessment leans on the bureau's broader view of a customer's repayment behavior across other lenders, a customer with a strong, on-time repayment record specifically with Helios Pay can still be scored down for poor repayment behavior recorded elsewhere. Bureau-wide history currently outweighs Helios Pay's own more relevant, direct evidence, rather than the other way around.  

**How it compounds:** Currently, in the wrong direction: a good customer relationship with Helios Pay itself doesn't reliably protect an applicant from being penalized for behavior with other lenders, undercutting the exact repayment history that should matter most for a repeat-purchase decision. The new model is designed to reweight this properly — giving Helios Pay's own direct repayment evidence with a given customer the priority it deserves over less relevant bureau-wide signal, so a strong track record with Helios Pay actually improves that customer's odds next time instead of being outweighed by unrelated history. For customers with a strong enough track record, this is also where the cost savings shows up directly: Helios Pay's own evidence can be enough on its own, without triggering a new, billable Tiresias call for a repeat applicant whose behavior is already proven. 

### Domain Context Loop - 1/5
**What you capture today:** BNPL decisions still run on the bureau's original scorecard today — the one built for higher-value loans repaid over a longer period, not a purchase capped at €1,000 and repaid in at most four instalments of up to €250 each. The bureau has since built a dedicated BNPL scorecard, informed in part by data collected across the market rather than disproportionately Helios Pay's own, but Helios Pay hasn't adopted it: the live decision in front of Helios Pay is whether to pay the bureau for that BNPL-specific scorecard or have Helios Pay build its own AI-enhancement layer instead. A bigger, separate question sits above that one: whether Tiresias is needed for BNPL at all — Credit Risk currently favors keeping it, but the business sees Klarna's own bureau-free Greek BNPL operation as a real, unresolved case worth assessing, not a closed door. Until either question is resolved, every BNPL application is scored against a template built for a different kind of lending entirely. Even if the bureau's own BNPL-specific alternative were adopted, it would still be weighted above what Helios Pay itself knows about a given customer's behavior with Helios Pay directly, would give a new applicant with no Helios Pay history no path to prove different behavior on a small purchase, and would apply the same weighting regardless of whether the amount requested is under €100 or the full €1,000 maximum, with one narrower exception: Credit Risk already runs rules on merchant and product category, but only to flag or exclude merchants with evidence of fraud or a high rate of customer disputes, and only the mobile category specifically for that same fraud/dispute purpose — not as a genuine credit-risk signal that differentiates legitimate applicants by what or where they're buying. The scorecard also already counts how often an applicant has recently applied and been rejected — without the domain knowledge to interpret either correctly. Because applying for Helios Pay is a checkout button, not a deliberate loan application, a customer who selects it by mistake or just to compare options at checkout generates the same recorded "application" as someone genuinely seeking credit, inflating how often they appear to be applying for reasons that have nothing to do with risk. 

**How it compounds:** Not yet, and the live choice in front of Helios Pay decides whether it ever will. Paying the bureau for its new BNPL-specific scorecard would fix the loan-type mismatch but leave every other domain gap in place — it would still outweigh Helios Pay's own transaction history, still give new customers no path to prove themselves, still leave purchase amount and category as fraud-exclusion rules rather than a genuine credit-risk signal, and still treat a checkout misclick or a good-faith retry after a wrongful decline the same as genuine repeat risk-seeking. Building Helios Pay's own AI-enhancement layer on top of the bureau relationship instead is what actually lets Helios Pay weight its own history properly, extend credit to new customers starting with a smaller first purchase, broaden the existing merchant- and mobile-category-only fraud rules into real credit-risk inputs across every merchant and category, add purchase amount as a scoring input in its own right, and tell a real credit request apart from checkout noise — domain knowledge only Helios Pay is positioned to have, and that no scorecard it merely pays for, bureau or otherwise, would fully use. 

### Network Loop - 2/5
**What you capture today:** Helios Pay's own applicant and outcome data does feed back into the model — but only once a year. Credit Risk shares customer data with Statistical Decisions Hellas annually so the scorecard can be reviewed and adjusted, and getting anything actually changed depends on Credit Risk actively challenging Statistical Decisions Hellas's own view of the model and making the case for what's wrong with it — the data doesn't speak for itself. And the evidence available for that case has a structural hole: an applicant who's rejected never gets the chance to repay, so there's no real outcome data to prove a declined applicant would have been a good customer. That gap falls hardest on applicants new to Helios Pay, who have the least other evidence in their favor — precisely the group the annual review is least able to build a case for. 

**How it compounds:** Once a year, and only for the applicants Helios Pay actually approved. Every rejection is a data point Helios Pay can never use to argue the model was wrong, so the population most likely to reveal a miscalibrated score — declined applicants who would have paid — never accumulates into evidence at all. An in-house AI model that retrains continuously, instead of waiting for an annual, negotiated review, is what shortens this cycle; deliberately extending credit to some new or marginal applicants on smaller amounts first — the same fix Domain Context points to — is what actually starts generating the outcome data this process structurally can't produce today.

**Total Flywheel Score: 7/20**

**Weakest Loop:** Domain Context

At 1/5, this is the clear low point, and the gap is more literal than it might sound: Helios Pay isn't just under-using BNPL-specific insight, it's still scoring every BNPL application today against a bureau template built for an entirely different kind of lending — one that also can't tell a genuine credit request apart from a checkout misclick, or a good-faith retry after a wrongful decline apart from real repeat risk. The bureau's own BNPL-specific fix already exists, but adopting it means paying for a scorecard that would still outweigh what Helios Pay itself knows about a given customer's behavior with Helios Pay directly, still give new customers no path to prove themselves, and still ignore the specific purchase's amount and category. That's exactly the domain knowledge Helios Pay is uniquely positioned to have and a purchased scorecard structurally can't hold — and it's a real part of why a segment defaulting at a materially higher rate went unaddressed for as long as it did.

**Fix for weakest loop:** This is the build-vs-buy decision this loop actually turns on — which party builds the layer that adds Helios Pay's own data on top of Tiresias, and, on a bigger and separately unresolved question, whether Tiresias is needed for BNPL at all (Credit Risk currently favors keeping it; the business sees Klarna's own bureau-free BNPL operation as a real case worth assessing, not settled either way). Paying the bureau for its BNPL-specific scorecard fixes the loan-type mismatch but not the domain gap underneath it. Helios Pay building its own AI-enhancement layer instead is what lets Helios Pay weight its own transaction and repayment history as the primary signal, give new customers a real path to build history starting with a smaller first purchase, broaden the merchant- and mobile-category-only fraud rules that already exist into real credit-risk inputs across every merchant and category and add purchase amount as a scoring input in its own right, distinguish a real application from checkout noise or a wrongful-decline retry, and — for customers whose behavior is already proven, or whose bureau data was pulled recently enough to still be current — skip a new, billable Tiresias call altogether. That's the clearest source of edge available, and one no bought scorecard delivers. This decision has sat unresourced while Klarna's own bureau-free underwriting keeps operating live in the market — the build itself needs a named owner, dedicated data science resourcing, and a committed timeline (model built and shadow-scored within the quarter, gated at week 8), not just a stated preference for build over buy. But weighting Helios Pay's own data more heavily is not, on its own, a durable moat — any bureau-integrated competitor with enough engineering effort and access to similar internal outcome data could replicate the same reweighting. Klarna's live, bureau-free underwriting is already proof the real competitive bar here is underwriting autonomy, not a more explainable scorecard. What would make this durable is a defensibility KPI the initiative is held to, not just shipped and left: lift on Helios Pay-owned repeat-purchase risk calibration versus the bureau baseline, stratified by cohort and by purchase category/amount. The next 90 days should go toward locking that lift into a genuinely hard-to-replicate mechanism — incremental repayment-performance labeling with cohort-specific priors — not just improving the current console.

---

## Encroachment Threat Assessment

### 1. Platform Encroachment

**Attacker:** Revolut 

**Vector:** Platform Encroachment 

**Time-to-threat:** Uncertain, but not distant. Revolut already has full Greek market access and a working BNPL product elsewhere in Europe — bringing it to Greece is an expansion decision, not a new-product build. No Greek launch has been confirmed. 

**% of value at risk:** ~30-40% (estimate)


### 2. Vertical Competitor

**Attacker:** Klarna 

**Vector:** Vertical Competitor 

**Time-to-threat:** Already live. This is a present threat, not a future one: Klarna is Greece's BNPL market leader today, specifically because it already solved the underwriting-dependency problem this initiative is trying to solve. 

**% of value at risk:** ~50% (estimate). Klarna already holds the default choice of both the customers Helios Pay's own underwriting rejected and the merchants who prefer the higher-approval option. Closing the gap this initiative targets defends against further share loss more than it recovers ground Klarna already holds.


### 3. Adjacent Expansion

**Attacker:** Hellas Direct 

**Vector:** Adjacent Expansion 

**Time-to-threat:** ~12 months (estimate). Its Bank of Greece credit licence application is filed and expected to be granted within the year it was filed; product expansion would likely follow licensing, not precede it. 

**% of value at risk:** ~20-25% (estimate). Limited today to the BNPL volume Hellas Direct currently routes through bank partners, Helios Pay included. The real exposure is losing that volume once Hellas Direct can originate credit itself instead of needing a bank partner for it. 

These three don't stack cleanly into one number, but together they cover every route into this market: a platform with better data than Helios Pay will ever have on its own, a specialist that already solved the exact problem this initiative is trying to solve, and a partner-turned-competitor with a licence already in motion. None of the three depends on the others — Revolut's Greek BNPL plans are unconfirmed, Klarna doesn't need Hellas Direct's licence to keep winning, and Hellas Direct doesn't need Revolut's data to disintermediate a bank partner. The one place all three converge is the higher-risk segment this initiative is built around: it's the segment most exposed to a data-richer outsider, most already lost to a competitor with independent underwriting, and most likely to move if a trusted adjacent brand offers an easier yes.

---

## 90-Day Encroachment Plan

*Your partner played the Big Tech attacker. What was their plan to kill you?*

**Attacker:** Klarna — the vertical competitor, and the only one of the three named above that's already live rather than pending.

**Attack vector (target the weakest loop):** Domain Context, scoring 1/5. BNPL applications still run against a bureau template built for higher-value, longer-tenor loans — blind to purchase amount and category as a genuine risk signal, beyond the narrow merchant/mobile-category fraud rules that already exist, unable to weight a customer's own Helios Pay history over less relevant bureau-wide signal, and unable to give a new applicant a path to prove themselves on a small first purchase. Klarna already runs its own independent, BNPL-native credit assessment, so this is the one loop it doesn't need to build — only to keep exploiting.

**Weeks 1-4 - what they ship:** Nothing new needs building — Klarna's independent, Tiresias-free BNPL underwriting is already live. What ships is sharper targeting: instant-approval marketing aimed specifically at merchants who've raised the decline rate as a problem, and at applicants Helios Pay's scorecard rejects for reasons that have nothing to do with real BNPL risk — thin file, no prior Helios Pay history, or a purchase amount and category the scorecard still can't weigh as a risk signal beyond its narrow fraud rules.

**Weeks 5-8 - how they poach users:** Merchants integrated with both providers route more checkout volume to Klarna by default, reinforcing the higher-approval reputation this initiative's own diagnostic already documents. Customers Helios Pay declines — including ones a domain-aware model would have approved — get approved by Klarna instead, and start building their repayment history there rather than with Helios Pay.

**Weeks 9-12 - why users don't come back:** Once a customer has a working repayment history and an approved limit with Klarna, there's little reason to retry Helios Pay — Helios Pay's scorecard still can't offer a differentiated first-purchase path for a new or previously-declined customer, still can't weigh their own purchase behavior over bureau-wide history, and still has no domain-specific reason to say yes where it said no before. The switch becomes permanent by default, not by any deliberate choice the customer makes.

**Your defense:** Ship the fix this loop is already pointed at — resolve the build-vs-buy decision toward Helios Pay building its own AI-enhancement layer on top of the bureau relationship, so Helios Pay can weight its own transaction and repayment history above bureau-wide signal, extend new and previously-declined customers a real path to prove themselves on a smaller first purchase, and broaden its narrow merchant/mobile-category fraud rules into real credit-risk inputs while adding purchase amount as a scoring input in its own right. Every week that decision stays unresolved is a week Klarna's advantage on exactly this segment compounds for free.


