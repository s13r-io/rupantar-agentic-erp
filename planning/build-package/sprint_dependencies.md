# Sprint Dependency Map

Scan this before starting each sprint (~2 minutes). Know what you depend on and what depends on you.

---

## What each sprint produces

### Sprint 0 produces:

| Output | Used by |
|---|---|
| Prisma schema (16 models) | **All sprints** — every service reads/writes these |
| Seed script + data IDs (`shop_shree_ganesh_kirana`, `cust_*`, `prod_*`, `sup_*`) | Sprint 1 (fixtures reference IDs), Sprint 3 (scenarios), Sprint 4 (fixture hardening) |
| Zustand stores: `sessionStore` | Sprint 1 (chat state machine) |
| Zustand stores: `partnerWizardStore` | Sprint 2 (wizard flow) |
| Zustand stores: `observerStore`, `auditStore` | Sprint 3 (observer canvas, orchestration feed) |
| Zustand stores: `uiStore` | Sprint 1+ (drawers, modals, toasts) |
| Demo reset API (`POST /api/v1/demo/reset`) | Sprint 3 (extends it), Sprint 4 (uses it) |
| Bootstrap API (`GET /api/v1/bootstrap`) | Sprint 3 (scenario launcher loads initial state) |
| Role selector (`/app/page.tsx`) | Sprint 1+ (entry point to all role views) |

### Sprint 1 produces:

| Output | Used by |
|---|---|
| `billing.ts` — `createDraftBill()`, `confirmBill()`, `cancelBill()` | Sprint 2 (sandbox tests), Sprint 3 (scenarios), Sprint 4 (remaining cards) |
| `inventory.ts` — `getStock()`, `getLowStockItems()`, `decrementStock()`, `incrementStock()` | Sprint 2 (health dashboard), Sprint 3 (scenarios), Sprint 4 (stock/reorder card, daily summary) |
| `khata.ts` — `getBalance()`, `applyBillToBalance()`, `recordPayment()` | Sprint 2 (health dashboard), Sprint 3 (scenarios), Sprint 4 (daily summary) |
| `procurement.ts` — `checkAndDraftReorder()`, `approveReorderDraft()`, `cancelReorderDraft()` | Sprint 2 (exception queue), Sprint 3 (scenarios), Sprint 4 (stock/reorder card) |
| `audit.ts` — `logEvent()`, `getSessionEvents()` | **All subsequent sprints** — every action must audit |
| Adapters: `intent.ts`, `voice.ts`, `invoice.ts` | Sprint 2 (sandbox tests call intent), Sprint 4 (enhanced with real API overlay) |
| Chat API routes (5 endpoints) | Sprint 3 (observer canvas embeds interactive chat) |
| Chat UI: `ChatHeader`, `MessageBubble`, `ChatComposer`, `QuickReplyChips` | Sprint 3 (embedded in observer canvas center column) |
| Action cards: `VoiceReviewCard`, `BillPreviewCard`, `PaymentKhataCard`, `ClarificationCard` | Sprint 3 (visible in observer canvas), Sprint 4 (extended with new cards) |
| Interaction state machine in `sessionStore` | Sprint 3 (observer watches state transitions) |

### Sprint 2 produces:

| Output | Used by |
|---|---|
| Partner API routes (13 endpoints) | Sprint 3 (scenario 7 = partner deploy) |
| Shop creation flow (8-step wizard) | Sprint 3 (`scenario_partner_deploy` needs this working) |
| Health dashboard | Sprint 4 (polish pass may adjust) |
| Exception queue | Sprint 4 (polish pass) |

### Sprint 3 produces:

| Output | Used by |
|---|---|
| Scenario definitions (`/lib/fixtures/scenarios.ts`) | Sprint 4 (`scenario-responses.ts` maps to these) |
| Observer canvas (3-column layout) | Sprint 4 (polish pass) |
| Audit trail drawer | Sprint 4 (polish pass) |
| Memory inspector | Sprint 4 (polish pass) |
| Extended demo reset (with `reload_seed_data`) | Sprint 4 (eval runs need reliable reset) |

### Sprint 4 produces:

Sprint 4 is the terminal sprint. Its outputs are the demo-ready prototype.

