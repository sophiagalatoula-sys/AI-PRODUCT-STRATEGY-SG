# Data Flywheel Map

> Score each loop 1-5. Your weakest loop is where competitors attack first.
> The four loops below are the M2 starting point - adapt if your product has 2 or 6 loops instead of 4.

## Flywheel Loops

| Loop | What It Measures | Score 1 | Score 5 | Score |
|------|------------------|---------|---------|-------|
| **Correction** | Do users fix AI outputs? Is that signal captured and reused? | No capture | Automated retraining | 2/5 |
| **Preference** | Does the product learn individual / team preferences over time? | Stateless | Deep personalization | 2/5 |
| **Domain Context** | Does usage in one area improve quality in adjacent areas? | Siloed | Cross-domain transfer | 1/5 |
| **Network** | Does each new user / team make the product better for everyone? | Isolated | Strong network effects | 2/5 |

### Correction Loop - 2/5
**What you capture today:** Above a specific score band, applications already go to an underwriter for manual review and a decision, so some correction signal exists today — but it doesn't retrain anything automatically. An underwriter's call is relayed to Statistical Decisions Hellas, the external firm behind Tiresias's scorecards, which decides whether and how to adjust the one actually driving Helios Pay's decisions today; any resulting change is then deployed through the Provenir credit-decisioning engine. The underlying bureau credit score itself cannot be corrected this way at all — it's built from data pooled across every lending company in the market, not just Helios Pay, so Helios Pay has no real lever over it, and no visibility into how it's actually constructed in the first place. There's also no mechanism to catch the model's own mistakes at the individual level: the scorecard already counts an applicant's recent rejections and recent applications against them, so a customer who was wrongly declined and reasonably retries — believing the decision was wrong — is scored as if the retry itself were the risk, with nothing in the process able to recognize that the model, not the customer, was the problem. 

**How it compounds:** Slowly, manually, and only partially — and only for the one layer Helios Pay has any influence over. There's no automated retraining loop — every correction depends on an external company acting on relayed feedback on its own schedule, and even a successful correction only ever reaches the scorecard layer Helios Pay pays for, never the pooled, opaque bureau score a meaningful part of the overall assessment still rests on. Worse, nothing today distinguishes a false decline from genuine risk, so a bad decision doesn't just fail to get corrected — it actively compounds against the customer it was wrong about. The new model is designed to bring this in-house and make it direct: the same underwriter decisions that go to an external party today would instead retrain a model Helios Pay owns and understands outright, with no layer permanently placed off-limits or unexplainable, and with a real path to tell a wrongful decline apart from a genuine risk pattern. 

### Preference Loop - 2/5
**What you capture today:** Repayment history is already a factor — but it's weighted the wrong way. Because the assessment leans on the bureau's broader view of a customer's repayment behavior across other lenders, a customer with a strong, on-time repayment record specifically with Helios Pay can still be scored down for poor repayment behavior recorded elsewhere. Bureau-wide history currently outweighs Helios Pay's own more relevant, direct evidence, rather than the other way around. 

**How it compounds:** Currently, in the wrong direction: a good customer relationship with Helios Pay itself doesn't reliably protect an applicant from being penalized for behavior with other lenders, undercutting the exact repayment history that should matter most for a repeat-purchase decision. The new model is designed to reweight this properly — giving Helios Pay's own direct repayment evidence with a given customer the priority it deserves over less relevant bureau-wide signal, so a strong track record with Helios Pay actually improves that customer's odds next time instead of being outweighed by unrelated history. 

### Domain Context Loop - 1/5
**What you capture today:** BNPL decisions still run on the bureau's original scorecard today — the one built for higher-value loans repaid over a longer period, not a purchase capped at €1,000 and repaid in at most four instalments of up to €250 each. The bureau has since built a dedicated BNPL scorecard, based mainly on Helios Pay's own BNPL data, but Helios Pay hasn't adopted it: the live decision in front of Helios Pay is whether to pay the bureau for that BNPL-specific scorecard or build an in-house AI-generated scorecard instead — and until that decision is made, every BNPL application is scored against a template built for a different kind of lending entirely. Even if the bureau's own BNPL-specific alternative were adopted, it would still be weighted above what Helios Pay itself knows about a given customer's behavior with Helios Pay directly, would give a new applicant with no Helios Pay history no path to prove different behavior on a small purchase, and would apply the same weighting regardless of whether the amount requested is under €100 or the full €1,000 maximum, or whether the purchase is a mobile phone or furniture. The scorecard also already counts how often an applicant has recently applied and been rejected — without the domain knowledge to interpret either correctly. Because applying for Helios Pay is a checkout button, not a deliberate loan application, a customer who selects it by mistake or just to compare options at checkout generates the same recorded "application" as someone genuinely seeking credit, inflating how often they appear to be applying for reasons that have nothing to do with risk.

