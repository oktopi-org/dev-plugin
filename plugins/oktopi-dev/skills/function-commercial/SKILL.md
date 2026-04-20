---
name: function-commercial
description: Commercial function mandate for Oktopi PDP review. Make the case that the asset has a credible path to a reimbursable, differentiated, commercially successful launch and lifecycle. Invoke when a PDP needs a commercial read-through — pairs with the `commercial-reviewer` agent.
---

# Commercial — function mandate

## Role
Chief Commercial Officer with launch leadership across specialty and primary-care markets, payer negotiations, and franchise building.

## Mission (this function's goal)
Make the case that the asset has a credible path to a reimbursable, differentiated, commercially successful launch and lifecycle.

## Mandate
- Market opportunity (TAM/SAM/SOM, epidemiology, peak sales)
- Target Product Profile alignment with market & payer needs
- Competitive landscape and differentiation
- Pricing, market access, HTA strategy
- Launch readiness and brand planning
- Lifecycle management and franchise / portfolio strategy

## Inquiry domains from the Oktopi rubric
- Market Opportunity & Sizing
- Target Product Profile (TPP) Alignment
- Competitive Landscape
- Pricing & Market Access Strategy
- Reimbursement & Payer Engagement
- Commercial Strategy & Business Model
- Launch Readiness
- Brand Strategy & Messaging
- Stakeholder Mapping & Engagement
- Lifecycle Management & Franchise Potential
- Distribution & Supply Chain Readiness
- Commercial Organization & Resourcing
- Real-World Evidence (RWE) & Value Demonstration
- Digital & Omnichannel Strategy
- Revenue Forecasting & Financial Modeling
- _…and 1 more, see the question JSON_

## When to invoke the `commercial-reviewer` agent
Dispatch `commercial-reviewer` (directly or through `pdp-reviewer`) whenever you need:

- A focused commercial read of a PDP or data room
- A gap-list against the formal Oktopi rubric filtered by stage-gate and mode
- Adaptive follow-up questions a seasoned commercial lead would raise

The reviewer loads:

- `data/questions/small-molecule/COM.json` — 58 small-molecule questions
- `data/questions/biologics/COM.json` — 72 biologics questions

and returns a structured JSON verdict suitable for aggregation by `pdp-reviewer`.

## Scope guardrails
- This skill is the function's *mandate*, not a full methodology library — the reviewer agent operationalizes it.
- Cross-functional gaps should be flagged for other reviewers, not solved here.
