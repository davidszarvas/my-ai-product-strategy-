# Compounding System Design

> Product: Diligent AI Risk Essentials (AI RE). This is my first draft. Some numbers are my own guesses. I'll update it after the partner session.

## Feedback Loops

| Loop | Input | Output | Compounds? | Status |
|------|-------|--------|-----------|--------|
| Recursive Learning | User edits, accepts and rejects on AI outputs (risks, summaries, mitigation proposals) | Better prompts, rules and golden set cases | N | broken |
| Cross-Domain Transfer | Risk assessments and register data | Grounding for mitigation proposals and other Diligent modules | N | active |
| Network Intelligence | Anonymized, opt-in patterns across customers (which mitigations get accepted) | Benchmarks for all customers | N | missing |

Quick notes on each loop:

- **Recursive Learning:** We only save the user's final text. We lose the AI's original and the diff. So we never learn what the AI got wrong.
- **Cross-Domain Transfer:** This works, but it only scales. Assessment data is passed in as context. Nothing gets smarter from it.
- **Network Intelligence:** Not built. Each customer is kept separate by design. The only shared data is the public 10-K corpus, and anyone can use that.

**Freeze test:** If we froze AI RE for 3 months, we would be the same product. That means we scale, but we don't compound yet.

**Broken loop identified by partner:** Recursive Learning. Users fix AI outputs every day, but we throw that signal away.

**Fix plan:**
1. Save the AI original, the final version and the diff for every AI Assist output.
2. Add accept / edit / reject buttons with an optional one-tap reason.
3. Each week, add rejected or heavily edited outputs to the golden set.
4. Use the saved edits as team memory, so the next proposal fits that team better.
5. Later, with customer consent, build anonymized benchmarks. This is how we start the Network loop.

## Context Connectivity
<!-- How does knowledge flow across teams and domains? Where does it silo? -->

**Where knowledge flows:** Inside one customer, it flows well. Assessments feed mitigation proposals. The register connects to other Diligent modules.

**Where it silos:**
- **User corrections:** They stay in the register as final text. They never reach the AI team.
- **Between customers:** Every tenant is isolated. Good for trust, but nobody benefits from anyone else.
- **Support and CS:** They hear about user workarounds (like pasting into ChatGPT). This rarely reaches the product team in a structured way.
- **AI RE and the board suite:** Risk data and board reporting live in different places. Users rebuild board summaries by hand.

## Governance Policy

**Scope:** All AI Assist features in AI RE: 10-K risk categorization, group assessment summaries and mitigation proposals. It also covers future bulk or "agent" jobs, like regenerating proposals for a whole register.

**Autonomy boundaries:** Draft risks, tag 10-K risk factors, summarize assessments, draft mitigation proposals: auto.

**Escalation triggers:** Groundedness is under 70%. A proposal fails the groundedness check twice (once on the cheap model, once on frontier). The input looks strange: injection text in comments, or contradictory scores. The user asks for a human review. The user asks to add a fact or number that isn't in the assessment.

**Audit cadence:** Real-time, groundedness gate on every proposal. Weekly, golden set run (PM). Monthly, a human reviews 50 random outputs and all escalations (Domain expert). Quarterly, full policy review with security and legal (Legal).

**Regulatory exposure (EU AI Act / other):**
- EU AI Act: Probably limited risk. AI RE helps people make decisions.
- GDPR: Assessments can include names of risk owners and comments.
- FedRAMP.

**Controls:**
- A human always decides.
- We keep prompts minimal and don't train on customer data.
- Clear audit trail of who accepted or changed what.

## Agent Topology

_Not shipping agents this version._

## Shadow AI Audit

### Discover: User-Side Workarounds

| Workaround | Source | Signal | Frequency | Spend | Decision |
|------------|--------|--------|-----------|-------|----------|
| Pasting assessment results into ChatGPT or Copilot to write board-ready summaries | User interview | Capability gap | H | $0/mo | Build |
| Pasting AI RE proposals into ChatGPT to rewrite them in the team's own style | User interview | Capability gap | H | $0/mo | Build |
| Pasting proposals into ChatGPT to "double-check" if they are right | Sales call | Trust gap | M | $0/mo | Build |
| Exporting the register to Excel and using Copilot to make charts and heatmaps | User interview | Capability gap | M | $0/mo | Build |
| Using ChatGPT to regenerate many proposals at once, to avoid the bulk add-on | User interview | Capability gap | M | $0/mo | Ignore |

### Pattern Assessment

- Workarounds found: 5
- Build candidates: 4
- Partner candidates: 0
- Ignore decisions: 1
- Adjacent spend: $0/mo
- Dominant signal: Capability gap

### Action Plan

**Build:** The first three are core to our product. Board summaries fit Diligent's board suite. Team style is the preference fix. The "double-check" one means we need to show sources more clearly. Excel charts and heatmaps should be built into AI RE, so users don't need to export.

**Partner:** I don't see any partnership opportunity.

**Ignore + Monitor:** Bulk risk workshop generation is rare. It's fine for now. I'll watch it.

### Roadmap Brief

Based on my audit: 5 user-side workarounds discovered.
Decisions: 4 build · 0 partner · 1 ignore · 0 TBD.
Estimated adjacent spend: $0/mo across surveyed users.
Dominant signal: Capability gap.

**Recommended next step:** Capability gaps dominate. Users want something our product does not do. The strongest near-term move is to build one or two of these natively before a competitor does.

Sequence the Build column by frequency × strategic relevance. Re-run this audit each quarter, because workarounds shift fast.

**Total tools found:** 5
**Tools after triage:** 4 build candidates
**Estimated hidden spend:** $0/mo
