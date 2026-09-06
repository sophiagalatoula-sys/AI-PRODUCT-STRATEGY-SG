# Compounding System Design

## Feedback Loops

| Loop | Input | Output | Compounds? | Status |
|------|-------|--------|-----------|--------|
| Recursive Learning | Underwriter decisions and justifications on the ~5% of applications routed for review, sampled in the existing weekly gold-set audit | Confirmed decisions become new golden-dataset rows; overturned ones flag a miss and feed the monthly Portfolio review model's characteristic-reweighting recommendations to Credit Risk | N | broken — the data-collection half runs on schedule, but nothing requires Credit Risk to act on a given month's recommendations, so the loop generates signal without a guaranteed path into an actual scorecard change |
| Cross-Domain Transfer | The holistic-judgment model's read of purchase amount, category, and merchant for every individual application in the pilot, which covers all applications rather than a single segment — whether this specific application's merchant, category, and amount should count as scoring signal, not what that merchant's whole history looks like across every application it's had (see Network Intelligence (merchant risk), below, for that). Category and merchant already carry narrow, fraud/dispute-only rules today (specific flagged merchants, the mobile category); amount carries none. All three are being assessed for broader, direct inclusion as credit-risk inputs in the new scorecard | A signal that's included is tested through the same pre-launch validation gate as the rest of the scorecard; a signal not yet included is meant to be surfaced by the holistic-judgment model as a recommendation to add it | N | broken — the same root cause as Recursive Learning above: nothing defines a cadence or a channel that commits Credit Risk to act on that recommendation once the holistic-judgment model makes it |
| Network Intelligence (fraud) | Device and browser fingerprints across all recent applications, cross-referenced against each other as the applicant pool grows | A shared-identity match routes an application to underwriter review regardless of what the applicant's own score would otherwise suggest; detection gets sharper as there are more applications to cross-reference against | Y | active |
| Network Intelligence (segment calibration) | Repayment and default outcomes across the full applicant population — not only routed cases — aggregated monthly by the Portfolio review model as the applicant base grows | Segment-level recalibration candidates for Credit Risk: evidence that a whole segment's scoring assumptions are off, not just that one flagged case was wrong | N | broken — same root cause as Recursive Learning and Cross-Domain Transfer above: the evidence compounds every month as more applicants generate outcomes, but nothing commits Credit Risk to act on what it shows |
| Network Intelligence (merchant risk) | None | None — no mechanism aggregates outcome patterns (fraud, disputes, early defaults) across Helios Pay's own merchant network as more merchants and transactions join it, the way the fraud-fingerprint check already does for applicants | N | missing |


**Broken loop identified by partner:**
**Fix plan:**

## Context Connectivity
<!-- How does knowledge flow across teams and domains? Where does it silo? -->

## Governance Policy

**Scope:**
**Autonomy boundaries:**
**Escalation triggers:**
**Audit cadence:**
**Regulatory exposure (EU AI Act / other):**

## Agent Topology
<!-- If using agents: what can each agent do? What can't it do? Who approves what? -->

## Shadow AI Audit

| Tool | Owner | Risk Level | Decision |
|------|-------|-----------|----------|
| | | H / M / L | keep / govern / kill |
| | | H / M / L | keep / govern / kill |
| | | H / M / L | keep / govern / kill |

**Total tools found:**
**Tools after triage:**
**Estimated hidden spend:**
