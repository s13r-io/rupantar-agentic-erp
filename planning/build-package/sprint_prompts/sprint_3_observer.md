# Sprint 3 — Observer Mode + Audit Trail

**Before using this prompt:** paste the contents of `build_brief.md` first, then paste this file.

**Assumes Sprints 0–2 are complete:** DB seeded, shopkeeper chat working, partner wizard working, business logic services exist.

---

## Goal

Build the observer experience: the side-by-side live demo canvas, scenario launcher, audit trail drawer, memory inspector, before/after ROI view, real vs simulated transparency panel, and the admin demo reset tool. By end of this sprint, the full 5-minute and 15-minute demo walkthroughs can be run.

---

## Observer + audit API routes

- `GET /api/v1/scenarios` — list all demo scenarios with title, subtitle, duration, tags
- `POST /api/v1/scenarios/[scenarioId]/start` — seed session state for scenario, return session_id
- `GET /api/v1/audit/sessions/[sessionId]` — ordered event log for a session
- `GET /api/v1/audit/sessions/[sessionId]/replay` — replay-optimized frames derived from events
- `GET /api/v1/shops/[shopId]/memory` — return all MemoryEntry records grouped by entity_type
- `POST /api/v1/demo/reset` — already built in Sprint 0; extend to accept `reload_seed_data: true`
- `POST /api/v1/demo/load-seed` — load a named seed pack (`kirana_default_v1`)

---

## Fixture: seeded scenarios

Create `/lib/fixtures/scenarios.ts` with 7 scenario definitions. Each scenario has:
- `id`, `title`, `subtitle`, `duration`, `tags[]`, `happyPath: boolean`
- `seedState` — which session events to pre-populate for instant replay
- `steps[]` — ordered list of { label, agent, confidence, observerAnnotation }

The 7 scenarios (from `02_prototype_blueprint.md` section 12):
1. `scenario_morning_rush_billing` — voice bill → stock update → khata update
2. `scenario_low_stock_reorder` — inventory trigger → supplier draft
3. `scenario_payment_received` — payment → balance change
4. `scenario_invoice_photo` — photo → extraction → confirmation → stock update
5. `scenario_daily_summary` — scheduled summary → business value
6. `scenario_ambiguity_customer` — uncertain input → clarification → safe continuation
7. `scenario_partner_deploy` — blank shop → configured → tested → live

---

## Observer UI screens

All observer screens use the desktop shell. The observer role is accessed at `/?role=observer`.

### `/app/observer/page.tsx` — Scenario Launcher (Screen 02)

7 scenario cards, each with title, subtitle, duration badge, tags (Audience / Flow type / Happy/Edge).
Filter chips: "All" / "Investor" / "Partner" / "Happy path" / "Edge case"
Primary CTA per card: "Start scenario" → calls `POST /api/v1/scenarios/:id/start` → redirects to canvas

### `/app/observer/overview/page.tsx` — Executive Overview (Screen 03)

3 columns: Shopkeeper experience / Partner deployment / Internal intelligence.
"What this proves" section with 4 bullet points.
CTA: "Open Live Demo Canvas"
Exact copy from `03_wireframe_spec.md` screen 03.

### `/app/observer/canvas/page.tsx` — Live Demo Canvas (Screen 04)

**This is the primary demo screen.** Three-column layout:

**Left column (240px):**
- Shop snapshot: name, owner, city, language, status chip
- Active bundle: 7 agents listed with status icons
- Today's stats: sales, cash, credit, low-stock count

**Center column (flexible):**
- Embedded mobile chat frame (shopkeeper view, 390px width)
- Scenario controls: "Switch scenario" / "Pause" / "Restart" in header
- Scenario name shown above chat frame

**Right column (320px):**
- "Orchestration feed" — live stream of audit events
- Each row: timestamp · agent · action · confidence badge
- Toggles at bottom: Show raw input / Show parsed intent / Show memory usage / Show state changes
- Connects to `observerStore` which polls `GET /api/v1/audit/sessions/:sessionId`

