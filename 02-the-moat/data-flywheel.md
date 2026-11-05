# Data Flywheel Map

> Score each loop 1-5. Your weakest loop is where competitors attack first.
> The four loops below are the M2 starting point - adapt if your product has 2 or 6 loops instead of 4.

## Flywheel Loops

| Loop | What It Measures | Score 1 | Score 5 | Score |
|------|------------------|---------|---------|-------|
| **Correction** | Do users fix AI outputs? Is that signal captured and reused? | No capture | Automated retraining | 2/5 |
| **Preference** | Does the product learn individual / team preferences over time? | Stateless | Deep personalization | 1/5 |
| **Domain Context** | Does usage in one area improve quality in adjacent areas? | Siloed | Cross-domain transfer | 3/5 |
| **Network** | Does each new user / team make the product better for everyone? | Isolated | Strong network effects | 1/5 |

### Correction Loop - 2/5
**What you capture today:** Final state only. When a user edits an AI Assist output (identified risk, assessment summary, mitigation proposal), we store the edited result. We do not store the original AI output, the diff, or an accept/reject/edit signal, so we can't tell what the AI got wrong.
**How it compounds:** It doesn't yet. The corrected text is useful to that customer's register and audit trail, but nothing flows back to improve prompts, rules, or the golden set. Correction data exists implicitly (edited vs. generated) and is lost the moment the AI original is overwritten.

### Preference Loop - 1/5
**What you capture today:** Nothing. AI Assist is stateless across sessions: each generation starts from the current inputs (e.g. the assessment being summarized) with no memory of what a user or team accepted, rewrote, or ignored before.
**How it compounds:** It doesn't. A team's tenth proposal is no better fitted to them than their first.

### Domain Context Loop - 3/5
**What you capture today:** Data from one workflow step feeds adjacent steps and modules: risk assessments ground mitigation proposals, and the register and assessment results connect across AI RE and other Diligent modules.
**How it compounds:** Within a customer, richer assessment and register data gives better-grounded downstream output, and the shared workflow spine spreads that context across modules. It is capped at 3 because this is context passed as grounding input at generation time, not learning: no model, ruleset, or benchmark improves from usage, and no transfer happens across customers.

### Network Loop - 1/5
**What you capture today:** No customer data is shared across tenants. The only shared asset is public: the SEC 10-K risk corpus, categorized by AI so customers can search it and add risks to their register.
**How it compounds:** It doesn't. A new customer doesn't make the product better for existing ones. The 10-K corpus grows with filings, not with our usage, and a competitor can ingest the same public data.

**Total Flywheel Score: 7/20**
**Weakest Loop:** Preference and Network (tied at 1/5). Network is the structurally weakest, since tenant isolation limits it by design. Preference is the weakest we can fix quickly.
**Fix for weakest loop:** Start with Correction capture, because it is the cheapest fix and feeds the other loops. Then build Preference on top of it:
1. Store the AI original beside the user's final version for every AI Assist output, plus an accept / edit / reject event and an optional reason. No new UX beyond a lightweight "why" on rejects.
2. Use that data in two ways: (a) as evaluation signal, feeding rejected or heavily edited outputs into the golden set and groundedness / usefulness checks; (b) as per-tenant preference memory, e.g. the team's preferred mitigation types, wording, and risk categories, injected as grounding in later generations.
3. Later, and opt-in only: aggregate anonymized patterns (which mitigations get accepted, which categories get edited) into cross-customer benchmarks. This is the only realistic path to a Network loop in a regulated, trust-first product.

> Scores reflect your answers on current capture. Domain Context is rated 3 rather than 4 because the cross-module flow is grounding, not learning. Correction is rated 2 rather than 1 because final-state edits are stored, though the AI original and the diff are not.

---

## Encroachment Threat Assessment

> Attackers are hypotheses based on public information (Nov 2026). Time-to-threat and % at risk are my estimates, not measured. Pressure-test them with your partner and sales/CS data.

### 1. Platform Encroachment
**Attacker:** Microsoft (Copilot, with Purview and Agent 365 for governance). OpenAI / Anthropic enterprise agents are a secondary attacker.
**Vector:** A Copilot agent over a customer's own risk documents, SharePoint risk registers and 10-K filings. It drafts risks, summarizes group assessments and proposes mitigations, inside the tools risk teams already use. This hits our weakest loops: with Preference at 1/5 and Correction at 2/5, we have no learned fit to a customer that a platform with the same documents can't match. Microsoft has no dedicated enterprise-risk agent yet. Public material shows Purview adding risk controls for AI agents, and Directions on Microsoft (Oct 2026) says Microsoft is cautious about AI in its own GRC services. The threat is a horizontal agent, not a GRC product.
**Time-to-threat:** 6-12 months for "good enough" drafting, summarization and mitigation suggestions from customer documents. 18-24+ months for auditable, grounded output with a claim-level trail, which is our groundedness and evaluation edge.
**% of value at risk:** ~35% of AI-attributable value, i.e. the generation features: identification, summaries, proposals. The risk register, assessment workflow and audit trail (system of record) stay mostly intact in the near term. Estimate, not measured.

