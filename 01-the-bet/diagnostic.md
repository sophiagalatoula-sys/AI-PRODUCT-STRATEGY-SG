# Three-Axis Vulnerability Diagnostic

## Product
<!-- Name the product you're diagnosing. Real product at your company — not a hypothetical. -->

**Product:** Helios Pay — a Greek digital lender that was the first BNPL (buy-now-pay-later) provider in the Greek market, now the second-largest after Klarna. This diagnostic covers an initiative to enhance the credit-risk decisioning model with AI/ML and alternative data, reducing dependency on Tiresias (Greece's credit bureau) and addressing a higher-risk applicant segment — roughly a tenth of monthly originations — defaulting at a rate in the high-20s percent, an estimated €550,000–600,000 in preventable losses per year.

**Your Role:** Product Leader (BNPL). I cooperated with the Credit Risk team on this initiative rather than owning it outright, as the business-side stakeholder for the BNPL product line the model serves.



---

## Scores

### Contextual Moat — 2/5
*Workflow depth × switching cost. Would users leave in a weekend if a competitor showed up?*

**Score rationale:** Helios Pay was Greece's first BNPL provider — genuine first-mover position, not simply "years in market." That advantage eroded through the company's own credit infrastructure, not through a better competing product. Before Helios Pay entered, Greek systemic banks only offered higher-value, longer-tenor loans, so the market's shared credit bureau scorecard was calibrated for that repayment pattern. BNPL's actual repayment behavior is different — a smaller purchase, first installment due immediately, the remainder over roughly three months — and applying a scorecard built for the wrong lending pattern made approval too conservative: roughly 60% versus Klarna's roughly 85%. The effect was concrete, not hypothetical: rejected customers learned Klarna approved more easily and made it their default choice going forward, and merchants fielding customer complaints about the rejection rate began preferring Klarna when they had to integrate with only one BNPL provider. The bureau has since built a separate, BNPL-specific scorecard using data collected since 2021, which should narrow the approval-rate gap — but whether it has fully closed it, and whether merchant and customer preference already formed for Klarna has reversed, isn't confirmed. Score held at 2 to reflect a moat actively eroded by self-inflicted underwriting infrastructure, not the more generous position "years of incumbency" alone would suggest.

**Named attacker:** Klarna — became the default choice for rejected customers and undecided merchants specifically because Helios Pay's own underwriting infrastructure rejected good customers too often, a self-inflicted vulnerability more than a product one.




---

### Data Advantage — 2/5
*Proprietary signal that compounds with usage. What do you see that OpenAI doesn't?*

**Score rationale:** Helios Pay has generated a genuinely valuable asset: years of ground-truth loan-outcome data — who defaulted, who repaid reliably — on BNPL's specific short-cycle repayment pattern, dating to 2021. The market's only BNPL-specific credit bureau scorecard was built using this data, after the bureau recognized its original scorecard didn't fit BNPL. Klarna does not route its Greek customer data through the same bureau, meaning this accumulated outcome data is likely disproportionately Helios Pay's own contribution to the market's shared credit-risk picture — Helios Pay effectively bootstrapped the only BNPL-specific scorecard in this market with its own data. Despite that, the score is held at 2: none of this value compounds as Helios Pay's own advantage today. It flows into a bureau product, and the independent scorecard-consultancy layer that might otherwise have helped Helios Pay capture this value separately (Statistical Decisions Hellas) was acquired by the bureau itself. The party best positioned to compound Helios Pay's own data into a durable edge is the bureau being paid for it, not Helios Pay.

**Named attacker:** Not a traditional competitor. The bureau (Tiresias, now including its Statistical Decisions Hellas subsidiary) functionally captures the compounding value of Helios Pay's own loan-outcome data, since Helios Pay pays for access to a scorecard built predominantly from data it originated.



---

### Platform Exposure — 4/5
*Encroachment risk × pivot speed. If Apple/Google/OpenAI ships your hero feature native — then what?*

**Score rationale:** The most acute threat isn't a hypothetical one — it's an existing commercial partner. Hellas Direct, a Greek digital insurer, already offers installment financing to its own customers through bank partnerships that include Helios Pay, and has filed a full application with the Bank of Greece for its own credit-provision licence, expected within the same year it was filed. Once licensed, Hellas Direct plans to expand well beyond its current auto-related financing into vehicle acquisition loans, leasing, and repair financing — a market it sizes at €2–3 billion annually against only €200–300 million currently bank-financed — built on its own insurance-customer risk data rather than a bank partner's. An insurer that already knows this market's approval-rate friction firsthand, moving to originate credit itself instead of routing customers through partners, is a direct and near-term threat to both distribution and revenue, not just a future one. Separately, Revolut has launched Greek IBANs, giving it full local market access, already offers a "Pay Later" BNPL product in at least one European market with stated plans to expand across Europe, and holds a global transactional-behavior dataset across roughly 75 million customers — an alternative-data advantage no local or regional player can match, even without a confirmed Greek BNPL launch yet. And Klarna, the market's scale leader, has already built its own credit-assessment capability rather than depending on the local bureau — demonstrating that the market leader has already solved the exact dependency problem this initiative is trying to solve. Score held at 4, not 5, because none of these has yet shipped a live, at-scale BNPL product specifically targeting Helios Pay's segment in Greece — Hellas Direct's licence is pending, Revolut's Greek BNPL plans are unconfirmed. Not held lower, because the threats are diversified across genuinely different vectors — an existing partner turning competitor, a global neobank with vastly superior data, and a direct competitor with independent underwriting — rather than resting on one speculative attacker.

**Named attacker:** Hellas Direct — an existing commercial partner with a Bank of Greece credit licence in progress, already planning to reduce its reliance on bank partners for financing once licensed, and building its own credit assessment on a different, non-bank dataset it already owns.



---

## Top Vulnerability
<!-- One line: what's the single biggest strategic risk? -->
Technically tied at 2/5 with Contextual Moat, but Data Advantage is the actual crack, because it's the upstream cause and Contextual Moat's weakness is the downstream symptom. Helios Pay's first-mover advantage eroded into "merchants and customers default to Klarna" not because of a worse product, but because of underwriting infrastructure Helios Pay doesn't own, calibrated for the wrong kind of lending, that rejected good customers too often. Bringing the scoring capability in-house, built on data Helios Pay already owns, gives the Contextual Moat symptom a real chance to reverse, because the root cause gets addressed. Fixing Contextual Moat directly, without fixing Data Advantage first, would mean chasing a symptom: better merchant incentives or marketing wouldn't change an approval rate still bottlenecked by a scorecard Helios Pay doesn't control. Helios Pay's most defensible potential asset — years of proprietary, ground-truth BNPL loan-outcome data that literally built the market's only BNPL-specific scorecard — currently compounds as value for the bureau that holds it, not for Helios Pay. Closing that gap is this initiative's real strategic point, with cost savings and segment-level default reduction as the visible, fundable justification layered on top.





## Confidence Level
<!-- H / M / L — how confident are you in this bet after the diagnostic? -->
**Medium.** The diagnostic surfaced a real, addressable root cause — bring the scoring capability in-house, built on data Helios Pay already owns — with a quantified upside (an estimated €550,000–600,000 in preventable annual losses) and a working design for how to do it without overwhelming a small underwriting team. That's enough to bet on. It falls short of high confidence because two of the three axes score at the bottom of the range (Contextual Moat and Data Advantage both 2/5), Platform Exposure sits at 4/5 against four converging real threats, and executing the fix depends on capabilities Helios Pay doesn't yet have proof it can build — a functioning correction loop, a properly weighted internal scoring model, and real independence from a bureau relationship that today is both uncorrectable and largely opaque from Helios Pay's side. The bet is worth making. It is not a low-risk one.
