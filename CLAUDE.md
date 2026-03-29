# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Rupantar AI** is a documentation and strategic analysis project for an AI-powered agentic ERP platform targeting India's 50 million SMB shops. This is **not a code repository** — it is a strategic thinking workspace containing proposal documents, framing analyses, risk evaluations, positioning guides, and the completed chairman-level deliverable package.

The project is in its **pre-build documentation phase**. No application code exists yet. All work is in the `docs/` directory. The chairman deliverable package (Executive Brief, Full Proposal, Appendices) lives under **`docs/draft/`** as numbered working copies.

## Repository Structure

```
docs/
  draft/
    01_Rupantar_AI_Executive_Brief.md         — Standalone 8-section brief for first read
    02_Rupantar_AI_Full_Proposal.md           — Decision document: What → Why → How → Risks → Ask
    03_Rupantar_AI_Appendices.md              — Reference material: all 20 verticals, partner programme, economics, competitive playbook, regulatory framework

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
7. **Rewrite Execution** — Full Proposal, Executive Brief, and Appendices drafted as decision-package documents. Progress tracked in `Rewrite_Plan.md`.

## Chairman Deliverable Package

The three deliverable files form a complete package for chairman review (working copies under `docs/draft/`):

- **Executive Brief** (`docs/draft/01_Rupantar_AI_Executive_Brief.md`) — The first thing the chairman reads. 8 sections, standalone-readable, conclusion-first. Works as a complete document on its own.
- **Full Proposal** (`docs/draft/02_Rupantar_AI_Full_Proposal.md`) — The complete decision document. Structured as: Part 1 (embedded brief) → Part 2 (The Proposal) → Part 3 (The Evidence) → Part 4 (The Execution) → Part 5 (The Risks) → Part 6 (The Ask).
- **Appendices** (`docs/draft/03_Rupantar_AI_Appendices.md`) — Reference material: all 20 vertical deep dives, partner programme detail, unit economics scenarios, competitive response playbook, regulatory/compliance framework.

## What Rupantar Is (Critical Context)

When working on any document in this project, understand that Rupantar AI is **two things you build** and **one way you distribute them:**

- **The Product** — AI agents running on WhatsApp/voice. Each shop gets a vertical-specific bundle of 3–5 agents (billing, inventory, credit, etc.). Revenue: SaaS subscriptions.
- **The Platform** — Agent Builder (Library + Visual Flow Builder + Config Studio + Pro Code SDK). Lets trained partners deploy agent bundles without code. Revenue: platform fees + marketplace royalties.
- **The Distribution** — Partner network (AI Shop Doctors). India's existing field force trained and certified to deploy the product using the platform. NOT a software product — a go-to-market channel.

Do NOT describe these as "three layers" or "three-tier architecture." That framing incorrectly implies the partner network is a technical component. Use "product + platform + distribution."

## Key Constraints for Document Work

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
