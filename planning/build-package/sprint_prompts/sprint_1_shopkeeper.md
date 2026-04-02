# Sprint 1 — Shopkeeper Chat + Business Logic

**Before using this prompt:** paste the contents of `build_brief.md` first, then paste this file.

**Assumes Sprint 0 is complete:** Next.js app running, Prisma schema migrated, seed data loaded, role selector works.

---

## Goal

Build the shopkeeper WhatsApp-like chat interface and all the stateful business logic services. By end of this sprint, a user entering as Shopkeeper can complete the voice bill flow, payment flow, and stock query end-to-end with real DB state mutations.

---

## Business logic services

Create these in `/lib/services/`. Each must read/write the Prisma DB — no mocked returns.

### `billing.ts`
- `createDraftBill(shopId, customerId, items[], paymentMode)` → creates `DraftBill` + `BillItem` records, returns bill with totals
- `confirmBill(billId)` → calls `inventory.decrementStock()` for each item + calls `khata.applyBillToBalance()` if credit, updates `DraftBill.status = 'confirmed'`
- `cancelBill(billId)` → sets status to `cancelled`

### `inventory.ts`
- `getStock(shopId, productId)` → returns current stock + whether below threshold
- `getLowStockItems(shopId)` → returns all products below `reorderThreshold`
- `decrementStock(shopId, productId, quantity, reason)` → updates `Product.currentStock` + creates `StockMovement`
- `incrementStock(shopId, productId, quantity, reason)` → same but direction `in`

### `khata.ts`
- `getBalance(shopId, customerId)` → returns `Customer.outstandingBalance`
- `applyBillToBalance(shopId, customerId, billTotal)` → increments balance + creates `KhataTransaction` (type: `bill`)
- `recordPayment(shopId, customerId, amount)` → decrements balance + creates `KhataTransaction` (type: `payment`)

### `procurement.ts`
- `checkAndDraftReorder(shopId)` → finds all low-stock items, groups by preferred supplier, creates `ReorderDraft` records with status `draft_created`
- `approveReorderDraft(draftId)` → sets status to `simulated_sent`, creates `AuditEvent`
- `cancelReorderDraft(draftId)` → sets status to `cancelled`

### `audit.ts`
- `logEvent(shopId, sessionId, step, label, eventType, opts)` → creates `AuditEvent` record
- `getSessionEvents(sessionId)` → returns ordered events for a session

---

## Adapter layer (fixtures-first)

Create `/lib/adapters/` with these three files. **See `fixture_map.md` for exact input→output mappings** — implement each fixture exactly as specified there.

### `intent.ts`
```typescript
// Fixture-first intent detection
// Returns: { intent, entities, confidence, agentsSuggested }
// Fixtures keyed by normalized input pattern — see fixture_map.md Section 2
// Toggle real API with NEXT_PUBLIC_USE_REAL_AI=true
```

Must handle these intents with fixtures:
- `create_bill` — extracts items[], customer, paymentMode
- `check_stock` — extracts product query
- `record_payment` — extracts customer, amount
- `daily_summary` — no entities needed
- `approve_action` — maps to pending card
- `reject_action` — maps to pending card

Ambiguity: if "Ram" matches 2+ customers or "tel" matches 2+ products, return `confidence: 'low'` with `clarificationOptions[]`.

### `voice.ts`
```typescript
// transcribeVoice(audioRef: string): Promise<string>
// Fixture: map known demo audio refs to their Hinglish transcripts
// Real: call Deepgram STT API or browser Web Speech API if NEXT_PUBLIC_USE_REAL_AI=true
```

### `invoice.ts`
```typescript
// extractInvoiceItems(imageRef: string): Promise<ExtractedItem[]>
// Fixture: return seeded extraction for 'invoice_photo_demo_001.jpg'
// Real: call Claude Sonnet with vision if NEXT_PUBLIC_USE_REAL_AI=true
```

---

## Chat API routes

Create these Route Handlers:

- `POST /api/v1/chat/[shopId]/messages/text` — receive text, run `intent.ts`, return interaction_id + next_state
- `POST /api/v1/chat/[shopId]/messages/voice` — receive audio_ref, call `voice.ts` then `intent.ts`, return transcription + next_state
- `POST /api/v1/chat/[shopId]/messages/image` — receive image_ref, call `invoice.ts`, return extraction preview
- `POST /api/v1/interactions/[interactionId]/resolve` — handle approval or clarification selection, run business logic, return outcome card
- `GET /api/v1/chat/[shopId]/sessions/[sessionId]` — return current chat state + pending cards

