---
name: oktopi-research-team
description: "Oktopi Research Team — 12-agent multi-agent team for pharma drug development reviews (CMC, pharm-tox, translational, clin pharm, clin dev, safety, clin ops, biostats, regulatory, epi/RWE, commercial, project management). Use PROACTIVELY when the user asks about drug development, PDP review, stage-gate readiness, due diligence of a pharma asset, or any of: drug substance or drug product development; GMP manufacturing, tech transfer, or process validation; analytical methods, specifications, or stability; CMC regulatory package, Module 3, or comparability; supply chain, API sourcing, or release testing; biologics CMC: cell line, upstream/downstream, aggregation; IND-enabling toxicology, GLP tox, or species selection; safety pharmacology, genotoxicity, or carcinogenicity; DMPK, ADME, or preclinical PK; starting dose, MABEL, HED, or first-in-human justification; juvenile, reproductive, or developmental tox; biologics-specific nonclinical concerns (immunogenicity, CRS, cytokine release); biomarker strategy, target engagement, or patient selection biomarkers; translational PK/PD modeling, human dose prediction; proof-of-mechanism or proof-of-concept design; companion diagnostic (CDx) strategy; reverse translation from clinical signals; bridging preclinical data to Phase 1/2 decisions; clinical PK, exposure-response, or dose-finding; DDI strategy or in vitro / clinical DDI studies; special populations (renal, hepatic, pediatric, pregnancy); pop-PK, PBPK, or QSP modeling; Project Optimus dose optimization; label dose justification."
---

# Oktopi Research Team — Pharma Development Router

## When this skill triggers

Claude should activate this skill whenever the user's question touches **pharmaceutical drug development**: discovery, preclinical, clinical trials, CMC/manufacturing, regulatory strategy, pharmacovigilance, clinical pharmacology, biostatistics, commercial / market access, epidemiology / RWE, or programme management.

## What to do

1. **Identify the function(s).** Match the user's question to one of the 12 functional areas below using the trigger phrases.
2. **For a focused question** (one function): invoke that function's reviewer agent directly via the Task tool.
3. **For a full PDP review or cross-functional question**: invoke the `pdp-reviewer` orchestrator agent, which will fan out to the relevant function reviewers in parallel and consolidate the report.
4. **If the question is ambiguous** or spans multiple functions: ask one clarifying question, then route.

## The team

| Code | Agent | Trigger phrases (partial) |
| ---- | ----- | ------------------------- |
| `CMC` | `cmc-reviewer` | drug substance or drug product development; GMP manufacturing, tech transfer, or process validation; analytical methods, specifications, or stability |
| `PT` | `pharmtox-reviewer` | IND-enabling toxicology, GLP tox, or species selection; safety pharmacology, genotoxicity, or carcinogenicity; DMPK, ADME, or preclinical PK |
| `TM` | `translational-medicine-reviewer` | biomarker strategy, target engagement, or patient selection biomarkers; translational PK/PD modeling, human dose prediction; proof-of-mechanism or proof-of-concept design |
| `CP` | `clinical-pharmacology-reviewer` | clinical PK, exposure-response, or dose-finding; DDI strategy or in vitro / clinical DDI studies; special populations (renal, hepatic, pediatric, pregnancy) |
| `CDM` | `clinical-development-medical-reviewer` | Target Product Profile (TPP) or clinical development plan (CDP); Phase 1, 2, or 3 protocol design; endpoint selection, comparator arm, or patient population |
| `SAF` | `clinical-safety-reviewer` | SAE, SUSAR, or expedited safety reporting; DSUR, PBRER, or integrated safety summary; Risk Management Plan (RMP) or REMS |
| `COP` | `clinical-operations-reviewer` | site activation, feasibility, or country selection; enrollment forecasting or risk-based monitoring; CRO selection, oversight, or governance |
| `STAT` | `biostatistics-reviewer` | sample size, power, or estimand (ICH E9 R1); SAP, multiplicity, or alpha-spending; adaptive design, group-sequential, or external control |
| `REG` | `regulatory-affairs-reviewer` | IND, NDA, BLA, CTA, or MAA submission; FDA, EMA, PMDA, or ICH agency interactions; pre-IND, EoP2, Type B/C meeting, or briefing document |
| `ERW` | `epi-rwe-reviewer` | epidemiology, prevalence, incidence, or burden of disease; real-world evidence (RWE), external control, or synthetic control arm; natural-history study or registry |
| `COM` | `commercial-reviewer` | market sizing (TAM/SAM/SOM), peak sales, or forecast; pricing, market access, or HTA (NICE, IQWiG, PBAC, G-BA) strategy; payer value dossier or reimbursement strategy |
| `PM` | `project-management-reviewer` | integrated development plan (IDP), critical path, or Gantt; cross-functional dependency, interlock, or handoff; risk register, RAID log, or escalation |

Plus orchestrator `pdp-reviewer` for full PDP gap-analysis.

## Decision matrix

| User intent | Invoke |
| --- | --- |
| "Review my PDP at SG5 OE" or "gate readiness" or "due diligence pack" | `pdp-reviewer` (orchestrator) |
| Single function question ("is my SAP airtight?") | matching function reviewer |
| Stage-gate goal question ("what does SG3 require?") | the corresponding `stage-gate-sg<N>` skill |
| Function mandate question ("what does Translational Medicine own?") | the corresponding `function-<slug>` skill |
| Novel modality (bispecific, ADC, cell therapy) | flag modality to every agent so they apply modality-specific adaptive questions |

## Reference data for the router

- `data/functions.json` — all 12 functions with role, mission, mandate, triggers
- `data/stage-gates.json` — SG1..SG9 goals
- `data/stage-gate-index.json` — Critical question load per (SG, mode, function)

## Guardrails
- **Route, don't answer.** This skill decides which specialist responds — it is not itself a subject-matter expert.
- **Prefer the orchestrator for broad questions.** The `pdp-reviewer` fans out in parallel, which is faster and more complete than serial calls.
- **Cite specialists by agent name** when handing off so the user knows who will respond.
