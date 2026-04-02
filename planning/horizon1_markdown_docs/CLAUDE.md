# CLAUDE.md — planning/horizon1_markdown_docs/

This file provides guidance to Claude Code (claude.ai/code) when working in this directory.

## Document set — read in order

| File | Contains |
|---|---|
| `01_horizon1_prototype_scope.md` | Goals, target audiences, v1 agent bundle, success criteria |
| `02_prototype_blueprint.md` | 4 surfaces, 34 screens, role flows, real vs simulated split, demo scripts |
| `03_wireframe_spec.md` | Screen-by-screen wireframe with exact UI copy, data model, Figma org |
| `04_component_inventory_and_interaction_spec.md` | Component library, state machines, audit schema, seed data JSON |
| `05_developer_handoff_packet.md` | Tech stack, API contracts, state machines, DB schema, build sequence |

## Prototype scope in one line

**Kirana only. One partner flow. One shopkeeper flow. One observer mode.** 7 agents. ~31 screens.

## Real vs simulated boundary (critical)

**Real:** billing calc, inventory state, khata ledger, reorder draft, daily summary, partner wizard, audit log
**Hybrid:** voice transcription, intent detection, invoice OCR, confidence scoring
**Simulated:** WhatsApp delivery, supplier messaging, UPI confirmation, offline sync

## Build sequence (from `05_developer_handoff_packet.md`)

Phase 1: shell + seed → Phase 2: business logic (billing/inventory/khata) → Phase 3: partner wizard → Phase 4: shopkeeper chat pipeline → Phase 5: observer/admin → Phase 6: polish + fixtures

## Open engineering decisions (must resolve before dev)

Next.js vs React+Vite · Zustand vs XState · SQLite vs PostgreSQL · real STT now or fixture-first · local vs Vercel deploy
