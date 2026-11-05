# Kill Switch Audit

**Product:** Diligent AI Risk Essentials (AI RE), AI Assist across risk identification, assessment summaries and mitigation proposals.
**Goal:** 48-hour swap readiness: replace the primary model vendor within 48 hours without losing quality or the groundedness gate.

> Current-state answers are yours; risk ratings and actions are my recommendations to pressure-test with engineering.

## Vendor Dependency Assessment

| Dimension | Current State | Risk Level | 48-Hour Action |
|-----------|--------------|------------|---------------|
| **Provider** | One model family, hosted via a hyperscaler (Bedrock / Azure OpenAI). Contract, security review and data-residency terms already cover the cloud account. | **M** | Confirm which other model families are enabled and approved in the same cloud account (and pass the Diligent security/legal review), so a swap needs no new procurement. |
| **Abstraction** | Feature code calls the vendor SDK directly; prompts are tuned to the current model. | **H** | Put one internal `generate()` interface in front of the SDK (model ID, params, prompt template version as config), starting with the mitigation-proposal path. |
| **Routing** | A model is chosen per feature, but there is no failover and no config-driven switch. | **H** | Move per-feature model selection into config / feature flag, with one pre-tested fallback model per feature. |
| **Eval** | The golden set and groundedness checks cannot run unchanged against another model. | **H** | Make the harness model-agnostic: same fixtures and 100% groundedness gate, model as a parameter, and a baseline score for the current model. |

## Portability Score

**Locked.** Three of four dimensions are High. A swap today means rewriting call sites, re-tuning prompts and re-validating by hand, so 48 hours is not realistic. The cloud hosting keeps Provider at Medium: other models likely sit behind the same account.

## Actions

**This week**
- Inventory every LLM call site (feature, model ID, prompt, params) and confirm which alternative models are already enabled and approved in the cloud account.
- Run the golden set on the current model and record the baseline: groundedness, Driver coverage, Usefulness, Signal density, Strategy fit, Trend fidelity.

**This month**
- Add the abstraction layer: one `generate()` interface with model, params and prompt version in config; migrate mitigation proposals first, then identification and summaries.
- Make the eval harness model-agnostic and run the golden set on one candidate model from a different family. Record the quality gap and cost per output.

**This quarter**
- Config-driven routing with a tested fallback per feature, health-based failover, and model-specific prompt variants kept in version control.
- Run a swap drill: switch one feature to the fallback model, pass the eval gate and ship, with a target of under 48 hours end to end.
- Add a gate to the release process: no prompt or model change ships without a passing golden-set run.

## If the primary vendor doubles pricing tomorrow:

- **Hours 0-24:** Compute cost per generation by feature to see where the increase hurts most. Mitigation proposals and group assessment summaries are probably heaviest, but verify with real usage. Cap or queue low-value generations and cache repeated ones, which needs no code rewrite.
- **Hours 24-48:** Today, a fallback model needs code changes in each feature and a manual quality check, and cannot be promoted without an eval run. Realistic response: run the golden set against one cheaper approved model and swap only the features that pass the groundedness gate.
- **Gap:** Without the abstraction layer and a portable eval, the real response today is "absorb the increase or pass it to customers" for several weeks. Closing that gap is the point of the plan above.

## If the primary vendor ships a competing product:

- **What they can replicate:** Drafting risks, summarizing assessments and proposing mitigations from customer documents. These are commodity LLM tasks (see `diagnostic.md`).
- **What's defensible:** (1) the risk register, assessments and audit trail as the system of record; (2) claim-level groundedness, the hard groundedness gate and the evaluation harness, which let us prove output is grounded in the customer's assessment; (3) once captured, correction and preference data per tenant (see `data-flywheel.md`); (4) Diligent's board and governance distribution and board-ready reporting.
- **Implication:** Defensibility lives in the workflow, the data and the evaluation layer, not the model. A portable eval harness is therefore both a kill-switch fix and a strategic asset: it lets us treat any vendor as a replaceable component.
