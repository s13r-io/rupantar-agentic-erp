# Fixture Map — Deterministic Demo Responses

Every demo scenario must run **without** an `ANTHROPIC_API_KEY`. This file specifies the exact input→output mappings for all three AI adapters and the 7 scenario step sequences. Implement these in Sprint 1 (`/lib/adapters/`) and harden in Sprint 4 (`/lib/fixtures/scenario-responses.ts`).

---

## 1. Voice adapter fixtures (`voice.ts`)

The `transcribeVoice(audioRef)` function maps demo audio references to Hinglish transcripts.

| `audioRef` | Transcript | Used in flow |
|---|---|---|
| `voice_demo_001` | "Ram ko 2 kilo chawal, 1 tel aur 3 biscuit ka bill bana do. Udhar mein daal do." | Flow 1 — Voice bill |
| `voice_demo_002` | "Sunflower oil kitna bacha hai?" | Flow 2 — Stock query |
| `voice_demo_003` | "Ram ne 500 de diye." | Flow 4 — Payment |
| `voice_demo_004` | "Aaj ka summary." | Flow 5 — Daily summary |
| `voice_demo_005` | "Ram ka balance batao." | Flow 6A — Ambiguous customer |
| `voice_demo_006` | "Tel order kar do." | Flow 6B — Ambiguous product |
| `voice_demo_007` | "Hotel Ganesh ke liye 5 kilo basmati rice aur 2 atta ka bill banao. Credit mein." | Approval gate test (total > ₹500) |

**Fallback:** Any unrecognized `audioRef` returns `"Yeh voice note samajh nahi aaya. Dubara try karo."` with `simulated: true`.

---

## 2. Intent adapter fixtures (`intent.ts`)

The `detectIntent(text, shopId)` function returns `{ intent, entities, confidence, clarificationOptions, agentsSuggested }`.

### Input: "Ram ko 2 kilo chawal, 1 tel aur 3 biscuit ka bill bana do. Udhar mein daal do."

```json
{
  "intent": "create_bill",
  "entities": {
    "customer_query": "Ram",
    "items": [
      { "product_query": "chawal", "quantity": 2, "unit": "kilo" },
      { "product_query": "tel", "quantity": 1, "unit": "piece" },
      { "product_query": "biscuit", "quantity": 3, "unit": "piece" }
    ],
    "payment_mode": "credit"
  },
  "confidence": "high",
  "clarificationOptions": null,
  "agentsSuggested": ["billing", "inventory", "khata"]
}
```

**Entity resolution (done by billing service, not adapter):**

| Query | Resolution | Rationale |
|---|---|---|
| "Ram" (customer) | `cust_ram_bhai` (confidence: high) | "Udhar mein" implies credit customer. Ram bhai has `credit_enabled: true`. Hotel Ram also matches "Ram" but the credit context disambiguates. |
| "chawal" (product) | `prod_regular_rice_loose` (confidence: high) | Memory entry `alias_chawal_prefers_regular`: "When user says 'chawal' in small basket billing, prefer regular loose rice." |
| "tel" (product) | **AMBIGUOUS** → triggers clarification | Both `prod_sunflower_oil_1l` and `prod_groundnut_oil_1l` have "tel" in aliases. No memory entry resolves this. |
| "biscuit" (product) | `prod_parle_g_small` (confidence: high) | Only product with "biscuit" alias. |

**Bill calculation (after "tel" resolved to sunflower oil):**

| Item | Product | Qty | Unit price | Line total |
|---|---|---|---|---|
| chawal | Regular Chawal Loose | 2 kg | ₹60 | ₹120 |
| tel | Sunflower Oil 1L | 1 | ₹160 | ₹160 |
| biscuit | Parle-G Small | 3 | ₹10 | ₹30 |
| **Total** | | | | **₹310** |

> Note: ₹310 < ₹500 threshold, so **no approval gate** for this bill. To test the approval gate feature, use `voice_demo_007` (see below).

---

### Input: "Sunflower oil kitna bacha hai?"

```json
{
  "intent": "check_stock",
  "entities": {
    "product_query": "sunflower oil"
  },
  "confidence": "high",
  "clarificationOptions": null,
  "agentsSuggested": ["inventory"]
}
```

**Resolution:** `prod_sunflower_oil_1l` — current_stock: 4, reorder_threshold: 6 → **low-stock warning triggered**.

**Expected follow-up:** Reorder suggestion card — 12 units from Bharat Traders (preferred supplier for oil category).

---

### Input: "Ram ne 500 de diye."

