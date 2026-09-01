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

### Preference Loop - __/5
**What you capture today:**
**How it compounds:**

### Domain Context Loop - __/5
**What you capture today:**
**How it compounds:**

### Network Loop - __/5
**What you capture today:**
**How it compounds:**

**Total Flywheel Score: __/20**
**Weakest Loop:**
**Fix for weakest loop:**

---

## Encroachment Threat Assessment

### 1. Platform Encroachment
**Attacker:**
**Vector:**
**Time-to-threat:**
**% of value at risk:**

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
