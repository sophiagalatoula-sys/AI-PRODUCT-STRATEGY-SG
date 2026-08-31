# The Prototype Bet

## What I Built
<!-- One sentence: what does this prototype demonstrate? -->
An AI-enhanced credit risk model for Greece BNPL, prototyped as a three-screen Credit Decision Console. At its core, the model's job is feature selection: figuring out which signals Helios Pay already holds about its own customers — signals the external credit bureau never sees — actually predict repayment, so the credit score can both approve genuinely creditworthy customers the bureau's more conservative, one-size-fits-all view would have rejected, and decline risky customers the bureau's score would have wrongly approved and who would otherwise go on to default. Two kinds of signal feed it: customer-profile data (age, gender, education, marital status, income, existing debt and expenses, and digital-footprint signals such as the number of emails and phone numbers associated with an applicant and their presence across social platforms) and transactional data (prior BNPL and general-purpose loan history with Helios Pay, on-time repayment record, and purchase behavior — merchant, category, and amount).

Screen one shows how that model actually gets used day to day, not just what it scores. Sending every application to manual review isn't workable — the underwriting team isn't large enough, and a BNPL decision has to come back instantly — so the model auto-decides applications where it agrees with the legacy bureau verdict, and routes to an underwriter only the applications where it disagrees. That disagreement is the trigger for review: during the pilot, the underwriter's job on each of these cases is specifically to confirm or correct the new model's call, which is also how the model gets fine-tuned on exactly the cases it's least sure about. The screen shows an analyst that exact moment — the legacy score and verdict next to the new model's score and verdict, with a plain-language reason behind each — rather than asking them to trust a black-box number. Screen two shows what this is meant to move at the portfolio level: the approval-rate gap and the higher-risk segment's default rate. Screen three shows the applicant's own outcome, approved or declined, in plain language.

## Tool Used
<!-- v0 / Cursor / Lovable / other -->
Claude

## Prototype Link
<!-- Paste the shareable URL -->
https://claude.ai/code/artifact/a63d5335-d609-4a88-b756-920464dc35d7

## AI Value Archetype
<!-- Automator / Copilot / Oracle / Creator / Orchestrator -->
Copilot

## The Bet in One Sentence
<!-- What you're building, for whom, why now -->
For a BNPL lender sitting on years of its own customer-profile and transaction data that the external credit bureau never sees, we're betting that using AI to identify which of those signals actually predict repayment — auto-deciding the applications where the resulting model agrees with the legacy bureau score, and routing only the disagreements to a small underwriting team — both approves more of the customers the legacy scorecard wrongly rejects and declines more of the customers it wrongly approves who go on to default, preventing losses in the higher-risk segment without demanding a review volume no underwriting team could sustain or slowing down BNPL's need for an instant decision.

## Kill Criteria
<!-- When would you stop? What evidence would kill this bet? -->
