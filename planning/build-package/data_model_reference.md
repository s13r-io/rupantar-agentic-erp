# Data Model Reference — Rupantar H1 Prototype

Quick-access reference for the Prisma schema, model relationships, and seed data IDs. Use this during Sprints 2–4 instead of re-reading `sprint_0_foundation.md`.

---

## Quick reference: 16 models

| Model | Key fields | Belongs to | Has many |
|---|---|---|---|
| **Shop** | shopName, ownerName, city, language, deploymentStatus | — | Products, Customers, Suppliers, ShopRules, MemoryEntries, Sessions, ReorderDrafts, DailySummaries, AuditEvents, SandboxTests |
| **Product** | displayName, aliases[], sellingPrice, currentStock, reorderThreshold | Shop | StockMovements, BillItems |
| **Customer** | displayName, aliases[], creditEnabled, outstandingBalance | Shop | KhataTransactions, DraftBills |
| **Supplier** | supplierName, categoriesSupplied[], leadTimeDays | Shop | ReorderDrafts |
| **ShopRules** | billApprovalThresholdInr, reorderRequiresApproval, clarifyAmbiguous* | Shop (1:1) | — |
| **MemoryEntry** | entityType, memoryKey, memoryValue, source | Shop | — |
| **Session** | scenarioId?, role, status | Shop | Messages, InteractionRecords, AuditEvents |
| **Message** | sender, type, text?, audioRef?, imageRef? | Session | — |
| **InteractionRecord** | rawInput, parsedIntent?, confidenceScore?, agentsCalled[], simulated | Session | — |
| **DraftBill** | total, paymentMode, status | Customer? | BillItems |
| **BillItem** | quantity, unitPrice, lineTotal | DraftBill, Product | — |
| **StockMovement** | direction, quantity, reason | Product | — |
| **KhataTransaction** | amount, type, balanceAfter | Customer | — |
| **ReorderDraft** | items (Json), status | Shop, Supplier? | — |
| **DailySummary** | totalSales, cashSales, creditSales, lowStockCount, summaryText? | Shop | — |
| **AuditEvent** | step, label, eventType, agent?, confidence?, simulated | Shop, Session? | — |
| **SandboxTest** | testType, input, output (Json), status, agentsUsed[] | Shop | — |

---

## Key cross-sprint relationships

These relationships are referenced across multiple sprints. Understand them before starting Sprint 2+.

```
Shop ──┬── Products ──── BillItems ──── DraftBill ──── Customer
       │                 StockMovements
       ├── Customers ─── KhataTransactions
       ├── Suppliers ─── ReorderDrafts
       ├── ShopRules (1:1)
       ├── MemoryEntries
       ├── Sessions ──┬── Messages
       │              ├── InteractionRecords
       │              └── AuditEvents
       ├── DailySummaries
       ├── AuditEvents (also linked via Session)
       └── SandboxTests
```

**Critical join paths:**
- **Billing flow:** Session → InteractionRecord → DraftBill → BillItems → Product (inventory decrement) + Customer (khata update)
- **Observer feed:** Session → AuditEvents (ordered by step) — this is what the orchestration feed reads
- **Partner health:** Shop → DraftBills (sales count), Products (low-stock count), KhataTransactions (dues), AuditEvents (interaction count)

---

## Seed data IDs

Use these exact IDs in fixtures, tests, and scenario responses. They are created by `prisma/seed.ts` in Sprint 0.

### Shop

| ID | Display name | City | Status |
|---|---|---|---|
| `shop_shree_ganesh_kirana` | Shree Ganesh Kirana | Surat | `live` |

### Products (14)

| ID | Display name | Price | Stock | Threshold | Supplier |
|---|---|---|---|---|---|
| `prod_basmati_rice_5kg` | Basmati Rice 5kg | ₹690 | 3 | 6 | sup_bharat_traders |
| `prod_regular_rice_loose` | Regular Chawal Loose | ₹60/kg | 42 | 20 | sup_bharat_traders |
| `prod_atta_10kg` | Atta 10kg | ₹420 | 8 | 5 | sup_bharat_traders |
| `prod_sugar_1kg` | Sugar 1kg | ₹46 | 26 | 12 | sup_bharat_traders |
| `prod_sunflower_oil_1l` | Sunflower Oil 1L | ₹160 | **4** | **6** | sup_bharat_traders |
| `prod_groundnut_oil_1l` | Groundnut Oil 1L | ₹175 | 9 | 5 | sup_bharat_traders |
| `prod_toor_dal_1kg` | Toor Dal 1kg | ₹130 | 11 | 6 | sup_bharat_traders |
| `prod_maggi_pack` | Maggi Pack | ₹14 | 36 | 12 | sup_shiv_distributors |
| `prod_parle_g_small` | Parle-G Small | ₹10 | **5** | **10** | sup_shiv_distributors |
| `prod_bread_britannia` | Britannia Bread | ₹45 | 7 | 6 | sup_fresh_mart_supply |
| `prod_milk_500ml` | Milk 500ml | ₹28 | 15 | 10 | sup_fresh_mart_supply |
| `prod_tea_powder_250g` | Tea Powder 250g | ₹95 | 10 | 5 | sup_shiv_distributors |
| `prod_detergent_1kg` | Detergent 1kg | ₹120 | 9 | 4 | sup_shiv_distributors |
| `prod_bath_soap` | Bath Soap | ₹35 | 20 | 8 | sup_shiv_distributors |