**How it compounds:** Not yet, and the live choice in front of Helios Pay decides whether it ever will. Paying the bureau for its new BNPL-specific scorecard would fix the loan-type mismatch but leave every other domain gap in place — it would still outweigh Helios Pay's own transaction history, still give new customers no path to prove themselves, still ignore purchase amount and category, and still treat a checkout misclick or a good-faith retry after a wrongful decline the same as genuine repeat risk-seeking. Building an in-house AI-generated scorecard instead is what actually lets Helios Pay weight its own history properly, extend credit to new customers starting with a smaller first purchase, treat amount and category as real inputs, and tell a real credit request apart from checkout noise — domain knowledge only Helios Pay is positioned to have, and that no scorecard it merely pays for, bureau or otherwise, would fully use.

### Network Loop - 2/5
**What you capture today:** Helios Pay's own applicant and outcome data does feed back into the model — but only once a year. Credit Risk shares customer data with Statistical Decisions Hellas annually so the scorecard can be reviewed and adjusted, and getting anything actually changed depends on Credit Risk actively challenging Statistical Decisions Hellas's own view of the model and making the case for what's wrong with it — the data doesn't speak for itself. And the evidence available for that case has a structural hole: an applicant who's rejected never gets the chance to repay, so there's no real outcome data to prove a declined applicant would have been a good customer. That gap falls hardest on applicants new to Helios Pay, who have the least other evidence in their favor — precisely the group the annual review is least able to build a case for. 

**How it compounds:** Once a year, and only for the applicants Helios Pay actually approved. Every rejection is a data point Helios Pay can never use to argue the model was wrong, so the population most likely to reveal a miscalibrated score — declined applicants who would have paid — never accumulates into evidence at all. An in-house AI model that retrains continuously, instead of waiting for an annual, negotiated review, is what shortens this cycle; deliberately extending credit to some new or marginal applicants on smaller amounts first — the same fix Domain Context points to — is what actually starts generating the outcome data this process structurally can't produce today.

**Total Flywheel Score: 7/20**

**Weakest Loop:** Domain Context

At 1/5, this is the clear low point, and the gap is more literal than it might sound: Helios Pay isn't just under-using BNPL-specific insight, it's still scoring every BNPL application today against a bureau template built for an entirely different kind of lending — one that also can't tell a genuine credit request apart from a checkout misclick, or a good-faith retry after a wrongful decline apart from real repeat risk. The bureau's own BNPL-specific fix already exists, but adopting it means paying for a scorecard that would still outweigh what Helios Pay itself knows about a given customer's behavior with Helios Pay directly, still give new customers no path to prove themselves, and still ignore the specific purchase's amount and category. That's exactly the domain knowledge Helios Pay is uniquely positioned to have and a purchased scorecard structurally can't hold — and it's a real part of why a segment defaulting at a materially higher rate went unaddressed for as long as it did.

**Fix for weakest loop:** This is the build-vs-buy decision this loop actually turns on. Paying the bureau for its BNPL-specific scorecard fixes the loan-type mismatch but not the domain gap underneath it. Building an in-house AI-generated scorecard is what lets Helios Pay weight its own transaction and repayment history as the primary signal, give new customers a real path to build history starting with a smaller first purchase, add purchase amount and category as direct scoring inputs, and distinguish a real application from checkout noise or a wrongful-decline retry — the clearest source of edge available, and one no bought scorecard delivers.

---

## Encroachment Threat Assessment

### 1. Platform Encroachment

**Attacker:** Revolut 

**Vector:** Platform Encroachment 

**Time-to-threat:** Uncertain, but not distant. Revolut already has full Greek market access and a working BNPL product elsewhere in Europe — bringing it to Greece is an expansion decision, not a new-product build. No Greek launch has been confirmed. 

**% of value at risk:** ~30-40% (estimate)


### 2. Vertical Competitor
**Attacker:**
**Vector:**
**Time-to-threat:**
**% of value at risk:**

### 3. Adjacent Expansion
**Attacker:**
**Vector:**
**Time-to-threat:**
**% of value at risk:**

---

## 90-Day Encroachment Plan

*Your partner played the Big Tech attacker. What was their plan to kill you?*

**Attacker:**
**Attack vector (target the weakest loop):**
**Weeks 1-4 - what they ship:**
**Weeks 5-8 - how they poach users:**
**Weeks 9-12 - why users don't come back:**
**Your defense:**
