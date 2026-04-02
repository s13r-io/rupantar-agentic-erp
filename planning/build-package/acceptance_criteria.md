# Acceptance Criteria — Rupantar H1 Prototype

Each flow is "done" when **all** criteria in its checklist pass. These apply to seeded demo data (Shree Ganesh Kirana).

---

## Flow 1 — Voice bill on credit (Priority: P0)

**Input:** Voice note / text "Ram ko 2 kilo chawal, 1 tel aur 3 biscuit ka bill bana do. Udhar mein daal do."

Done when:
- [ ] Voice review card shows correct transcript and extracted items
- [ ] "Tel" ambiguity triggers clarification (sunflower oil vs groundnut oil)
- [ ] Bill preview card shows: customer = Ram bhai, 3 items, correct totals
- [ ] Bill total ₹310 (< ₹500 threshold) — confirm happens **without** approval gate
- [ ] Approval gate tested separately: use "Hotel Ganesh ke liye 5 kilo basmati rice aur 2 atta ka bill banao. Credit mein." (₹1,530 > ₹500 → approval gate triggers)
- [ ] On confirm: inventory decrements for all 3 items
- [ ] On confirm: Ram bhai's khata balance increases by bill total
- [ ] Audit trail records: intent_detected → agents_called → bill_drafted → approval_requested → confirmed → state_updated
- [ ] Observer right panel shows the agent routing in real time

---

## Flow 2 — Stock query + low stock detection (Priority: P0)

**Input:** "Sunflower oil kitna bacha hai?"

Done when:
- [ ] Stock response card shows: product name, current quantity (4 units), low-stock warning badge (below threshold = 6)
- [ ] Reorder suggestion card appears: 12 units from Bharat Traders, estimated value shown
- [ ] Buttons: "Order draft dikhao" / "Abhi nahi"
- [ ] Draft stays as `draft_created` — not sent until approved
- [ ] "Abhi nahi" dismisses without placing order
- [ ] Approving draft sets status to `simulated_sent` + shows "Order abhi send nahi hua" label (see `fixture_map.md` Hinglish copy registry)

---

## Flow 3 — Reorder draft + approval (Priority: P1)

**Input:** Triggered from low-stock detection or proactive stock check.

Done when:
- [ ] Reorder draft card shows supplier name, item list, estimated value
- [ ] Approval buttons: "Approve order" / "Quantity change karo" / "Cancel"
- [ ] Approving creates a `ReorderDraft` record with status `simulated_sent`
- [ ] Partner exception queue clears once approved
- [ ] Audit event logged for draft creation and approval

---

## Flow 4 — Payment received / khata update (Priority: P0)

**Input:** "Ram ne 500 de diye."

Done when:
- [ ] Khata update card shows: old balance, payment amount, new balance
- [ ] `KhataTransaction` record created (type: `payment`)
- [ ] Ram bhai's `outstanding_balance` decreases by ₹500 in DB
- [ ] Optional receipt prompt appears ("Receipt note bhejna hai?")
- [ ] Audit event logged

---

## Flow 5 — Daily summary (Priority: P1)

**Input:** "Aaj ka summary" (manual trigger only — no scheduled 9 PM cron in H1 prototype).

Done when:
- [ ] Summary card shows: total sales, cash, credit, dues received, low-stock count, pending dues count
- [ ] Values are calculated from actual `DraftBill`, `KhataTransaction`, and `StockMovement` records created during the session
- [ ] At least one recommendation line appears ("Kal subah Bharat Traders ko order approve karna useful rahega.")
- [ ] "Theek hai" dismisses the card

---

## Flow 6 — Ambiguity handling (Priority: P0)

**Input A:** "Ram ka balance batao." (2 customers: Ram bhai + Hotel Ram)  
**Input B:** "Tel order kar do." (2 products: sunflower oil + groundnut oil)

Done when:
- [ ] Clarification card lists both options as tap buttons (never guesses)
- [ ] Selecting one option continues the flow correctly
- [ ] Cancelling returns to idle without any state mutation
- [ ] Audit trail shows: `confidence_low → clarification_requested → clarification_resolved`

---

## Flow 7 — Partner deploys a new shop (Priority: P1)

Done when:
- [ ] Partner can complete all 8 wizard steps: basic details → bundle → catalog → customers → suppliers → rules → sandbox → go-live
- [ ] Cannot proceed past catalog step without at least 1 product entered
- [ ] Cannot go live without at least one sandbox test passing
- [ ] Go-live changes shop `deployment_status` from `sandbox` to `live`
- [ ] Shop appears in partner portfolio with "Live" chip
- [ ] Health dashboard is accessible immediately after go-live

---

## Global criteria (apply to all flows)

- [ ] Every state-changing action writes an `AuditEvent` record
- [ ] Observer right panel reflects agent routing within 1 second of action
- [ ] All API responses include `"simulated": true/false` in meta
- [ ] Shopkeeper never sees internal agent names — only the assistant identity
- [ ] Demo reset (`POST /api/v1/demo/reset`) restores all seed state in ≤10 seconds
- [ ] All 7 flows can run back-to-back after a single reset without manual patching
