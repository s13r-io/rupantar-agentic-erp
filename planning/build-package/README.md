# Rupantar H1 Prototype — Developer Handoff Package

This folder contains everything needed to build the **Rupantar Horizon 1 Prototype — Kirana Ops** using Claude Code (or any AI coding agent). Hand this folder to the development team. No other documents are required.

---

## What this prototype is

A browser-based demo proving that a kirana owner can run daily operations through a WhatsApp-like interface, and a partner can configure and deploy that system without engineers. See `build_brief.md` for full product context.

**Stack:** Next.js 14 · TypeScript · Tailwind + shadcn/ui · Zustand · Prisma · PostgreSQL (Neon) · Vercel

---

## Prerequisites

Before starting Sprint 0, have these ready:

| Requirement | Where to get it |
|---|---|
| Node.js 20+ | nodejs.org |
| Git | git-scm.com |
| GitHub account | github.com |
| Neon account (free) | neon.tech — create a project, copy the connection string |
| Vercel account (free) | vercel.com — connect your GitHub repo after Sprint 0 |
| Anthropic API key (optional) | console.anthropic.com — only needed to test real AI adapters in Sprint 4 |

---

## How to use the sprint prompts

Each sprint is a separate Claude Code session. Follow this sequence every time:

### Step 1 — Start a new Claude Code session in the app repo
```
cd rupantar-h1-prototype   # your new repo
claude                      # open Claude Code
```

### Step 2 — Paste the build brief
Copy the full contents of `build_brief.md` and paste it as your first message. This gives Claude Code the product context, tech stack decisions, and constraints.

### Step 3 — Paste the sprint prompt
Copy the relevant `sprint_prompts/sprint_N_*.md` file and paste it as your second message. Claude Code will now build exactly what that sprint requires.

### Step 4 — Review and approve
Claude Code will show you the changes before writing files. Review each diff. If something looks wrong, ask Claude Code to explain or revise.

### Step 5 — Verify
Run the acceptance criteria at the bottom of each sprint prompt. All criteria must pass before moving to the next sprint.

### Step 6 — Review (recommended)
Before starting the next sprint, run the **Sprint Reviewer** agent. Open a new Claude Code session, paste `build_brief.md`, then paste `agents/sprint_reviewer.md`. It checks cross-sprint consistency and catches issues before they compound. See `agents/README.md` for all available agents.

---

## Sprint order

| Sprint | File | What gets built | Est. time |
|---|---|---|---|
| 0 | `sprint_0_foundation.md` | Repo setup, Prisma schema, seed data, role selector | ~2h |
| 1 | `sprint_1_shopkeeper.md` | Chat shell, billing/khata/inventory logic, bill/payment cards | ~5h |
| 2 | `sprint_2_partner.md` | Partner wizard (8 steps), sandbox, go-live, health dashboard | ~5h |
| 3 | `sprint_3_observer.md` | Observer canvas, audit trail, memory inspector, demo reset | ~4h |
| 4 | `sprint_4_polish.md` | Remaining cards, AI adapters, scenario hardening, Vercel deploy | ~4h |
| Review | `agents/eval_runner.md` | Evaluate all 3 tiers of demo-readiness | ~30min |

Total estimated build time: **~20 hours** (with Claude Code) + ~1 hour for review agents.

---

## Running the prototype locally

After Sprint 0:
```bash
# Install dependencies
npm install

# Set up database (create .env from .env.example, add your Neon DATABASE_URL)
cp .env.example .env

# Push schema + seed data
npx prisma db push
npx prisma db seed

# Start dev server
npm run dev
# → Open http://localhost:3000
```

---

## Voice input (demo mode)

In fixture mode, **voice input does not require a microphone**. The voice button in the shopkeeper chat opens a dropdown of pre-recorded demo options:

| Demo | audioRef | What it says |
|---|---|---|
| Bill banao (voice) | `voice_demo_001` | "Ram ko 2 kilo chawal, 1 tel aur 3 biscuit ka bill bana do..." |
| Stock check | `voice_demo_002` | "Sunflower oil kitna bacha hai?" |
| Payment | `voice_demo_003` | "Ram ne 500 de diye." |
| Daily summary | `voice_demo_004` | "Aaj ka summary." |
| Ambiguous customer | `voice_demo_005` | "Ram ka balance batao." |
| Ambiguous product | `voice_demo_006` | "Tel order kar do." |
| Approval gate test | `voice_demo_007` | "Hotel Ganesh ke liye 5 kilo basmati rice..." |

The voice adapter returns the fixture transcript for the selected `audioRef`. See `fixture_map.md` for full mappings.

For real voice input (optional, Sprint 4): wire Deepgram STT API or browser Web Speech API.

---

## Deploying to Vercel

1. Push your repo to GitHub
2. Go to vercel.com → New Project → Import your repo
3. Set environment variables: `DATABASE_URL` (Neon connection string)
4. Deploy — Vercel auto-detects Next.js
5. Optional: set `NEXT_PUBLIC_USE_REAL_AI=true` + `ANTHROPIC_API_KEY` to enable real AI adapters

---

## Demo reset

To restore the demo to its baseline state at any time:

```bash
# Via API (from demo operator screen or curl)
curl -X POST https://your-vercel-url/api/v1/demo/reset \
  -H "Content-Type: application/json" \
  -d '{"reset_inventory":true,"reset_balances":true,"reset_chat":true,"reload_seed_data":true}'
```

Or use the "Demo Operator" role in the app UI → "Reset all" button.

---

## Evaluation

Use `evals.md` to assess if the prototype is ready. Three tiers:

1. **Product truth** — can each role (shopkeeper, partner, observer) complete their core job?
2. **Engineering truth** — is the state model real, or just UI theatrics?
3. **Demo truth** — can you run the 5-minute demo 3 times in a row without issues?

The prototype is demo-ready when all three tiers pass.

---

## What is real vs simulated

| Capability | Mode |
|---|---|
| Billing, inventory, khata state | Real — actual DB mutations |
| Partner wizard, shop deployment | Real |
| Audit trail, memory, session replay | Real |
| Voice transcription | Hybrid — fixture default, real STT optional (Deepgram or browser Web Speech API) |
| Intent detection | Hybrid — fixture default, real Claude Haiku optional |
| Invoice photo extraction | Hybrid — fixture default, real Claude Sonnet with vision optional |
| WhatsApp message delivery | Simulated — shown as `simulated_sent` status |
| Supplier ordering | Simulated — `draft_created` status only |
| UPI payment confirmation | Simulated |

---

## Decision-maker contacts

For any product decisions, UX ambiguities, or scope questions during development, escalate to:

| Decision type | Owner |
|---|---|
| Product / UX | [Add name] |
| Technical architecture | [Add name] |
| Design / visual direction | [Add name] |

---

## Reference documents (in this package)

Use these during development when you need to look something up mid-sprint:

| File | When to use |
|---|---|
| `data_model_reference.md` | Check a Prisma field name or relationship during Sprints 2–4 |
| `fixture_map.md` | Implement adapter fixtures in Sprint 1, or scenario responses in Sprint 4 |
| `sprint_dependencies.md` | Before starting any sprint — understand what you depend on and what depends on you |
| `agents/` | After each sprint and after Sprint 4 — see `agents/README.md` |

## Full spec documents

The full spec lives in `planning/horizon1_markdown_docs/` in the parent repo:
- `02_prototype_blueprint.md` — screens, role flows, demo scenarios
- `03_wireframe_spec.md` — exact UI copy and Hinglish text
- `04_component_inventory_and_interaction_spec.md` — component specs, state machines
- `05_developer_handoff_packet.md` — API contracts, DB schema, build sequence