---

## Shopkeeper UI screens

### `/app/shopkeeper/page.tsx` — WhatsApp Chat Home (Screen 22)

Layout: Mobile frame `390×844px` centered inside desktop shell for demo visibility.

Create a `MobileFrame` wrapper component in `/components/ui/mobile-frame.tsx`:
```tsx
export function MobileFrame({ children }: { children: React.ReactNode }) {
  return (
    <div className="mx-auto w-[390px] h-[844px] rounded-[2.5rem] border-2 border-slate-300 overflow-hidden shadow-xl bg-white flex flex-col">
      {children}
    </div>
  );
}
```

The observer canvas (Sprint 3) will embed this same component in its center column.

Components to build in `/components/chat/`:
- `ChatHeader` — assistant name "Rupantar Assistant", status "Shop Ops Active"
- `MessageBubble` — user (right, green) + assistant (left, white) variants
- `VoiceNoteMessage` — waveform placeholder SVG + duration + transcribing state
- `ImageMessage` — thumbnail + extracting state
- `QuickReplyChips` — "Bill banao", "Stock check", "Khata dekho", "Aaj ka summary"
- `ChatComposer` — text input + voice button + image upload button

**Voice input in demo mode:** The voice button does NOT require a real microphone. Instead, it opens a dropdown of pre-recorded demo options:
- "Demo 1: Bill banao (voice)" → sends `audioRef: "voice_demo_001"`
- "Demo 2: Stock check" → sends `audioRef: "voice_demo_002"`
- "Demo 3: Payment" → sends `audioRef: "voice_demo_003"`
- etc. (see `fixture_map.md` Section 1 for all 7 voice refs)

The voice adapter returns the fixture transcript for the selected audioRef. This avoids any microphone dependency during demos.

Opening message (exact Hinglish copy from wireframe spec screen 22):
> "Namaste Ramesh bhai 👋 Main aapka Rupantar Assistant hoon..."

### Action cards (rendered inline in chat thread):

- `VoiceReviewCard` — transcript + detected items + customer + "Sahi hai" / "Edit karo" / "Cancel" (Screen 23)
- `BillPreviewCard` — customer name, line items with prices, total, "Confirm bill" / "Edit items" / "Cancel" (Screen 24)
- `PaymentKhataCard` — old balance, payment, new balance, receipt prompt (Screen 26)
- `ClarificationCard` — 2 options as tap buttons, handles both customer and product ambiguity (Screen 29)

Exact Hinglish copy for all cards from `03_wireframe_spec.md` screens 23–29.

---

## Interaction state machine

Implement this state machine in the `sessionStore`:

States: `idle → text_submitted → parsing → draft_ready → awaiting_approval → executing → completed`

The store drives what card is shown in the thread at any time.

---

## Acceptance criteria for Sprint 1

- [ ] User can type "Ram ne 500 de diye" → payment card shows correct balances → DB `KhataTransaction` created
- [ ] User can trigger voice bill flow → bill preview shows 3 items → confirm → `DraftBill` confirmed + inventory decremented + khata updated
- [ ] "Tel" input triggers clarification card with 2 oil options
- [ ] "Ram" input triggers clarification card with Ram bhai + Hotel Ram
- [ ] Bill total > ₹500 shows approval gate before confirming
- [ ] Every interaction creates an `AuditEvent` in DB
- [ ] `GET /api/v1/chat/:shopId/sessions/:sessionId` returns chat state with messages array
- [ ] Chat renders correctly in mobile frame (390px width)
- [ ] All Hinglish copy matches wireframe spec exactly

---

## Before starting Sprint 2

**Recommended:** Run the Sprint Reviewer agent to verify service signatures and fixture alignment. Start a new Claude Code session, paste `build_brief.md`, then paste `agents/sprint_reviewer.md`. Tell it you just completed Sprint 1. This is especially important because Sprint 2 (sandbox tests) and Sprint 3 (observer) both depend heavily on Sprint 1's service interfaces and adapter fixtures.

---

## What NOT to build in this sprint

- No stock/reorder card yet (Sprint 4)
- No daily summary card yet (Sprint 4)
- No photo extraction card yet (Sprint 4)
- No partner console yet (Sprint 2)
- No observer canvas yet (Sprint 3)
