# Diligent AI Risk Essentials (AI RE), an AI-assisted risk management product

> We make the Diligent ERM portfolio the place risk teams do AI-assisted work they can defend to an auditor, and we charge for each mitigation plan they accept.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [x] | `01-the-bet/` |
| **The Moat** | M2 | [x] | `02-the-moat/` |
| **The Margin** | M3 | [x] | `03-the-margin/` |
| **The Contract** | M4 | [x] | `04-the-contract/` |
| **The Guardrails** | M5 | [x] | `05-the-guardrails/` |
| **The Pitch** | M6 | [x] | `06-the-pitch/` |

---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** Diligent AI Risk Essentials (AI RE), an AI-assisted risk management product within the Diligent ERM portfolio, with AI Assist at every step of the risk workflow: risk identification, risk assessment, and mitigation proposals grounded in customer risk assessments.
- **AI Value Archetype:** Creator
- **Vulnerability Scores:** _(add: Moat _/5 · Data _/5 · Platform _/5)_
- **Top Risk:** AI RE's hero AI feature is replicable with a frontier model, and we don't yet have a proprietary cross-customer data signal that compounds with usage, so differentiation rests on workflow depth and trust/grounding alone.
- **Confidence:** M
- **Kill Criteria:** If by month 3 of the pilot, customers don't accept our mitigation proposals measurably more often than a plain frontier-model draft from the same input, we stop the pricing change and re-scope. _(Threshold to be agreed with leadership.)_

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:**
- **Weakest Loop:** Preference and Network (tied at 1/5). Network is the structurally weakest, since tenant isolation limits it by design. Preference is the weakest we can fix quickly.
- **Top Encroachment Threat:** Microsoft (Copilot, with Purview and Agent 365 for governance). OpenAI / Anthropic enterprise agents are a secondary attacker.
- **Encroachment Defense:** Start with Correction capture, because it is the cheapest fix and feeds the other loops. Then build Preference on top of it:
- **Vendor Portability:** Locked. Three of four dimensions are High. A swap today means rewriting call sites, re-tuning prompts and re-validating by hand, so 48 hours is not realistic. The cloud hosting keeps Provider at Medium: other models likely sit behind the same account.

→ Details: [`02-the-moat/`](02-the-moat/)

---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):**
- **Gross Margin (AI-adjusted):**
- **Pricing Model:** hybrid
- **Pricing Today → Tomorrow:** Seat-based, about $40 per user per month (assumed, replace with the real number). Traditional COGS is about $6/user, so gross margin is around 85%. → Hybrid. $45 per user per month base, plus $1.00 per accepted mitigation proposal. The unit of work is one accepted mitigation proposal. I'm assuming about 20 per user per month, so about $65 revenue per user per month. Strategy: maximize, because it's regulated work where trust matters more than price.
- **Total AI COGS / unit:** $9.58
- **Cascading Strategy:** Triage: A small, cheap model (Haiku-class or mini-class) for simple stuff, plus a mid-size model for medium stuff.; frontier: A top-tier model, only for mitigation proposals that need careful grounding in the assessment.; ratio 80% / 20% (55% small, 25% mid, 20% frontier). I'll test 70/30 and 60/40 too, since our quality bar is high and we might need more frontier.
- **Net Margin Shift:** Margin % drops about 9 points (85% → 76%), but gross profit per user goes up about $15.42 (+45%). The margin % falls because AI costs scale with usage, but we make more money per customer.
- **Break-even at:**

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:**
- **Golden Dataset:** 10 rows, 3 adversarial
- **Confidence UX:** Tiered confidence plus a human-in-the-loop trigger. "Confidence" here means how many claims in the output are backed by the customer's assessment (our groundedness check), not just how sure the model sounds.
- **HITL Architecture:** - **When a human steps in:** (1) confidence is under 70%, (2) a proposal fails the groundedness check, or (3) the input looks weird (injection text, contradictory scores).…
- **Failure Mode Coverage:** *What failure mode did your partner find that you missed?*

→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)

**What breaks when this scales, and what compounds.**

- **Compounding System:** | Loop | Input | Output | Compounds? | Status | |------|-------|--------|-----------|--------| | Recursive Learning | User edits, accepts and rejects on AI outputs (risks, summaries, mitigation proposals) | Better prompt…
- **Governance Posture:** All AI Assist features in AI RE: 10-K risk categorization, group assessment summaries and mitigation proposals. It also covers future bulk or "agent" jobs, like regenerating proposals for a whole register.
- **Autonomy Boundaries:** Draft risks, tag 10-K risk factors, summarize assessments, draft mitigation proposals: auto.
- **Escalation Triggers:** Groundedness is under 70%. A proposal fails the groundedness check twice (once on the cheap model, once on frontier). The input looks strange: injection text in comments, or contradictory scores.…
- **Audit Cadence:** Real-time, groundedness gate on every proposal. Weekly, golden set run (PM). Monthly, a human reviews 50 random outputs and all escalations (Domain expert).…
- **Shadow AI Audit (user-side):** 5 workarounds found · 4 build candidates build candidates · adjacent spend $0/mo
- **Agent Boundaries:** _Not shipping agents this version._
- **Regulatory Exposure:** - EU AI Act: Probably limited risk. AI RE helps people make decisions.

→ Details: [`05-the-guardrails/`](05-the-guardrails/)

---

## The Pitch (M6)

**How you get this funded, shipped, and adopted.**

- **Horizon 1 (Now, 0-3 months):** Correction capture (≥80% of AI outputs with an accept/edit/reject signal) · AI-Powered Group Risk Assessments · Golden set 10 → 50 rows with a written reliability target · Accepted-proposal metering + AI usage analytics
- **Horizon 2 (Next, 3-9 months):** Preference loop (≥20% fewer edits per tenant) · Continuous Risk Monitoring (merged with Advanced Risk Indicator Monitoring) · Bidirectional Projects Integration
- **Horizon 3 (Bet, 9-18 months):** Financial Risk Quantification · Autonomous Risk Intelligence (only after Agent Boundaries are defined)
- **Board Narrative:** Thesis: we make ERM the place risk teams do AI work they can defend to an auditor, and we charge for each accepted mitigation plan. The case: users already work around us with AI (5 workarounds found) while Microsoft moves into governance; our defense is grounding against the customer's own assessment plus per-tenant correction and preference loops (1/5 today, which is what the funding builds); +$15.42 gross profit per user (+45%) at 76% margin. Risks: an ungrounded mitigation reaching an auditor (caught by the groundedness gate and HITL; test set still 10 cases), cost on rejected proposals at 10x usage, and Copilot matching our acceptance rate.
- **Ask:** 7 engineers + 1 PM for 6 months, go/no-go at month 3, fully loaded cost [$ — finance to fill in]. Paused if funded: federal deployment, cross-product issue management, financial risk quantification, autonomous agents, standalone analytics. Cross-portfolio trade-off still to name.
- **Key Strategic Change:** From "AI Assist at every step" to "proof plus learning": generation isn't the moat, grounding to the customer's own assessments and per-tenant correction loops are, and pricing follows accepted work.

→ Details: [`06-the-pitch/`](06-the-pitch/)
