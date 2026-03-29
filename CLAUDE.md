# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Rupantar AI** is a documentation and strategic analysis project for an AI-powered agentic ERP platform targeting India's 50 million SMB shops. This is **not a code repository** — it is a strategic thinking workspace containing proposal documents, framing analyses, risk evaluations, and positioning guides prepared for chairman-level review.

The project is in its **pre-build documentation phase**. No application code exists yet. All work is in the `docs/` directory.

## Repository Structure

```
docs/
  Rupantar_AI_Master_Proposal.md          — The original master proposal (775 lines)
  Rupantar_AI_Master_Proposal_Analysis.md — Why the proposal was written and for whom
  Rupantar_AI_Reframed_Objective.md       — Grand "infrastructure-first" positioning
  Rupantar_AI_Reframed_Objective_Risks.md — Risks of infrastructure framing + mitigations
  Rupantar_AI_Hybrid_Framing.md           — Recommended hybrid positioning (platform ambition + product execution)
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

## Key Constraints for Document Work

- **Do not modify existing content** when adding to analysis documents unless explicitly asked. Use new sections, subsections, or new files.
- **Audience**: The chairman of the company — the highest decision maker. Documents should be calibrated for someone who thinks in categories and decades, not sprints and features.
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
