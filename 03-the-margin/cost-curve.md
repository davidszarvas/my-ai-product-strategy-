# Cost Curve & Pricing Strategy

> Heads up: I don't have our real usage or price data, so the numbers below are my own estimates (marked "assumed"). The class said structure matters more than exact numbers. Swap in real numbers when we have them.

## Packaging Decision

| | Feature |
|---|---|
| **Leader** | AI mitigation proposals (grounded in the customer's risk assessments). This is what people come for. |
| **Filler** | 10-K risk categorization and summaries of group assessments. Nice to have, cheap to run. |
| **Killer** | Bulk or "agent" jobs, like regenerating proposals for a whole risk register at once. Heavy and expensive. Not shipped yet. |
| **Killer usage %** | ~30% of users (assumed, to be checked) |
| **Bundle or add-on** | Add-on. Under the 70% rule, so bundling it would make everyone pay for our heaviest users. |

## Cost Model

Assumed: about 200 AI requests per user per month. Rough cost per request: small model $0.003, mid model $0.02, frontier model $0.10.

| Cost Category | Per-User/Month | Notes |
|--------------|----------------|-------|
| Inference (primary model) | $4.00 | 40 requests (20%) go to the frontier model at $0.10. Mostly mitigation proposals. |
| Inference (cascading/triage) | $1.33 | 110 simple requests at $0.003 + 50 medium requests at $0.02 (10-K tagging, summaries). |
| Infrastructure | $2.00 | Hosting, APIs, the cloud setup. Mostly fixed, so I split it across users. |
| Data/storage | $0.75 | 10-K corpus, embeddings, customer risk data and the audit trail. |
| Human-in-the-loop | $1.50 | Reviewing sample outputs and keeping the golden set up to date. |
| **Total AI COGS** | **$9.58** | About $5.33 of that is model cost. |

If we sent everything to the frontier model, inference alone would be 200 × $0.10 = $20/user/month and AI COGS would be about $24. Cascading saves roughly $14.67 per user.

## Cascading Strategy
<!-- Cheap model → frontier model routing logic -->

**Triage model:** A small, cheap model (Haiku-class or mini-class) for simple stuff, plus a mid-size model for medium stuff.
**Frontier model:** A top-tier model, only for mitigation proposals that need careful grounding in the assessment.
**Routing rule:** Simple tasks (tagging 10-K risks, short summaries) go to the small model. Medium tasks (group assessment summaries) go to the mid model. Mitigation proposals go to frontier. If a cheap model's answer fails the groundedness check, it escalates to the frontier model.
**Expected cascade ratio:** 80% / 20% (55% small, 25% mid, 20% frontier). I'll test 70/30 and 60/40 too, since our quality bar is high and we might need more frontier.

Blended cost is about $0.027 per request (0.55 × $0.003 + 0.25 × $0.02 + 0.20 × $0.10).

## Pricing Model

**Current pricing:** Seat-based, about $40 per user per month (assumed, replace with the real number). Traditional COGS is about $6/user, so gross margin is around 85%.
**Proposed AI pricing:** Hybrid. $45 per user per month base, plus $1.00 per accepted mitigation proposal. The unit of work is one accepted mitigation proposal. I'm assuming about 20 per user per month, so about $65 revenue per user per month. Strategy: maximize, because it's regulated work where trust matters more than price.
**Model:** hybrid

I picked "accepted" proposals on purpose. Customers only pay when the AI did useful work, which is like Intercom charging per resolved conversation. It also gives us a reason to capture accept/edit/reject (see data flywheel).

## Stress Tests

Baseline: total COGS is $15.58 ($6 normal + $9.58 AI). Hybrid price is $65, giving a 76% margin. If we just bundled AI into the $40 seat, margin would be 61%.

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x | Model cost goes from $5.33 to $16.00, so total COGS is $26.25. Hybrid: 60% margin. Flat $40: 34%, which is below 40%. | Push more requests to the small model, cache repeated queries, shorten prompts. This is also why we shouldn't bundle AI into a flat seat. |
| Heaviest segment doubles | Say the top 20% of users make about half the requests. Doubling them means 1.5x requests overall. Model cost is $8.00, total COGS $18.25. Hybrid: 76% (they also pay per proposal). Flat $40: 54%. | The hybrid price covers heavy users. Put bulk jobs in a paid add-on and set a fair-use limit on the base plan. |
| Model provider raises prices 50% | Model cost is $8.00, total COGS $18.25. Hybrid: 72%. Flat $40: 54%. | Switch some features to a backup model. This depends on the kill-switch work, because right now we're Locked and can't swap quickly. Also renegotiate the cloud contract. |

## Board One-Pager
<!-- Before/After: Old SaaS revenue vs. AI usage revenue for your product -->

**Before (traditional SaaS):**
- Revenue: $40 per seat per user per month
- COGS: $6 (mostly fixed)
- Gross margin: 85% ($34 per user)

**After (AI-enabled):**
- Revenue: $45 base + $1.00 × 20 accepted proposals = $65 per user per month
- COGS: $15.58 (about $9.58 is AI, and it's variable)
- Gross margin: 76% ($49.42 per user)

**Net margin shift:** Margin % drops about 9 points (85% → 76%), but gross profit per user goes up about $15.42 (+45%). The margin % falls because AI costs scale with usage, but we make more money per customer.

Narrative for the board: the lower percentage is fine because we earn more dollars per user. Cascading keeps costs under control, and charging per accepted proposal means heavy usage brings in revenue. The main risk is being locked into one model provider, so portability work (kill switch) is part of the plan. If we bundled AI for free, margin would drop to about 61% and we'd earn nothing extra, which is the thing to avoid.
