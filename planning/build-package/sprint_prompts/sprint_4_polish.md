# Sprint 4 — Remaining Cards, AI Adapters + Demo Polish

**Before using this prompt:** paste the contents of `build_brief.md` first, then paste this file.

**Assumes Sprints 0–3 are complete:** All core flows working, observer canvas live, partner wizard deployed.

---

## Goal

Complete the remaining shopkeeper cards (stock/reorder, daily summary, photo extraction), wire the optional real AI adapters, harden all 7 demo scenarios with deterministic fixtures, and prepare the prototype for demo-ready delivery. By end of this sprint, the prototype passes all three tiers of `evals.md`.

---

## Remaining shopkeeper cards

Add these to `/components/chat/`. **See `fixture_map.md` for exact fixture values and Hinglish copy for each card.**

### `StockReorderCard` (Screens 25 + 30 in wireframe spec)

Two states:

**State 1 — Stock result:**
```
"Sunflower oil 1L: 4 units bache hain. Yeh low stock mein hai."
Suggested order: 12 units from Bharat Traders — ₹1,680
```
Buttons: "Order draft dikhao" / "Abhi nahi"

**State 2 — Order draft:**
```
"Order abhi send nahi hua hai. Aapke approval ka wait hai."
```
Buttons: "Approve order" / "Quantity change karo" / "Cancel"

On approve: calls `procurement.approveReorderDraft()` → sets `ReorderDraft.status = 'simulated_sent'`

### `DailySummaryCard` (Screen 28)

Calculates values from real DB state at time of trigger:
- Total sales (sum of confirmed DraftBill.total for today)
- Cash / credit breakdown
- Dues received (sum of KhataTransaction type=payment for today)
- Low-stock count (from `inventory.getLowStockItems()`)
- Pending dues count (customers with outstanding_balance > 0)
- One recommendation line (generated from state: if low stock → suggest reorder approval)

Buttons: "Voice mein sunao" (plays fixture audio or calls TTS) / "Detail bhejo" (simulated_sent) / "Theek hai"

### `PhotoExtractionCard` (Screen 27 + 31)

**Flow:**
1. User uploads image (demo: pre-loaded `invoice_photo_demo_001.jpg`)
2. Calls `invoice.ts` adapter → returns fixture extraction:
   - Sunflower oil 1L — 12 units
   - Parle-G — 24 packs
   - Toor dal 1kg — 10 packs
   - "Refined Oil" — `confidence: 'low'`
3. Extraction preview card shows items with low-confidence warning
4. "Confirm stock add" → calls `inventory.incrementStock()` for each confirmed item
5. Low-confidence item shows edit option before committing

Photo extraction state machine from `05_developer_handoff_packet.md` section 9.4:
`idle → uploading → extracting → preview_ready → editing → committing → completed`

---

## AI adapter enhancement

Upgrade `/lib/adapters/` to support the `.env`-toggled real API overlay:

### `intent.ts` — enhance

Add real API path using Anthropic Claude (model: `claude-haiku-4-5` for cost efficiency):
```typescript
import Anthropic from '@anthropic-ai/sdk';

if (process.env.NEXT_PUBLIC_USE_REAL_AI === 'true') {
  const anthropic = new Anthropic(); // uses ANTHROPIC_API_KEY env var
  // System prompt: include shop name, language, product list, customer list
  // User message: the shopkeeper's input text
  // Return structured JSON: { intent, entities, confidence, clarificationOptions? }
}
```

Install: `npm install @anthropic-ai/sdk`

Fallback: always fall back to fixture if real API returns error or takes > 3s.

### `voice.ts` — enhance

Real path: Deepgram STT API (`nova-2` model) or browser Web Speech API. Input: audio blob or file reference.
Fixture: map demo audio refs to pre-written Hinglish transcripts (see `fixture_map.md` Section 1).

> Note: Voice transcription uses a dedicated STT service, not Claude, because real-time audio transcription requires a streaming speech-to-text pipeline. For the prototype, fixtures handle all demo scenarios — the real STT path is fully optional.

