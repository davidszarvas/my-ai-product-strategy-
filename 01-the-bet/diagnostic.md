# Three-Axis Vulnerability Diagnostic

> Draft based on limited context (AI RE skill descriptions only). Scores and attackers are hypotheses to pressure-test, not validated findings.

## Product

**Product:** Diligent AI Risk Essentials (AI RE), an AI-assisted risk management product within the Diligent ERM portfolio, with AI Assist at every step of the risk workflow: risk identification, risk assessment, and mitigation proposals grounded in customer risk assessments.
**Your Role:** Product Manager, AI Risk Essentials

---

## Scores

### Contextual Moat: 3/5
*Workflow depth × switching cost. Would users leave in a weekend if a competitor showed up?*

**Score rationale:** The risk register, assessments, and mitigation plans are system-of-record data that live inside AI RE, so leaving means migrating the customer's risk history and re-establishing audit trails. That is real stickiness. It is capped at 3 because "Essentials" implies a lighter, easier-to-adopt tier, and lighter tiers have lower switching costs. AI Assist is embedded across the workflow: in risk identification, AI categorizes SEC 10-K risk data so customers can search it and add relevant risks to their register, and in risk assessment, AI summarizes results after a group assessment. That embedding raises the cost of leaving, but the AI capabilities themselves (categorization, summarization, proposal generation) are replicable on the same inputs with a frontier model, so the moat comes from the workflow and the customer's risk data, not the AI.

**Named attacker (from partner challenge):** Hypothesis, to be confirmed with your partner: ServiceNow IRM / Archer, which already own enterprise risk workflows and can bundle AI into existing contracts.

---

### Data Advantage: 2/5
*Proprietary signal that compounds with usage. What do you see that OpenAI doesn't?*

**Score rationale:** Each customer's assessments are private and the generator is grounded in them, so output quality is tied to customer-specific context. But nothing visible so far shows a cross-customer signal compounding with usage (benchmarks, which mitigations actually reduce risk, control-effectiveness outcomes). Today the data is an input to the AI, not a learning flywheel. Any competitor with the same customer inputs and a frontier model could produce similar proposals.

**Named attacker (from partner challenge):** Hypothesis: OpenAI / Anthropic enterprise offerings paired with a customer's own documents, plus GRC-native competitors (e.g. OneTrust, LogicGate) building their own AI features.

---

### Platform Exposure: 3/5
*Encroachment risk × pivot speed. If Apple/Google/OpenAI ships your hero feature native, then what?*

**Score rationale:** The hero capability, AI Assist across identification, assessment, and mitigation proposals, is largely a commodity LLM task a horizontal platform or Microsoft Copilot could do with the right documents. Mitigating factors: customers in regulated risk and compliance work need grounding, auditability, and governance, which horizontal tools handle poorly. The grounding-and-evaluation discipline (hard groundedness gate, claim-level checks) is the defensible part and the team can pivot toward it quickly. Exposure is moderate, not low.

**Named attacker (from partner challenge):** Hypothesis: Microsoft Copilot (embedded in the tools risk teams already use) and OpenAI's enterprise agents.

---

## Top Vulnerability

AI RE's hero AI feature is replicable with a frontier model, and we don't yet have a proprietary cross-customer data signal that compounds with usage, so differentiation rests on workflow depth and trust/grounding alone.

## Confidence Level

**M**: The strategy (trust-first, verifiable AI) is coherent and fits regulated buyers, but the moat and data scores rest on assumptions I could not verify. Confidence rises to H if you can show a compounding data signal or evidence of real switching costs.
