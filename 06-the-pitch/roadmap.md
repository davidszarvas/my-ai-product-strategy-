# Three-Horizon Roadmap & Board Pitch

**Product:** Diligent AI Risk Essentials (AI RE)

## Roadmap

### Horizon 1 — Now (0-3 months)
*Quick wins. Ship with existing capabilities.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Correction capture: log every accept, edit and reject on AI outputs (Moat, M2's first move) | ≥80% of AI outputs (risks, summaries, proposals) have a captured accept/edit/reject signal | H |
| AI-Powered Group Risk Assessments (Bet) | 100% of summaries pass the groundedness gate; ≥60% accepted with light or no edits | H |
| Golden set expansion: 10 → 50 rows, ≥15 adversarial (Contract) | Weekly run in place; groundedness pass rate on golden set tracked and ≥95% | H |
| Accepted-proposal metering + AI usage analytics (Margin; reworked from "Unified Risk Analytics") | Billing-grade count of accepted proposals per user; actual AI COGS/user reported against the $9.58 target | M |

### Horizon 2 — Next (3-9 months)
*Bets. Requires new capabilities or integrations.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Preference loop on top of correction capture (Moat, fixes the weakest loop) | Per-tenant edit rate on mitigation proposals drops ≥20% vs. H1 baseline | M |
| Continuous Risk Monitoring, merged with Advanced Risk Indicator Monitoring (Bet) | ≥30% of pilot tenants act on a monitoring alert each month (re-assess or accept a proposal) | M |
| Bidirectional Projects Integration (Moat) | ≥25% of accepted proposals pushed to Projects, with status flowing back | M |

### Horizon 3 — Bet (9-18 months)
*Moonshots. High uncertainty, high potential.*

| Initiative | Metric | Confidence |
|-----------|--------|-----------|
| Financial Risk Quantification (Bet) | 100% of numeric claims grounded on a numeric adversarial golden set; ≥1 design partner uses outputs in board reporting | L |
| Autonomous Risk Intelligence: bulk/agent jobs, e.g. regenerating proposals for a whole register (Guardrails) | Agent Boundaries defined; escalation rate <10% at register scale; zero outputs skip the groundedness gate | L |

*Not on the roadmap: Federal Compliance & Deployment (no federal segment in the Bet, conflicts with vendor lock-in), Cross-Product Issue Management (platform plumbing, unless used as the HITL escalation queue). Updated Financial Risk Data runs as maintenance work.*

## Board Pitch

**Thesis (1 sentence):**
We make the Diligent ERM portfolio the place risk teams do AI-assisted work they can defend to an auditor, and we charge for each mitigation plan they accept.

**The case:**
1. Why now: Risk teams are already using AI outside our product. Our own audit found 5 workarounds, 4 of them worth building. At the same time, Microsoft is moving into governance with Copilot, Purview and Agent 365. If we don't own grounded AI inside the ERM workflow in the next two quarters, customers will default to the copilot already on their desktop, and our role shrinks to system of record.
2. What's defensible: Today, very little, and the pitch should say so plainly. A frontier model can copy our hero feature, and we have no data signal that pools across customers (tenant isolation rules it out by design). What we can defend is three things, two of which we have to build with this funding: (a) depth inside the Diligent workflow, (b) a check that proves every claim in a proposal against the customer's own assessment, and (c) a correction-and-preference loop that makes AI RE better for each customer the more they use it. That loop scores 1/5 today. Building it is most of what this ask buys.
3. The economics: +$15.42 gross profit per user per month (+45%). We move from about $40/user seat pricing to $45 base plus $1 per accepted mitigation plan, about $65/user. AI cost is about $9.58/user, so margin goes from 85% to 76%, but each customer is worth more. Gap: we have not stress-tested this. Break-even and the margin if quality forces heavier use of expensive models are both still blank, and the $40 and 20-plans-per-user figures are assumptions. Month 1 replaces all three with real numbers.

**The risks:**
1. Trust / failure modes: The front-page scenario is a regulated company adopting an AI-proposed mitigation that cites a control or fact that isn't in its own assessment, and an auditor or regulator finding it. How we catch it:
   - every proposal is checked against the assessment before a user sees it
   - anything under 70% backed, or failing the check twice, goes to a human
   - suspicious inputs are blocked
   - a domain expert reviews 50 random outputs and every escalation monthly

   Weakness, stated plainly: our test set is 10 cases and we have no written reliability target yet. Both are fixed in the first 4 weeks, before any customer pilot scales.
2. Scale / governance: At 10x usage, three things break.
   - Cost: we pay for every proposal but only earn on accepted ones, so a low acceptance rate turns usage into losses.
   - Review: 50 human checks a month doesn't scale with volume.
   - Lock-in: switching AI vendors today means rewriting and re-validating by hand.

   Bulk and agent jobs (for example, regenerating a whole risk register) are explicitly not in this ask. They wait until escalation is proven at volume.
3. Competitive: The kill scenario is Microsoft shipping risk drafting in Copilot that our pilot customers accept about as often as ours. Kill criterion: if by month 3 pilot customers don't accept our proposals measurably more often than a plain frontier-model draft from the same input, we stop the pricing change and re-scope. Gap: our original kill criteria were never written down. This line replaces them and needs a number agreed in this room.

**The ask:**
7 engineers + 1 PM for 6 months. Fully loaded cost: [$ — not in the strategy; finance to fill in]. Check-in at month 6, go/no-go at month 3.
- **Months 0–3:** capture every accept, edit and reject on AI output; AI-assisted group risk assessments; a 50-case test set with a written reliability target; billing-grade metering of accepted proposals.
- **Months 3–6:** a preference loop that learns from each customer's edits (target: 20% fewer edits), and two-way sync with Projects.

Paused if funded: federal deployment, cross-product issue management, financial risk quantification, autonomous risk agents, and a standalone analytics build. Gap: the cross-portfolio trade-off (which other team's bet waits) isn't in the strategy. Name it before the meeting.

## M1 Baseline vs. Now
*Your 3-sentence AI strategy from Module 1 vs. what you'd say now:*

**M1 baseline:** *(reconstructed from the M1 summary; replace with your original wording)* AI RE adds AI Assist to every step of the risk workflow: identification, assessment and mitigation proposals. It is a Creator-archetype product that drafts risk work for users. We have medium confidence it differentiates on workflow depth and trust.

**Now:** AI generation alone isn't a moat, because a frontier model can copy it. AI RE has to win on proof: every proposal grounded in the customer's own assessments, gated and reviewable. Each accepted or corrected proposal makes it better for that customer. We price on accepted proposals, so we earn more when the AI does work customers trust, and we start with correction capture because every other loop depends on it.