### `invoice.ts` — enhance

Real path: Claude Sonnet with vision (`claude-sonnet-4-6`). Send the invoice image with a prompt to extract: item name, quantity, unit.
Match extracted items against shop product list using fuzzy name matching (use `string-similarity` npm package).
Fixture: always return seeded extraction for demo invoice photo (see `fixture_map.md` Section 3).

Install: `npm install string-similarity`

**Critical:** All three adapters must log `simulated: true/false` in the `InteractionRecord` and `AuditEvent` they produce.

---

## Scenario fixture hardening

For each of the 7 scenarios in `/lib/fixtures/scenarios.ts`, ensure:
- Every step has a deterministic fixture response
- No live API call is required for the scenario to run end-to-end
- Demo operator can run the scenario without an `ANTHROPIC_API_KEY` set

Create `/lib/fixtures/scenario-responses.ts` with hardcoded response maps keyed by `(scenarioId, stepIndex)`.

---

## Demo polish tasks

### Copy audit
Go through every screen and verify all Hinglish copy exactly matches `03_wireframe_spec.md`. Fix any deviations.

### Mobile frame polish
- Ensure chat frame looks correct at 390px width on all major desktop browsers
- Add phone frame border (subtle gray rounded-3xl border) around the chat shell in observer canvas

### Loading states
- Add `Skeleton` components for: chat card loading, audit log loading, health dashboard KPIs
- Add toast notifications for: successful bill confirmation, payment recorded, stock updated

### Error states (shopkeeper-safe copy only)
- Parse error: "Mujhe yeh samajhne mein thodi problem aayi. Dobara try karein?"
- Stock error: "Abhi stock info nahi mil rahi. Thodi der baad try karein."
- Network error: show generic retry card — never show "500" or stack traces

### Scenario transitions
- Clicking "Restart" on observer canvas calls demo reset API and reloads scenario
- Scenario completion shows a "Scenario complete" overlay with time taken and next scenario suggestion

---

## Final integration checklist

Run these before marking Sprint 4 complete:

### All 7 flows from `acceptance_criteria.md`
- [ ] Flow 1: Voice bill on credit — all 8 criteria
- [ ] Flow 2: Stock query + low stock — all 5 criteria
- [ ] Flow 3: Reorder draft + approval — all 5 criteria
- [ ] Flow 4: Payment received — all 4 criteria
- [ ] Flow 5: Daily summary — all 4 criteria
- [ ] Flow 6: Ambiguity handling — all 5 criteria
- [ ] Flow 7: Partner deploys new shop — all 7 criteria

### Engineering truth (from `evals.md` Tier 2)
- [ ] All 6 DB state checks pass
- [ ] All API responses carry correct `simulated` flag
- [ ] Demo reset restores seed state in ≤ 10 seconds

### Demo truth (from `evals.md` Tier 3)
- [ ] 5-minute demo runs 3x clean
- [ ] 15-minute walkthrough has no dead ends
- [ ] Vercel production URL is live and shareable

---

## After Sprint 4 — Demo readiness checks

Before declaring demo-ready, run these two agents in separate Claude Code sessions (paste `build_brief.md` first, then the agent prompt):

1. **UI Auditor** — paste `agents/ui_auditor.md`. Checks color palette, typography, layout, chat bubbles, status chips, and Hinglish copy against the style brief. ~10–15 min.

2. **Eval Runner** (**required**) — paste `agents/eval_runner.md`. Walks through all 3 tiers of `evals.md` systematically: product truth, engineering truth, demo truth. Produces a Demo Readiness Report. ~20–30 min.

Fix any blocking issues from the Eval Runner report before sharing the prototype.

---

## What is explicitly NOT in scope

- Production WhatsApp Business API integration
- Real UPI payment confirmation
- Multi-vertical support
- SDK / marketplace
- Full 12-language support
- Production observability (DataDog, Sentry, etc.)
