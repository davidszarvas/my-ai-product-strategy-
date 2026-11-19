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

**Thesis (1 sentence):** AI RE wins regulated risk teams because it is the AI that proves every claim against the customer's own assessments, and it gets better for each customer with every correction, which a general-purpose copilot can't match.

**The case:**
1. Why now: Frontier models have made drafting risks and mitigations nearly free, so the scarce thing is trust. Microsoft is moving into governance with Copilot, Purview and Agent 365. We have a short window to own "grounded AI for risk" inside the Diligent ERM workflow before customers default to a horizontal copilot.
2. What's defensible: Not the model. Our hero feature can be copied with a frontier model. What's defensible is (a) workflow depth across the Diligent ERM portfolio (Projects integration, continuous monitoring), (b) a groundedness gate and HITL design that auditors can inspect, and (c) correction and preference loops that compound per tenant. Our honest starting point: Preference and Network loops score 1/5 today. H1 and H2 exist to fix Preference.
3. The economics: Move from about $40/user/month seat pricing to a hybrid of $45 base plus $1 per accepted mitigation proposal, about $65/user/month at ~20 proposals. AI COGS is $9.58/user on an 80/20 cascade (55% small, 25% mid, 20% frontier). Gross margin drops from about 85% to 76%, but gross profit per user rises $15.42 (+45%). We get paid when the AI produces work the customer accepts.

**The risks:**
1. Trust / failure modes: A hallucinated or ungrounded mitigation in regulated work is a credibility-ending event. Mitigation: a groundedness gate on every proposal, HITL when confidence is under 70% or a proposal fails the gate twice, a weekly golden set and a monthly expert review of 50 random outputs.
2. Scale / governance: Bulk and agent jobs multiply both errors and cost. If quality forces a 60/40 cascade, COGS rises and the margin shrinks. Vendor portability is "Locked": swapping models means rewrites and re-validation. Mitigation: no agents until Agent Boundaries are defined (H3), cascade ratios tested in H1, COGS tracked monthly.
3. Competitive: Microsoft Copilot with Purview and Agent 365 is bundled and already in the tenant. OpenAI and Anthropic enterprise agents are a secondary threat. Mitigation: compete on grounding to the customer's own assessments and on depth inside the Diligent workflow, not on generation quality.

**The ask:** Approve a [6]-month validation of H1 + H2 with [N] design-partner tenants and [X] engineers + [1] domain expert reviewer. Go/no-go at month 3 on: correction capture ≥80%, golden-set groundedness ≥95% and accepted-proposal volume near the 20/user/month pricing assumption. If those miss, we stop the hybrid pricing move and revisit the Bet.

## M1 Baseline vs. Now
*Your 3-sentence AI strategy from Module 1 vs. what you'd say now:*

**M1 baseline:** *(reconstructed from the M1 summary; replace with your original wording)* AI RE adds AI Assist to every step of the risk workflow: identification, assessment and mitigation proposals. It is a Creator-archetype product that drafts risk work for users. We have medium confidence it differentiates on workflow depth and trust.

**Now:** AI generation alone isn't a moat, because a frontier model can copy it. AI RE has to win on proof: every proposal grounded in the customer's own assessments, gated and reviewable. Each accepted or corrected proposal makes it better for that customer. We price on accepted proposals, so we earn more when the AI does work customers trust, and we start with correction capture because every other loop depends on it.
