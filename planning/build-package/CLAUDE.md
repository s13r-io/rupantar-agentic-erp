# CLAUDE.md — planning/build-package/

This file provides guidance to Claude Code (claude.ai/code) when working in this directory.

## What this folder is

The complete developer handoff package for the **Rupantar H1 Prototype — Kirana Ops**. This folder is given to the development team as a self-contained unit — they do not need any other planning documents.

## File guide

| File | Role |
|---|---|
| `README.md` | How to use, prerequisites, local setup, Vercel deploy, demo reset, eval tiers |
| `build_brief.md` | **Paste first in every Claude Code session** — locked stack, real vs simulated, API conventions, seed data, out-of-scope list |
| `ui_style_brief.md` | Color palette, typography, density, chat bubble spec, status chip colors |
| `acceptance_criteria.md` | Checkbox-level "done" criteria for all 7 demo flows, tied to real DB state |
| `evals.md` | 3-tier quality evaluation: product truth · engineering truth · demo truth |
| `data_model_reference.md` | Standalone Prisma schema + relationships + seed IDs — quick-reference during Sprints 2–4 |
| `fixture_map.md` | Exact input→output mappings for all AI adapter fixtures — implement in Sprint 1, harden in Sprint 4 |
| `sprint_dependencies.md` | What each sprint produces that later sprints consume — check before starting each sprint |
| `agents/` | Claude Code prompts for post-sprint review, eval execution, and UI audit — see `agents/README.md` |
| `sprint_prompts/` | One Claude Code prompt per sprint — see its own CLAUDE.md |

## How the prompts are used

Each sprint = one Claude Code session in the **new app repo** (`rupantar-h1-prototype`):
1. Paste `build_brief.md` content
2. Paste the relevant `sprint_prompts/sprint_N_*.md`
3. Review + approve Claude Code's changes
4. Verify against the sprint's acceptance criteria

## Do not edit these files without also updating

If you update `build_brief.md` (e.g. changing a tech stack decision), propagate the change to any sprint prompt that references the affected area.