```json
{
  "intent": "record_payment",
  "entities": {
    "customer_query": "Ram",
    "amount": 500
  },
  "confidence": "high",
  "clarificationOptions": null,
  "agentsSuggested": ["khata"]
}
```

**Resolution:** `cust_ram_bhai` — payment context ("de diye" = gave money) disambiguates from Hotel Ram.

**Expected state change:**
- Old balance: ₹1,850
- Payment: ₹500
- New balance: ₹1,350
- KhataTransaction record: `{ type: "payment", amount: 500, balanceAfter: 1350 }`

---

### Input: "Aaj ka summary."

```json
{
  "intent": "daily_summary",
  "entities": {},
  "confidence": "high",
  "clarificationOptions": null,
  "agentsSuggested": ["daily_summary"]
}
```

**Expected card values (from seed `daily_state`):**
- Total sales: ₹8,540
- Cash: ₹5,900
- Credit: ₹2,640
- Dues received: ₹500
- Low-stock count: 2 (sunflower oil, Parle-G)
- Pending dues customers: 3 (Ram bhai, Shyam, Hotel Ram)
- Recommendation: "Kal subah Bharat Traders ko order draft approve karna useful rahega."

---

### Input: "Ram ka balance batao."

```json
{
  "intent": "check_balance",
  "entities": {
    "customer_query": "Ram"
  },
  "confidence": "low",
  "clarificationOptions": [
    { "id": "cust_ram_bhai", "label": "Ram bhai (₹1,850 baki)" },
    { "id": "cust_hotel_ram", "label": "Hotel Ram (₹900 baki)" }
  ],
  "agentsSuggested": ["khata"]
}
```

**Resolution:** AMBIGUOUS — "Ram" matches both `cust_ram_bhai` (aliases: `["ram", "ram bhai"]`) and `cust_hotel_ram` (aliases: `["ram hotel", "ram"]`). No context clue to disambiguate. ClarificationCard shown.

**After user selects "Ram bhai":**
- Show khata balance: ₹1,850 outstanding
- No state mutation for a balance query

---

### Input: "Tel order kar do."

```json
{
  "intent": "create_reorder",
  "entities": {
    "product_query": "tel"
  },
  "confidence": "low",
  "clarificationOptions": [
    { "id": "prod_sunflower_oil_1l", "label": "Sunflower Oil 1L (4 left, threshold 6)" },
    { "id": "prod_groundnut_oil_1l", "label": "Groundnut Oil 1L (9 left, threshold 5)" }
  ],
  "agentsSuggested": ["procurement"]
}
```

**After user selects "Sunflower Oil 1L":**
- Creates `ReorderDraft` with status `draft_created`
- Items: `[{ productId: "prod_sunflower_oil_1l", quantity: 12 }]` (reorderQuantity from product)
- Supplier: `sup_bharat_traders` (preferred supplier)
- Approval required (per shop rules `reorder_requires_approval: true`)

---

### Input: "Hotel Ganesh ke liye 5 kilo basmati rice aur 2 atta ka bill banao. Credit mein."

```json
{
  "intent": "create_bill",
  "entities": {
    "customer_query": "Hotel Ganesh",
    "items": [
      { "product_query": "basmati rice", "quantity": 5, "unit": "kilo" },
      { "product_query": "atta", "quantity": 2, "unit": "piece" }
    ],
    "payment_mode": "credit"
  },
  "confidence": "high",
  "clarificationOptions": null,
  "agentsSuggested": ["billing", "inventory", "khata"]
}
```

**Entity resolution:**

| Query | Resolution | Rationale |
|---|---|---|
| "Hotel Ganesh" | `cust_hotel_ganesh` | Exact alias match. `credit_enabled: true`, `approval_limit_override: 2500`. |
| "basmati rice" | `prod_basmati_rice_5kg` | Exact alias match. unit_type is "piece" (5kg bags). "5 kilo" → 1 bag. |
| "atta" | `prod_atta_10kg` | Single match. |

**Bill calculation:**

| Item | Product | Qty | Unit price | Line total |
|---|---|---|---|---|
| basmati rice | Basmati Rice 5kg | 1 bag | ₹690 | ₹690 |
| atta | Atta 10kg | 2 | ₹420 | ₹840 |
| **Total** | | | | **₹1,530** |

> ₹1,530 > ₹500 threshold → **approval gate triggered**. Shopkeeper must tap "Confirm" before bill is committed.

---

### Action intents (no entity extraction needed)

