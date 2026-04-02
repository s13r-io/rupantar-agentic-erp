# CLAUDE.md — planning/build-package/sprint_prompts/

This file provides guidance to Claude Code (claude.ai/code) when working in this directory.

## What lives here

One Claude Code prompt per sprint. Each file is self-contained when combined with `build_brief.md`.

| File | Builds | Est. time |
|---|---|---|
| `sprint_0_foundation.md` | Repo init, Prisma schema (16 models), seed script, Zustand stores, role selector, Vercel setup | ~2h |
| `sprint_1_shopkeeper.md` | 5 business logic services, fixture adapters, chat API routes, 4 action cards, interaction state machine | ~5h |
| `sprint_2_partner.md` | 13 partner APIs, 8-step wizard, sandbox test lab, go-live, health dashboard, exception queue | ~5h |
| `sprint_3_observer.md` | Observer canvas (3-col), scenario launcher, audit drawer, memory inspector, demo reset admin | ~4h |
| `sprint_4_polish.md` | Remaining cards (stock/reorder, summary, photo), real AI adapter overlay, scenario fixture hardening | ~4h |

## Usage

These prompts are used in the **app repo** (`rupantar-h1-prototype`), not here. Do not run Claude Code from this planning repo when using sprint prompts.

## Cross-sprint references

If you need to check the Prisma schema, seed data IDs, or fixture specifications while working on any sprint:
- Schema + seed IDs: `data_model_reference.md`
- Fixture input→output mappings: `fixture_map.md`
- What this sprint depends on / what depends on it: `sprint_dependencies.md`

## Editing sprint prompts

If product decisions change mid-build:
- Update `build_brief.md` first
- Then update the relevant sprint prompt
- Do not contradict `build_brief.md` within a sprint prompt — `build_brief.md` always takes precedence
