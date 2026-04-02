# Sprint 2 — Partner Wizard + Deployment Console

**Before using this prompt:** paste the contents of `build_brief.md` first, then paste this file.

**Assumes Sprint 0 + Sprint 1 are complete:** DB seeded, shopkeeper chat working, business logic services exist.

---

## Goal

Build the full partner experience: portfolio view, 8-step new shop wizard, sandbox test lab, go-live activation, shop health dashboard, and exception queue. By end of this sprint, a partner can configure a new kirana shop from scratch and make it live.

---

## Partner API routes

Create these Route Handlers under `/app/api/v1/`:

- `GET /api/v1/partner/shops` — list all shops with deployment_status, health summary
- `POST /api/v1/shops` — create shop (step 1 of wizard)
- `PUT /api/v1/shops/[shopId]/bundle` — assign kirana bundle
- `POST /api/v1/shops/[shopId]/products` — bulk add products
- `POST /api/v1/shops/[shopId]/customers` — bulk add customers
- `POST /api/v1/shops/[shopId]/suppliers` — bulk add suppliers
- `PUT /api/v1/shops/[shopId]/rules` — save trust/language/rule config
- `POST /api/v1/shops/[shopId]/sandbox-tests` — run a sandbox test (calls intent adapter with fixture)
- `POST /api/v1/shops/[shopId]/deploy` — sets `deployment_status = 'live'`
- `GET /api/v1/shops/[shopId]/health` — returns bills_today, credit_sales, dues_received, low_stock_alerts, pending_clarifications, pending_approvals, health_status
- `GET /api/v1/shops/[shopId]/context` — returns full shop config + memory entries
- `PUT /api/v1/shops/[shopId]/context` — edit products/customers/suppliers/preferences
- `GET /api/v1/shops/[shopId]/exceptions` — returns unresolved `AuditEvent` records with status `clarification_needed` or low-confidence items

---

## Partner UI screens

All partner screens use the desktop shell (`1440px`, sidebar nav + main panel).

### `/app/partner/page.tsx` — Portfolio Home (Screen 09)

- Header: "Good morning, Neha" + "You manage 12 shops"
- KPI tiles: Live shops / Sandbox shops / Shops with pending exceptions / Shops needing attention
- Shop list table: name, status chip, health badge, last activity, quick actions
- CTA buttons: "Add new shop" / "Open sandbox lab" / "View exception queue"

### `/app/partner/new-shop/page.tsx` — 8-step wizard (Screens 10–17)

Use `partnerWizardStore` for state. Use `cmp.nav.stepper` across top. Each step saves draft automatically.

**Step 1 — Basic Details (Screen 10)**
Fields: shop name, owner name, WhatsApp number, city/area, GST status (radio), business hours, preferred language (dropdown: Hinglish/Hindi/English/Gujarati), summary time. Helper: "This should take 8–10 minutes in demo mode."

**Step 2 — Bundle Selection (Screen 11)**
Show "Kirana Core Bundle" card with 7 agents listed. Checkmarks. Estimated setup time: "10 minutes." Bundle is pre-selected and locked for v1.

**Step 3 — Catalog Import (Screen 12)**
Tabs: "Upload CSV" / "Manual entry" / "Use sample catalog". For demo, "Use sample catalog" pre-fills 15 products from seed data. Manual entry shows inline-editable table with: display_name, alias (token input), category (dropdown), unit_type, selling_price, opening_stock, reorder_threshold, preferred_supplier.

**Step 4 — Customers + Khata (Screen 13)**
Inline-editable table: customer name, alias, phone, credit enabled (toggle), current outstanding (currency input), reminder timing.

**Step 5 — Suppliers + Reorder Rules (Screen 14)**
Supplier form: name, phone, categories_supplied (multi-select), lead time. Rule section showing the 3 default rules.

**Step 6 — Language / Tone / Trust Rules (Screen 15)**
3 cards: Language & tone config / Approval rules / Clarification rules. Show exact copy from wireframe spec screen 15.

**Step 7 — Sandbox Test Lab (Screen 16)**
6 test buttons: voice bill / stock query / payment update / invoice photo / daily summary / ambiguous request. Each calls `POST /api/v1/shops/:shopId/sandbox-tests`. Result panel on right: input, output, agents used, confidence, result badge. Center note: "This test uses sandbox state."

**Step 8 — Go Live Summary (Screen 17)**
Checklist showing completion status for each wizard step. "Go live" primary CTA → calls `POST /api/v1/shops/:shopId/deploy`. "Back to sandbox" secondary CTA. Cannot go live if sandbox tests = 0.

### `/app/partner/shops/[shopId]/health/page.tsx` — Shop Health Dashboard (Screen 18)

KPIs: bills today, credit sales today, dues collected today, low-stock alerts, pending clarifications, pending approvals. Recent activity feed (last 10 AuditEvents). Health label chip: Healthy / Needs follow-up / Risk of disengagement.

### `/app/partner/shops/[shopId]/context/page.tsx` — Edit Context (Screen 19)

Tabs: Products / Customers / Suppliers / Shop preferences / Learned memory. Inline-editable tables for each. "Save changes" → "Retest in sandbox" → "Push live" action flow.

### `/app/partner/exceptions/page.tsx` — Exception Queue (Screen 20)

Table columns: Type, Shop, Severity chip, Created at, Suggested action, Resolve button. Filter by severity (Low/Medium/High). Types match wireframe spec screen 20 exactly.

### `/app/partner/rules/page.tsx` — Lite Rule Builder (Screen 21)

Display 4 static rules as read-only cards with edit capability. Helper text: "v1 supports simple operational rules. Full visual flow building is out of scope." No drag-and-drop.

---

## Partner wizard state machine

Implement from `05_developer_handoff_packet.md` section 9.2 in `partnerWizardStore`:

`basic_details → bundle_selection → catalog_setup → customers_setup → suppliers_setup → rules_setup → sandbox_testing → go_live_summary → deployed_live`

- Allow backward navigation to completed steps
- Block forward jumps past incomplete required steps
- Warn (don't block) if catalog has < 10 products

---

## Acceptance criteria for Sprint 2

- [ ] Partner can navigate to all 8 wizard steps in sequence
- [ ] "Use sample catalog" auto-fills 15 seeded products
- [ ] Sandbox test lab runs a voice bill test and shows result
- [ ] Cannot click "Go live" without at least 1 sandbox test
- [ ] Go live changes `deployment_status` to `live` in DB
- [ ] Shop appears in portfolio with "Live" chip after deployment
- [ ] Health dashboard KPIs reflect real data from DB (bills, khata, inventory)
- [ ] Exception queue shows unresolved low-confidence audit events
- [ ] Edit context changes persist to DB and are reflected in next shopkeeper interaction

---

## Before starting Sprint 3

**Recommended:** Run the Sprint Reviewer agent. Start a new Claude Code session, paste `build_brief.md`, then paste `agents/sprint_reviewer.md`. Tell it you just completed Sprint 2. It will verify the wizard + deployment flow work correctly and that Sprint 1 shopkeeper chat hasn't regressed.

---

## What NOT to build in this sprint

- No observer canvas yet (Sprint 3)
- No AI adapters beyond fixtures (Sprint 4)
- No multi-vertical wizard (Kirana only)
- No visual flow builder (explicitly out of scope)