| Input text | Intent | Maps to |
|---|---|---|
| "Sahi hai" / "Confirm" / "Haan" | `approve_action` | Approves the current pending card (bill, reorder, etc.) |
| "Nahi" / "Cancel" / "Rehne do" | `reject_action` | Cancels the current pending action |
| "Edit karo" / "Badlo" | `edit_action` | Returns to editable state for current draft |
| "Abhi nahi" | `dismiss_action` | Dismisses suggestion without mutation |

---

## 3. Invoice extraction adapter fixtures (`invoice.ts`)

The `extractInvoiceItems(imageRef)` function returns extracted items with match confidence.

### Input: `invoice_photo_demo_001`

```json
{
  "extractedItems": [
    {
      "itemName": "Sunflower Oil 1L",
      "quantity": 12,
      "confidence": "high",
      "matchedProductId": "prod_sunflower_oil_1l"
    },
    {
      "itemName": "Parle-G",
      "quantity": 24,
      "confidence": "high",
      "matchedProductId": "prod_parle_g_small"
    },
    {
      "itemName": "Toor Dal 1kg",
      "quantity": 10,
      "confidence": "high",
      "matchedProductId": "prod_toor_dal_1kg"
    },
    {
      "itemName": "Refined Oil",
      "quantity": 6,
      "confidence": "low",
      "matchedProductId": null
    }
  ],
  "simulated": true
}
```

**Expected flow:** Photo extraction card shows 4 items. First 3 are auto-matched. "Refined Oil" shows low confidence — user must select from product list or dismiss. After confirmation, `incrementStock()` is called for each accepted item.

**Fallback:** Any unrecognized `imageRef` returns `{ "extractedItems": [], "error": "Photo se items nahi nikal paaye. Clear photo try karo." }`.

---

## 4. Scenario-response map

Each scenario is a sequence of steps. When running in fixture mode, each step uses the adapter fixtures defined above. This map specifies the exact step sequence for `/lib/fixtures/scenario-responses.ts` (built in Sprint 4).

### Scenario 1: `scenario_morning_rush_billing`

**Duration:** ~90 seconds | **Tags:** Investor, Happy path

| Step | User action | Adapter called | Fixture key | Expected card | State change |
|---|---|---|---|---|---|
| 1 | Voice note (`voice_demo_001`) | `voice.ts` → `intent.ts` | `voice_demo_001` → `create_bill` | VoiceReviewCard (transcript + 3 items) | Message + InteractionRecord created |
| 2 | Tap "Sahi hai" (approve transcript) | `intent.ts` | `approve_action` | ClarificationCard ("tel" ambiguity) | None |
| 3 | Tap "Sunflower Oil 1L" | `intent.ts` | `clarification_resolved` | BillPreviewCard (3 items, ₹310) | None |
| 4 | Tap "Confirm bill" | `intent.ts` | `approve_action` | Bill confirmed card + balance update | DraftBill confirmed, inventory -3 items, KhataTransaction created, Ram bhai balance +₹310 |

**Audit events generated:** `intent_detected` → `agents_called(billing,inventory,khata)` → `voice_transcribed` → `bill_drafted` → `clarification_requested(tel)` → `clarification_resolved(sunflower_oil)` → `bill_confirmed` → `inventory_decremented(×3)` → `khata_updated`

---

### Scenario 2: `scenario_low_stock_reorder`

**Duration:** ~60 seconds | **Tags:** Investor, Happy path

| Step | User action | Adapter called | Fixture key | Expected card | State change |
|---|---|---|---|---|---|
| 1 | Type "Sunflower oil kitna bacha hai?" | `intent.ts` | `check_stock` | Stock response card (4 units, low badge) | InteractionRecord created |
| 2 | System auto-suggests reorder | (service logic) | — | Reorder suggestion card (12 units, Bharat Traders) | ReorderDraft created (status: `draft_created`) |
| 3 | Tap "Approve order" | `intent.ts` | `approve_action` | Order confirmed card ("simulated_sent" label) | ReorderDraft status → `simulated_sent`, AuditEvent logged |

**Audit events:** `intent_detected` → `stock_queried(sunflower_oil, 4)` → `low_stock_detected` → `reorder_drafted` → `reorder_approved` → `supplier_notified(simulated)`

---

### Scenario 3: `scenario_payment_received`

**Duration:** ~45 seconds | **Tags:** Investor, Happy path

| Step | User action | Adapter called | Fixture key | Expected card | State change |
|---|---|---|---|---|---|
| 1 | Type "Ram ne 500 de diye." | `intent.ts` | `record_payment` | PaymentKhataCard (₹1,850 → ₹1,350) | KhataTransaction created, Ram bhai balance decremented |
| 2 | Dismiss receipt prompt | — | — | Card dismissed | None |