**Bold** = below reorder threshold (triggers low-stock demo).

### Customers (5)

| ID | Display name | Credit | Balance | Aliases |
|---|---|---|---|---|
| `cust_ram_bhai` | Ram bhai | yes | ₹1,850 | "ram", "ram bhai" |
| `cust_shyam` | Shyam | yes | ₹450 | "shyam bhai" |
| `cust_meena_aunty` | Meena aunty | no | ₹0 | "meena" |
| `cust_hotel_ganesh` | Hotel Ganesh | yes | ₹5,200 | "hotel", "ganesh hotel" |
| `cust_hotel_ram` | Hotel Ram | yes | ₹900 | "ram hotel", "ram" |

**Ambiguity seeds:** "Ram" matches `cust_ram_bhai` + `cust_hotel_ram`.

### Suppliers (3)

| ID | Name | Categories | Lead time |
|---|---|---|---|
| `sup_bharat_traders` | Bharat Traders | grains, oil, pulses | 1 day |
| `sup_shiv_distributors` | Shiv Distributors | snacks, beverages, homecare, personalcare | 2 days |
| `sup_fresh_mart_supply` | Fresh Mart Supply | fresh | 1 day |

### Memory entries (5)

| Key | Value | Source |
|---|---|---|
| `preferred_language` | Hinglish | config |
| `summary_time` | 21:00 | config |
| `cust_ram_bhai_usually_credit` | Ram bhai usually buys on credit. | learned |
| `alias_tel_ambiguous` | The word 'tel' may refer to sunflower oil or groundnut oil. | inferred |
| `alias_chawal_prefers_regular` | When user says 'chawal' in small basket billing, prefer regular loose rice. | learned |

### Daily summary seed state (baseline for Flow 5)

These values represent the expected daily summary after seed data is loaded. Use them to verify `DailySummaryCard` output.

| Metric | Seed value |
|---|---|
| Total sales | ₹8,540 |
| Cash sales | ₹5,900 |
| Credit sales | ₹2,640 |
| Dues received | ₹500 |
| Low-stock count | 2 (sunflower oil, Parle-G) |
| Pending dues customers | 3 (Ram bhai, Shyam, Hotel Ram) |
| Recommendation | "Kal subah Bharat Traders ko order draft approve karna useful rahega." |

> Note: These values come from the seed `daily_state` in `04_component_inventory.md`. In the running prototype, the daily summary card should compute values from actual DB records (`DraftBill`, `KhataTransaction`, `StockMovement`), not hardcode these numbers. These serve as the expected baseline for a freshly-seeded demo.

---

## Full Prisma schema

Exact copy from `sprint_0_foundation.md`. This is the authoritative schema — do not deviate.