### 2. Vertical Competitor
**Attacker:** AuditBoard (G2 now lists it as Optro, formerly AuditBoard). I could not verify a specific niche startup, so I'm naming the established vertical player. It is deeper in audit, controls and compliance, and has agreed to acquire FairNow (AI governance registry, dynamic risk assessments, automated compliance); I did not confirm the deal closed.
**Vector:** Link risks to control tests, audit evidence and compliance results, then use AI to propose mitigations tied to measured control effectiveness. This is the data we lack. We can generate a mitigation plan from an assessment. They can show whether similar controls passed testing. They can also win the AI-risk-governance niche that AI RE buyers are starting to ask about.
**Time-to-threat:** Already present in competitive deals with audit-led buyers. Within 12 months for control-informed mitigation proposals. Their AI so far has focused on drafting risk/control descriptions and vendor assessments; review-site feedback on their risk assessment and scoring is mixed, which is our opening.
**% of value at risk:** ~20-25% of the addressable base, in audit-led or compliance-heavy accounts where mitigation grounded in control data matters. Estimate, not measured.

### 3. Adjacent Expansion
**Attacker:** ServiceNow (IRM, with Now Assist for IRM). Oracle, SAP and Workiva-style suites are possible but less direct.
**Vector:** Add risk AI as "one more thing" on the platform where IT, security and operations already run. ServiceNow ships a Risk Suggestion AI agent and agentic workflows for IRM (March 2026 release docs), lets customers choose model providers, and in some releases activates the skills by default after install. It is sold bundled into existing contracts, so a risk team can get AI risk features without a separate purchase or procurement cycle.
**Time-to-threat:** Already shipping. It is a threat now for customers on ServiceNow, and the gap to ours narrows with each quarterly release.
**% of value at risk:** ~25-30% of pipeline and renewals in accounts already on ServiceNow, where "free with the platform" competes with our price. Estimate, not measured.

---

## 90-Day Encroachment Plan

*Your partner played the Big Tech attacker. What was their plan to kill you?*

> Written as the strongest attack I could build against AI RE as it is today (flywheel 7/20). It is a hypothesis to run through the partner role-play, not a forecast.

**Attacker:** Head of Product, Microsoft Copilot (M365 Copilot + Copilot Studio + Purview)

**Attack vector (target the weakest loop):** Preference (1/5). AI RE is stateless, so every user gets generic output. Copilot already knows each user and team through Microsoft Graph: their past risk memos, board decks, emails and edits. We make Copilot the AI that "writes risk like your team does" and bundle it into licenses the customer already pays for. AI RE's remaining value then shrinks to a database.

**Weeks 1-4 - what they ship:** A "Risk & Resilience" agent in Copilot Studio, free with M365 Copilot. It:
- drafts risk statements, summarizes assessment results (including group workshops held in Teams), and proposes mitigations grounded in the customer's own SharePoint, Excel and Teams content;
- reads public 10-K risk factors, which replicates our SEC categorization, since the data is public;
- adapts to each user's edits through Copilot memory, so quality improves visibly in the first week.

**Weeks 5-8 - how they poach users:**
- Import: a one-click importer for registers exported from AI RE (CSV/API), shipped with Big 4 and GSI partners who already run implementation projects.
- Distribution: pitch to the CFO, CISO and CRO, who are already in Teams and Outlook. Free pilots with M365 E5 customers: "No new tool, no new login, no new budget."
- Trust: use Purview audit logs, sensitivity labels and data-residency controls to neutralize our "governed AI" story.
- Teams: AI RE users get nudges inside Teams and Excel, where their risk work actually happens.

**Weeks 9-12 - why users don't come back:**
- Their drafts now sound like the team and keep getting better, while AI RE's stay generic.
- Risk owners work inside Teams, Excel and Outlook, so opening a separate AI RE tab becomes an extra step.
- AI RE quietly becomes a read-only archive, and the next renewal is framed as "we already pay for Copilot."
- Switching costs fall because the register is exportable and the AI value was never in the data.

**Your defense:** Make AI RE the system of record that Copilot depends on, and fix Preference before week 4.
1. **Weeks 1-4, capture corrections.** Store the AI original, the final version, the diff and an accept/edit/reject event on every AI Assist output (see Correction loop fix). This is the base for everything else.
2. **Weeks 3-8, ship per-tenant preference memory.** Seed it from each customer's existing register, past edits and strategy settings. The pitch becomes "AI RE gets more like your team every quarter," not generic output.
3. **Position on trust Copilot can't match.** Claim-level groundedness, the hard groundedness gate, and an auditor-ready trail of who accepted or changed what, exportable for audit. A generic agent can draft, but it can't prove the output is grounded in the assessment.
4. **Don't fight Copilot where users work.** Expose AI RE inside Teams and Copilot (Teams app, plugin or MCP/API) so Copilot reads from and writes to the AI RE register. We become the governed backend, which keeps the system of record and the audit trail.
5. **Use Diligent's distribution.** Bundle with the board and governance suite already in front of the CRO and board, with board-ready risk reporting no Copilot agent produces.
6. **Open the Network loop, opt-in.** Start the consent model for anonymized benchmarks (which mitigations get accepted, which risks get edited) so there is a cross-customer signal Microsoft can't get from one tenant's Graph.

**Biggest open risk:** Defense items 1-2 are work we haven't started and need engineering capacity. If corrections aren't captured by week 4, the attack lands, because Preference stays at 1/5.