**Audit events:** `intent_detected` → `agents_called(khata)` → `payment_recorded(500)` → `balance_updated(1850→1350)`

---

### Scenario 4: `scenario_invoice_photo`

**Duration:** ~75 seconds | **Tags:** Investor, Happy path

| Step | User action | Adapter called | Fixture key | Expected card | State change |
|---|---|---|---|---|---|
| 1 | Upload image (`invoice_photo_demo_001`) | `invoice.ts` | `invoice_photo_demo_001` | PhotoExtractionCard (4 items, 1 low confidence) | InteractionRecord created |
| 2 | Select product for "Refined Oil" or dismiss | — | — | Updated extraction card | None |
| 3 | Tap "Confirm stock update" | `intent.ts` | `approve_action` | Stock updated confirmation | `incrementStock()` for 3-4 items, StockMovement records |

**Audit events:** `image_received` → `invoice_extracted(4 items)` → `low_confidence_flagged(refined_oil)` → `user_resolved` → `stock_incremented(×3-4)`

---

### Scenario 5: `scenario_daily_summary`

**Duration:** ~30 seconds | **Tags:** Investor, Happy path

| Step | User action | Adapter called | Fixture key | Expected card | State change |
|---|---|---|---|---|---|
| 1 | Type "Aaj ka summary." | `intent.ts` | `daily_summary` | DailySummaryCard (6 metrics + recommendation) | DailySummary record created |
| 2 | Tap "Theek hai" | — | — | Card dismissed | None |

**Audit events:** `intent_detected` → `summary_generated` → `summary_dismissed`

> Note: Summary card values should be computed from actual DB state (DraftBill, KhataTransaction, StockMovement records), not hardcoded. The seed `daily_state` values serve as expected baseline.

---

### Scenario 6: `scenario_ambiguity_customer`

**Duration:** ~60 seconds | **Tags:** Investor, Edge case

| Step | User action | Adapter called | Fixture key | Expected card | State change |
|---|---|---|---|---|---|
| 1 | Type "Ram ka balance batao." | `intent.ts` | `check_balance` (low confidence) | ClarificationCard (Ram bhai / Hotel Ram) | InteractionRecord created |
| 2 | Tap "Ram bhai (₹1,850 baki)" | — | — | Balance display card (₹1,850) | None (read-only query) |

**Alternate path (cancel):**

| Step | User action | Expected card | State change |
|---|---|---|---|
| 2-alt | Tap "Cancel" | Return to idle | None — no mutation |

**Then test product ambiguity:**

| Step | User action | Adapter called | Fixture key | Expected card | State change |
|---|---|---|---|---|---|
| 3 | Type "Tel order kar do." | `intent.ts` | `create_reorder` (low confidence) | ClarificationCard (Sunflower / Groundnut) | InteractionRecord created |
| 4 | Tap "Sunflower Oil 1L" | — | — | Reorder draft card (12 units, Bharat Traders) | ReorderDraft created |

**Audit events:** `confidence_low` → `clarification_requested(customer:ram)` → `clarification_resolved(ram_bhai)` → `balance_queried` | `confidence_low` → `clarification_requested(product:tel)` → `clarification_resolved(sunflower_oil)` → `reorder_drafted`

---

### Scenario 7: `scenario_partner_deploy`

**Duration:** ~5 minutes | **Tags:** Partner, Happy path

This scenario runs in the **partner console**, not the shopkeeper chat.

| Step | Wizard step | Action | Expected result | State change |
|---|---|---|---|---|
| 1 | Basic Details | Fill: "Jai Shree Krishna Store", owner "Amit Shah", Ahmedabad, Hinglish | Form validates | Shop record created (status: `draft`) |
| 2 | Bundle Selection | Pre-selected "Kirana Core Bundle" (7 agents) | Bundle card shown, locked | None |
| 3 | Catalog Import | Click "Load sample catalog" | 14 products populate table | Product records created |
| 4 | Customers + Khata | Click "Load sample customers" or add manually | 3+ customers in table | Customer records created |
| 5 | Suppliers + Reorder | Click "Load sample suppliers" or add manually | 2+ suppliers with categories | Supplier records created |
| 6 | Language / Trust / Rules | Review 3 config cards, adjust if needed | Settings saved | ShopRules record created |
| 7 | Sandbox Test Lab | Run "Test billing", "Test stock query", "Test payment" | 3+ tests pass with green checkmarks | SandboxTest records, Shop status → `sandbox` |
| 8 | Go Live Summary | Review checklist, tap "Go Live" | Success confirmation | Shop status → `live`, AuditEvent logged |

