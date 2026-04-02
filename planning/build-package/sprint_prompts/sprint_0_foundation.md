# Sprint 0 — Foundation

**Before using this prompt:** paste the contents of `build_brief.md` first, then paste this file.

---

## Goal

Set up the entire project foundation: Next.js app, UI system, database schema, seed data, Zustand stores, and the role selector landing screen. By end of this sprint, the app should deploy to Vercel and show the role selector screen with seeded data in the database.

---

## What to build

### 1. Project init
- `npx create-next-app@latest rupantar-h1-prototype --typescript --tailwind --app --src-dir=false`
- Install: `zustand`, `@prisma/client`, `prisma`, `zod`, `react-hook-form @hookform/resolvers`
- Initialize shadcn/ui: `npx shadcn-ui@latest init` (select `slate` base color, `neutral` style)
- Install shadcn/ui components:
  ```bash
  npx shadcn-ui@latest add button card input dialog tabs skeleton select textarea form badge separator tooltip avatar scroll-area
  ```
- Create `.env.example` with:
  ```
  DATABASE_URL=postgresql://user:pass@host/db?sslmode=require
  NEXT_PUBLIC_USE_REAL_AI=false
  ANTHROPIC_API_KEY=
  ```

### 2. Prisma schema

Create `prisma/schema.prisma` with **exactly these 16 models** and appropriate field types:

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

### 3. Seed script

Create `prisma/seed.ts` that:
- Creates shop "Shree Ganesh Kirana" with `id = "shop_shree_ganesh_kirana"`
- Creates all products, customers, suppliers, rules, and memory entries from `build_brief.md` seed data
- Sets Ram bhai outstanding_balance = 1850, Shyam = 450
- Sets Sunflower oil 1L current_stock = 4 (below threshold of 6 — triggers low-stock demo)
- Sets Parle-G current_stock = 5 (below threshold of 10 — triggers low-stock demo)
- Upserts all records (safe to re-run)

Add to `package.json`: `"prisma": { "seed": "ts-node --compiler-options {\"module\":\"CommonJS\"} prisma/seed.ts" }`

### 4. Zustand stores

Create these 5 store files in `/lib/stores/`:

- `sessionStore.ts` — `currentRole`, `currentScenarioId`, `currentShopId`, `currentSessionId`, `chatMessages[]`, `pendingCards[]`, `sessionStatus`
- `partnerWizardStore.ts` — `stepStates`, `shopDraft`, `productsDraft[]`, `customersDraft[]`, `suppliersDraft[]`, `rulesDraft`, `sandboxTestResults[]`
- `observerStore.ts` — `selectedScenario`, `playbackState`, `selectedEventId`, `showRawInput`, `showMemory`, `showStateChanges`
- `auditStore.ts` — `events[]`, `replayFrames[]`, `filters`
- `uiStore.ts` — `activeDrawer`, `activeModal`, `toastQueue[]`

### 5. Role selector screen

Implement `/app/page.tsx` as the landing role selector with:
- Rupantar logo + "Horizon 1 Prototype" hero title
- 3 main role cards: Shopkeeper / Partner / Observer
- 1 smaller "Demo Operator" card
- Each card links to `/?role=<role>` which sets role in sessionStore and redirects
- Footer: "Prototype scope: Kirana only · Horizon 1 · v1"
- "Reset demo data" button (top right) that calls `POST /api/v1/demo/reset`

Exact copy from wireframe spec screen 01 in `03_wireframe_spec.md`.

### 6. Demo reset API

Create `/app/api/v1/demo/reset/route.ts`:
- Accepts `POST` with body `{ reset_inventory, reset_balances, reset_chat, reload_seed_data }`
- Re-runs the seed upsert logic for selected entities
- Returns standard envelope with list of what was reset

### 7. Bootstrap API

Create `/app/api/v1/bootstrap/route.ts`:
- Returns roles, default shop ID, default scenarios list
- Used by role selector to confirm DB connection on load

### 8. CLAUDE.md for the app repo

Create `CLAUDE.md` in the repo root with:
- What this is (Rupantar H1 Prototype — Kirana Ops)
- Tech stack (one line each)
- Folder structure (the structure from build_brief.md)
- Real vs simulated rule
- API envelope convention
- "Do not introduce" list
- Link to planning docs: these live in the parent planning repo (not this repo)

### 9. Vercel setup

- Add `vercel.json` with `{ "framework": "nextjs" }`
- Document in `README.md` how to set `DATABASE_URL` (Neon connection string) in Vercel environment variables

---

## Acceptance criteria for Sprint 0

- [ ] `npm run dev` starts without errors
- [ ] `npx prisma db push` + `npx prisma db seed` completes without errors
- [ ] Role selector screen renders at `localhost:3000`
- [ ] Clicking "Enter as Shopkeeper" sets role in store and navigates to `/shopkeeper`
- [ ] `GET /api/v1/bootstrap` returns 200 with roles and default_shop_id
- [ ] `POST /api/v1/demo/reset` returns 200 and re-seeds the DB
- [ ] App deploys to Vercel with no build errors
- [ ] Vercel URL shows the role selector screen

---

## Before starting Sprint 1

**Recommended:** Run the Sprint Reviewer agent to catch issues before they compound. Start a new Claude Code session, paste `build_brief.md`, then paste `agents/sprint_reviewer.md`. Tell it you just completed Sprint 0. Fix any FAIL items before proceeding.

---

## What NOT to build in this sprint

- No chat UI yet
- No partner wizard yet
- No observer canvas yet
- No business logic services yet
- No AI adapters yet
