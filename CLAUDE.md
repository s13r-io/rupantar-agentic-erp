# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Rupantar AI** is a documentation and strategic analysis project for an AI-powered agentic ERP platform targeting India's 50 million SMB shops. This is **not a code repository** — it is a strategic thinking workspace containing proposal documents, framing analyses, risk evaluations, positioning guides, and execution planning for chairman-facing deliverables.

The project is in its **pre-build documentation phase**. No application code exists yet. All work is in the `docs/` directory.

**`docs/draft/`** — Contains the current deliverable documents (Executive Brief, Full Proposal, Appendices). These are the active working files. When the user asks to work on a document, read from this folder.

## Repository Structure

```
docs/
  # Source Analysis Documents (preserved unmodified)
  Rupantar_AI_Master_Proposal.md              — The original master proposal (775 lines)
  Rupantar_AI_Master_Proposal.pdf             — Original proposal in PDF format
  Rupantar_AI_Master_Proposal.txt             — Original proposal in plain text
  Rupantar_AI_Master_Proposal_Analysis.md     — Why the proposal was written and for whom
  Rupantar_AI_Reframed_Objective.md           — Grand "infrastructure-first" positioning
  Rupantar_AI_Reframed_Objective_Risks.md     — Risks of infrastructure framing + mitigations
  Rupantar_AI_Hybrid_Framing.md               — Recommended hybrid positioning (platform ambition + product execution)
  Rupantar_AI_Deliverable_Structure.md        — The deliverable package format (brief + full proposal + appendices)
  Rupantar_AI_Original_Document_Structure_Analysis.md — Section-by-section breakdown + clarity assessment

  # Execution Tracking
  Rewrite_Plan.md                             — Phase-by-phase execution checklist

  # Deliverable Documents (active)
  01_Rupantar_AI_Executive_Brief.md          — Standalone 9-section executive brief
  02_Rupantar_AI_Full_Proposal.md            — Full proposal (6 parts)
  03_Rupantar_AI_Appendices.md               — Reference material (verticals, partner programme, economics, competitive playbook, regulatory)
  Content_Audit_Source_vs_Drafts.md         — Audit mapping source proposal to draft deliverables
```

## Strategic Thinking Progression

The documents follow a deliberate analytical progression. Future instances should understand this sequence when working with these files:

1. **Analysis** — What the proposal is, why it exists, what the chairman needs to hear
2. **Reframe (Ambitious)** — How to make the objective grander: "digital backbone of India's retail economy"
3. **Risk Evaluation** — Why the ambitious framing could backfire (credibility gap, regulatory exposure, capital anxiety, scope creep, narrative incoherence, data fragility, competitive provocation) with detailed mitigations for each
4. **Hybrid Framing (Recommended)** — Synthesizes both into a risk-mitigated positioning using:
   - "Platform" not "infrastructure" (regulatory safety)
   - "Foundation" not "wedge" (SaaS is intrinsically valuable)
   - Two-Horizon Framework (product now, platform later)
   - Confidence Roadmap (know / believe / test)
   - Platform Readiness Scorecard (measurable criteria before claiming platform status)
   - Value Compounding Model (staircase of value at each scale milestone)
5. **Deliverable Structure** — Defines the two-file format (executive brief + full proposal), three-tier vertical depth strategy, decision-document flow (What/Why/How/Risks/Ask), and writing rules for the chairman
6. **Original Document Analysis** — Complete section-by-section breakdown of the master proposal with line references, clarity assessment, and prioritised rewrite recommendations
7. **Rewrite Execution** — Deliverable shape and checklist in `Rewrite_Plan.md` and `Rupantar_AI_Deliverable_Structure.md`.
8. **Platform Restructuring (March 2026)** — Full Proposal Part 2 restructured: opportunity before solution (§2.1–§2.4 reordered), "two things we build" replaced with "Agentic Operations Platform" (one composable system), "Platform Readiness Scorecard" renamed to "Ecosystem Readiness Scorecard." Applied across Executive Brief, Full Proposal, Content Audit, and CLAUDE.md.

## What Rupantar Is (Critical Context)

When working on any document in this project, understand that Rupantar company is building **Rupantar AI** — an **Agentic Operations Platform**. This is one system, not two:

- **The Agentic Operations Platform** — A composable system of 160+ pre-built AI agents covering every aspect of shop operations (billing, inventory, credit, compliance, etc.). Partners use the platform's four-layer architecture (Agent Library → Visual Flow Builder → Config Studio → Pro Code SDK) to select and combine agents into bespoke solutions for each shop. Each shop subscribes to its composed solution. Revenue: solution subscriptions + platform fees + marketplace royalties.
- **The Distribution** — Partner network (AI Shop Doctors). India's existing field force trained and certified to compose and deploy solutions using the platform. NOT a software product — a go-to-market channel.

Do NOT describe this as "product + platform" or "two things we build." The agents are components within the platform, not a separate product. Use "the platform" or "Agentic Operations Platform."

## Key Constraints for Document Work

- **`docs/draft/`** — Treat as **ignored** unless the user explicitly opens it or asks for changes there. Do not proactively use or describe what is inside.
- **Do not modify existing content** when adding to analysis documents unless explicitly asked. Use new sections, subsections, or new files.
- **Audience**: The chairman of the company — the highest decision maker. He reads thoroughly and alone before calling a meeting. He does not tolerate fluff and does not like being strung along. Key insights go first, not last.
- **Language discipline**: When writing in the hybrid framing voice, avoid "infrastructure," "DPI," "backbone," "monopoly" in thesis/core content. Use "platform," "foundation," "digital layer," "ecosystem." These trigger words may appear in comparison tables or when explicitly contrasting framings.
- **Data integrity**: All market data in the proposal is sourced from public reports (SaaSBoomi, KenResearch, Mordor Intelligence, NPCI, MSME Ministry). Do not fabricate statistics. When uncertain, flag as estimate.

## Context: The Product Being Proposed

Rupantar AI is an AI agentic ERP delivered through WhatsApp and voice for India's unorganised retail economy (₹95 lakh crore across 50M shops). Key design principles:
- Zero UI — shopkeepers interact via voice notes, photos, and one-word WhatsApp replies
- Vernacular NLP — Hindi, Hinglish, and 12 regional languages with local commercial vocabulary
- Partner-distributed — India's existing field force (FMCG reps, pharma MRs, Tally resellers) becomes certified "AI Shop Doctors"
- 20 verticals: kirana, restaurant, pharmacy, salon, garage, repair, fashion, hardware, education, and more

## Git Workflow

All work happens on `main`. Commit messages should be descriptive and follow the pattern established in the repo:
- Reference the document being modified
- Summarise the change in one line
- Include `Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>`