**Post go-live verification:**
- New shop appears in partner portfolio with "Live" chip
- Health dashboard accessible with zero-state metrics
- Shopkeeper chat works for the new shop

---

## 5. Confidence scoring rules

These rules apply to all adapter fixtures:

| Confidence | Condition | Adapter behavior |
|---|---|---|
| `high` | Single unambiguous match + supporting context (e.g., memory entry) | Return resolved entity directly |
| `medium` | Single match but no supporting context | Return entity + flag for approval |
| `low` | Multiple matches OR no match | Return `clarificationOptions[]` or error |

**Memory entries that affect resolution** (from seed data):

| Memory key | Effect on resolution |
|---|---|
| `alias_chawal_prefers_regular` | "chawal" in small billing → `prod_regular_rice_loose` (not basmati) |
| `cust_ram_bhai_usually_credit` | "Ram" + credit context → `cust_ram_bhai` (not Hotel Ram) |
| `alias_tel_ambiguous` | "tel" always triggers clarification (no memory resolves this) |

---

## 6. Hinglish copy registry

All user-facing Hinglish strings for shopkeeper action cards. Implement these exactly — do not paraphrase.

### Chat

| Context | Copy |
|---|---|
| Welcome message | "Namaste Ramesh bhai :wave: Main aapka Rupantar Assistant hoon. Aap mujhe voice note ya message bhej sakte ho. Main bill bana sakta hoon, stock check kar sakta hoon, khata update kar sakta hoon, aur aaj ka summary bhej sakta hoon." |
| Quick reply chips | "Bill banao" · "Stock check" · "Khata dekho" · "Aaj ka summary" |

### VoiceReviewCard

| Element | Copy |
|---|---|
| Header | "Aapne yeh bola:" |
| Approve button | "Sahi hai" |
| Edit button | "Edit karo" |
| Cancel button | "Cancel" |

### BillPreviewCard

| Element | Copy |
|---|---|
| Header | "Bill preview" |
| Confirm button | "Confirm bill" |
| Edit button | "Edit items" |
| Cancel button | "Cancel" |

### PaymentKhataCard

| Element | Copy |
|---|---|
| Header | "Khata update" |
| Receipt prompt | "Receipt note bhejna hai?" |

### ClarificationCard

| Element | Copy |
|---|---|
| Header (customer) | "Kaun sa customer?" |
| Header (product) | "Kaun sa product?" |
| Cancel button | "Cancel" |

### StockReorderCard

| Element | Copy |
|---|---|
| Stock result | "[Product]: [N] units bache hain. Yeh low stock mein hai." |
| Reorder suggestion | "Order draft dikhao" / "Abhi nahi" |
| Pending order | "Order abhi send nahi hua hai. Aapke approval ka wait hai." |
| Approve button | "Approve order" |
| Edit button | "Quantity change karo" |
| Cancel button | "Cancel" |
| Simulated label | "Order abhi send nahi hua" (shown after approval, with `simulated_sent` status) |

### DailySummaryCard

| Element | Copy |
|---|---|
| Header | "Aaj ka summary" |
| Recommendation (example) | "Kal subah Bharat Traders ko order draft approve karna useful rahega." |
| Buttons | "Voice mein sunao" · "Detail bhejo" · "Theek hai" |

### PhotoExtractionCard

| Element | Copy |
|---|---|
| Processing | "Photo se items nikal rahe hain..." |
| Low confidence | "Yeh item match nahi hua — select karo ya skip karo" |
| Confirm button | "Confirm stock update" |

> For exact screen-by-screen copy beyond these cards, refer to `planning/horizon1_markdown_docs/03_wireframe_spec.md`.

---

## 7. Error / fallback fixtures

| Scenario | Adapter response |
|---|---|
| Unrecognized voice input | `{ intent: "unknown", confidence: "low", agentsSuggested: [] }` + assistant message: "Samajh nahi aaya. Dubara try karo ya type karo." |
| Unrecognized text input | `{ intent: "unknown", confidence: "low" }` + assistant message: "Yeh samajh nahi aaya. Aap bill, stock check, payment ya summary ke baare mein pooch sakte ho." |
| Unrecognized image | `{ extractedItems: [] }` + assistant message: "Photo se items nahi nikal paaye. Clear photo try karo." |
| Product not found in catalog | Entity resolution returns `null` + assistant message: "Yeh product aapke catalog mein nahi mila." |
| Customer not found | Entity resolution returns `null` + assistant message: "Yeh customer nahi mila. Naam dubara check karo." |