```prisma
model Shop {
  id               String   @id @default(cuid())
  shopName         String
  ownerName        String
  phoneNumber      String
  city             String
  language         String   @default("Hinglish")
  vertical         String   @default("kirana")
  gstStatus        String   @default("non_gst")
  businessHoursOpen  String @default("08:00")
  businessHoursClose String @default("22:00")
  summaryTime      String   @default("21:00")
  deploymentStatus String   @default("draft")
  createdAt        DateTime @default(now())
  products         Product[]
  customers        Customer[]
  suppliers        Supplier[]
  rules            ShopRules?
  memoryEntries    MemoryEntry[]
  sessions         Session[]
  reorderDrafts    ReorderDraft[]
  dailySummaries   DailySummary[]
  auditEvents      AuditEvent[]
  sandboxTests     SandboxTest[]
}

model Product {
  id                  String   @id @default(cuid())
  shopId              String
  displayName         String
  aliases             String[]
  category            String
  unitType            String
  packSize            String?
  sellingPrice        Float
  currentStock        Float
  reorderThreshold    Float
  reorderQuantity     Float
  preferredSupplierId String?
  shop                Shop     @relation(fields: [shopId], references: [id])
  stockMovements      StockMovement[]
  billItems           BillItem[]
}

model Customer {
  id                    String   @id @default(cuid())
  shopId                String
  displayName           String
  aliases               String[]
  phoneNumber           String?
  creditEnabled         Boolean  @default(false)
  outstandingBalance    Float    @default(0)
  reminderAfterDays     Int      @default(7)
  approvalLimitOverride Float?
  shop                  Shop     @relation(fields: [shopId], references: [id])
  khataTransactions     KhataTransaction[]
  draftBills            DraftBill[]
}

model Supplier {
  id                  String   @id @default(cuid())
  shopId              String
  supplierName        String
  phoneNumber         String?
  categoriesSupplied  String[]
  leadTimeDays        Int      @default(1)
  shop                Shop     @relation(fields: [shopId], references: [id])
  reorderDrafts       ReorderDraft[]
}

model ShopRules {
  id                        String  @id @default(cuid())
  shopId                    String  @unique
  language                  String  @default("Hinglish")
  tone                      String  @default("hinglish")
  billApprovalThresholdInr  Float   @default(500)
  reorderRequiresApproval   Boolean @default(true)
  clarifyAmbiguousCustomer  Boolean @default(true)
  clarifyAmbiguousProduct   Boolean @default(true)
  sendDailySummaryAt        String  @default("21:00")
  shop                      Shop    @relation(fields: [shopId], references: [id])
}

model MemoryEntry {
  id          String   @id @default(cuid())
  shopId      String
  entityType  String
  memoryKey   String
  memoryValue String
  source      String
  lastUsedAt  DateTime @default(now())
  shop        Shop     @relation(fields: [shopId], references: [id])
}

model Session {
  id           String   @id @default(cuid())
  shopId       String
  scenarioId   String?
  role         String
  startedAt    DateTime @default(now())
  endedAt      DateTime?
  status       String   @default("active")
  shop         Shop     @relation(fields: [shopId], references: [id])
  messages     Message[]
  interactions InteractionRecord[]
  auditEvents  AuditEvent[]
}

model Message {
  id         String   @id @default(cuid())
  sessionId  String
  sender     String
  type       String
  text       String?
  audioRef   String?
  imageRef   String?
  timestamp  DateTime @default(now())
  state      String   @default("shown")
  session    Session  @relation(fields: [sessionId], references: [id])
}

model InteractionRecord {
  id             String   @id @default(cuid())
  sessionId      String
  rawInput       String
  parsedIntent   String?
  confidenceScore String?
  agentsCalled   String[]
  status         String   @default("completed")
  simulated      Boolean  @default(false)
  session        Session  @relation(fields: [sessionId], references: [id])
}

model DraftBill {
  id          String     @id @default(cuid())
  shopId      String
  sessionId   String?
  customerId  String?
  total       Float
  paymentMode String     @default("cash")
  status      String     @default("draft")
  createdAt   DateTime   @default(now())
  customer    Customer?  @relation(fields: [customerId], references: [id])
  items       BillItem[]
}

model BillItem {
  id         String    @id @default(cuid())
  billId     String
  productId  String
  quantity   Float
  unitPrice  Float
  lineTotal  Float
  bill       DraftBill @relation(fields: [billId], references: [id])
  product    Product   @relation(fields: [productId], references: [id])
}

model StockMovement {
  id        String   @id @default(cuid())
  shopId    String
  productId String
  direction String
  quantity  Float
  reason    String
  createdAt DateTime @default(now())
  product   Product  @relation(fields: [productId], references: [id])
}

model KhataTransaction {
  id           String   @id @default(cuid())
  shopId       String
  customerId   String
  amount       Float
  type         String
  balanceAfter Float
  createdAt    DateTime @default(now())
  customer     Customer @relation(fields: [customerId], references: [id])
}

model ReorderDraft {
  id         String   @id @default(cuid())
  shopId     String
  supplierId String?
  items      Json
  status     String   @default("draft_created")
  createdAt  DateTime @default(now())
  shop       Shop     @relation(fields: [shopId], references: [id])
  supplier   Supplier? @relation(fields: [supplierId], references: [id])
}

model DailySummary {
  id               String   @id @default(cuid())
  shopId           String
  date             String
  totalSales       Float    @default(0)
  cashSales        Float    @default(0)
  creditSales      Float    @default(0)
  duesReceived     Float    @default(0)
  lowStockCount    Int      @default(0)
  pendingDuesCount Int      @default(0)
  summaryText      String?
  createdAt        DateTime @default(now())
  shop             Shop     @relation(fields: [shopId], references: [id])
}

model AuditEvent {
  id                 String   @id @default(cuid())
  sessionId          String?
  shopId             String
  step               Int
  label              String
  eventType          String
  agent              String?
  confidence         String?
  memoryUsed         String?
  recordChanges      Json?
  observerAnnotation String?
  simulated          Boolean  @default(false)
  createdAt          DateTime @default(now())
  shop               Shop     @relation(fields: [shopId], references: [id])
  session            Session? @relation(fields: [sessionId], references: [id])
}

model SandboxTest {
  id              String   @id @default(cuid())
  shopId          String
  testType        String
  input           String
  output          Json?
  status          String   @default("pending")
  agentsUsed      String[]
  confidenceBand  String?
  createdAt       DateTime @default(now())
  shop            Shop     @relation(fields: [shopId], references: [id])
}
```
