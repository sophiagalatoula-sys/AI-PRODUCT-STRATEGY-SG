# Three-Axis Vulnerability Diagnostic

## Product
<!-- Name the product you're diagnosing. Real product at your company — not a hypothetical. -->

**Product:** A digital wardrobe app. Users catalog the clothes they own by photographing items or automatically importing a product image at the point of an online purchase, and get a personal avatar sized to their own measurements. Users describe an occasion and receive an outfit suggestion — first assembled from clothes they already own, and only if nothing suitable exists, drawn from an AI search of e-shops — visualized on their avatar. The app also lets users set explicit style preferences, collects fit feedback per brand and size, and includes an honesty mechanic that flags already-owned duplicates at both cataloging and purchase time, routes worn-out or poor-fitting items toward resale or donation, and redirects spend toward genuine gaps in the wardrobe rather than repeats.

**Your Role:** Product Leader


---

## Scores

### Contextual Moat — 3/5
*Workflow depth × switching cost. Would users leave in a weekend if a competitor showed up?*

**Score rationale:** Cataloging a full wardrobe with photos, sizes, and purchase history takes real effort, and once a user has invested that time, they're unlikely to want to redo it elsewhere — a genuine switching cost. But the core mechanic isn't unique: Whering and Acloset already run a wardrobe-plus-outfit-suggestion loop at meaningful scale, so this product matches an existing pattern rather than leading one. Personal wardrobe management is also inherently lower-frequency than a work tool — usage tracks shopping cadence and how often the app proactively resurfaces the wardrobe, not daily necessity.

**Named attacker (from partner challenge):** Whering — already runs the wardrobe-plus-outfit-suggestion loop live with a large user base, and could plausibly add an avatar and active cross-retailer search faster than this product could build a comparable user base from zero.



---

### Data Advantage — _3/5
*Proprietary signal that compounds with usage. What do you see that OpenAI doesn't?*

**Score rationale:** The product is designed to build a genuine per-user data loop: accumulated liked outfit combinations, explicit stated style preferences, and brand/size-level fit feedback tied to the user's avatar measurements. Aggregated across users, this could become a cross-brand size-and-fit dataset that no single retailer currently exposes. The score is held at 3, not higher, because none of this is running yet — at launch, with close to no users, this is a well-designed mechanism for a compounding advantage, not a realized one.

**Named attacker (from partner challenge):** Zalando — its Virtual Fitting Room already collects real body-measurement-to-garment fit and return data at transaction scale, from actual purchases, putting it ahead on raw data volume even though its data is limited to its own catalog.


---

### Platform Exposure — 3/5
*Encroachment risk × pivot speed. If Apple/Google/OpenAI ships your hero feature native — then what?*

**Score rationale:** Two large platforms already ship pieces of this product's core mechanic: Zalando's 3D body-measurement avatar, and Google Shopping's AI Mode, which offers photo-based try-on and AI-driven product discovery across a massive catalog. This product's honesty mechanic — flagging owned duplicates at cataloging and purchase time, redirecting spend toward genuine gaps, and routing worn-out items to resale or donation — is a real business-model difference, since a commerce-driven platform profits from selling more and has a structural disincentive to build a sincere version of it. The score is held at 3, not higher, because a platform could still ship a shallow "you may already own this" prompt as a return-reduction feature without adopting the full anti-overconsumption approach.

**Named attacker (from partner challenge):** Google (Google Shopping AI Mode) — already ships photo-based virtual try-on and AI-driven product discovery across a massive, ad-monetized catalog; a saved-avatar wardrobe layer on top is a plausible incremental feature for them, not a research problem.


---

## Top Vulnerability
<!-- One line: what's the single biggest strategic risk? -->
Platform Exposure: Zalando's body-measurement avatar and Google's cross-catalog visual try-on already exist inside shopping apps people use today, and both have far more existing distribution than this product will have at launch.



## Confidence Level
<!-- H / M / L — how confident are you in this bet after the diagnostic? -->