---

## Do-not-break contracts

These interfaces are referenced across 2+ sprints. **Do not rename, change signatures, or restructure without checking all consumers.**

| Interface | Defined in | Consumers | Signature |
|---|---|---|---|
| `billing.createDraftBill()` | Sprint 1 | Sprint 2 sandbox, Sprint 3 scenarios | `(shopId, customerId, items[], paymentMode) → DraftBill` |
| `billing.confirmBill()` | Sprint 1 | Sprint 2 sandbox, Sprint 3 scenarios, Sprint 4 cards | `(billId) → DraftBill` |
| `inventory.getStock()` | Sprint 1 | Sprint 2 health, Sprint 4 stock card | `(shopId, productId) → { currentStock, belowThreshold }` |
| `inventory.getLowStockItems()` | Sprint 1 | Sprint 2 health, Sprint 4 summary card | `(shopId) → Product[]` |
| `inventory.decrementStock()` | Sprint 1 | Sprint 3 scenarios, Sprint 4 photo card | `(shopId, productId, quantity, reason) → StockMovement` |
| `inventory.incrementStock()` | Sprint 1 | Sprint 4 photo extraction card | `(shopId, productId, quantity, reason) → StockMovement` |
| `khata.getBalance()` | Sprint 1 | Sprint 2 health, Sprint 3 scenarios | `(shopId, customerId) → { outstandingBalance }` |
| `khata.recordPayment()` | Sprint 1 | Sprint 3 scenarios, Sprint 4 cards | `(shopId, customerId, amount) → KhataTransaction` |
| `audit.logEvent()` | Sprint 1 | **All sprints** | `(shopId, sessionId, step, label, eventType, opts) → AuditEvent` |
| `audit.getSessionEvents()` | Sprint 1 | Sprint 3 observer feed + audit drawer | `(sessionId) → AuditEvent[]` |
| Intent adapter fixture format | Sprint 1 | Sprint 2 sandbox, Sprint 4 hardening | `{ intent, entities, confidence, clarificationOptions, agentsSuggested }` |
| Seed data IDs | Sprint 0 | **All sprints** | `shop_shree_ganesh_kirana`, `cust_*`, `prod_*`, `sup_*` |
| `sessionStore` state shape | Sprint 0 | Sprint 1 (chat), Sprint 3 (observer) | `{ currentRole, currentShopId, currentSessionId, chatMessages[], pendingCards[] }` |
| Demo reset API | Sprint 0 | Sprint 3 (extends), Sprint 4 (uses) | `POST /api/v1/demo/reset` with body `{ reset_inventory, reset_balances, reset_chat, reload_seed_data }` |
| `procurement.approveReorderDraft()` | Sprint 1 | Sprint 2 (exception queue clears on approval) | Approving a reorder must resolve the corresponding low-confidence AuditEvent so Sprint 2's exception queue (`GET /api/v1/shops/:shopId/exceptions`) reflects the cleared state |

---

## Sprint-start checklist

Before starting each sprint, verify these prerequisites still hold:

**Before Sprint 1:**
- [ ] `npx prisma db push` and `npx prisma db seed` run cleanly
- [ ] `GET /api/v1/bootstrap` returns shop ID and roles
- [ ] Role selector navigates to `/shopkeeper`

**Before Sprint 2:**
- [ ] All Sprint 1 acceptance criteria pass (see `sprint_1_shopkeeper.md`)
- [ ] `billing.createDraftBill()` + `confirmBill()` work end-to-end
- [ ] `audit.logEvent()` creates AuditEvent records in DB

**Before Sprint 3:**
- [ ] All Sprint 2 acceptance criteria pass (see `sprint_2_partner.md`)
- [ ] Partner wizard can create + deploy a shop (status → `live`)
- [ ] Sprint 1 chat still works after Sprint 2 changes

**Before Sprint 4:**
- [ ] All Sprint 3 acceptance criteria pass (see `sprint_3_observer.md`)
- [ ] Observer canvas embeds interactive shopkeeper chat
- [ ] `GET /api/v1/audit/sessions/:sessionId` returns ordered events
- [ ] Demo reset restores all seed state