The center chat frame must be **fully interactive** — observer can trigger flows themselves, or watch the scenario play through.

### Audit Trail Drawer — `components/observer/AuditDrawer.tsx`

Slides in from right over the canvas. Triggered by "Audit trail" button.
Per-step fields: step number, timestamp, raw input, intent detected, agents called, confidence, memory used, record changes, user-visible output, final status.
Buttons: "Replay from start" / "Jump to this step" / "Download demo log" / "Pin to canvas"
Exact fields from `03_wireframe_spec.md` screen 05.

### Memory Inspector — `components/observer/MemoryInspector.tsx`

Tabs: Shop / Customers / Products / Suppliers / Learned patterns.
Reads from `GET /api/v1/shops/:shopId/memory`.
Sample entries from wireframe spec screen 06 ("Ram bhai usually buys on credit", "'Tel' is ambiguous", etc.)

### `/app/observer/roi/page.tsx` — Before vs After / ROI View (Screen 07)

Two columns: Before (paper-based) vs After (AI-assisted).
Estimated value box with 4 metrics.
Small disclaimer note: "Values shown are demo estimates, not production benchmarks."
Exact copy from wireframe spec screen 07.

### `/app/observer/transparency/page.tsx` — Real vs Simulated Panel (Screen 08)

Three sections: Real / Assisted-hybrid / Simulated.
Each item is a row with a label and status chip.
Exact content from wireframe spec screen 08.

### `/app/admin/page.tsx` — Demo Reset + Seed Control (Screen 31)

Reset checkboxes: inventory / customer balances / conversation history / partner setup / reload seed data.
Warning banner: "This will overwrite current demo state."
"Reset selected" and "Reset all" buttons.
Calls `POST /api/v1/demo/reset`.

### `/app/admin/inspector/page.tsx` — Session Inspector (Screen 30)

Sections: Raw input / Parsed intent / Agent timeline / State before / State after / User output / Error if any.
Buttons: "Replay session" / "Fork from step" / "Export JSON"
Reads from `GET /api/v1/audit/sessions/:sessionId/replay`.

---

## Observer scenario player state machine

Implement in `observerStore` from `05_developer_handoff_packet.md` section 9.3:

`scenario_idle → scenario_loading → scenario_ready → playing → paused → completed`

The player drives the orchestration feed in the right column of the canvas.

---

## Real-time orchestration feed

The right column must update in near-real-time as the shopkeeper interacts in the center column. Implement using polling (`setInterval`, 1.5s) on `GET /api/v1/audit/sessions/:sessionId`. Replace with SSE in a later sprint if needed.

---

## Acceptance criteria for Sprint 3

- [ ] Scenario launcher shows 7 scenario cards; clicking one starts the scenario and loads the canvas
- [ ] Observer canvas shows 3-column layout with live shop snapshot, chat frame, and orchestration feed
- [ ] Orchestration feed updates within 2 seconds of a shopkeeper action
- [ ] Audit drawer opens and shows step-by-step event log for the current session
- [ ] Memory inspector shows all 5 tabs with real data from DB
- [ ] Before/after ROI view renders with correct copy and disclaimer
- [ ] Real vs simulated panel correctly labels all capabilities
- [ ] Demo reset restores all seed state; all 7 flows can run again
- [ ] Session inspector shows replay frames derived from audit events

---

## Before starting Sprint 4

**Recommended:** Run the Sprint Reviewer agent. Start a new Claude Code session, paste `build_brief.md`, then paste `agents/sprint_reviewer.md`. Tell it you just completed Sprint 3. It will verify the observer canvas embeds Sprint 1's chat (not a separate implementation) and that demo reset works end-to-end.

---

## What NOT to build in this sprint

- No stock/reorder/daily summary cards (Sprint 4)
- No photo extraction flow (Sprint 4)
- No real AI adapters (Sprint 4)
- No multi-scenario simultaneous replay
