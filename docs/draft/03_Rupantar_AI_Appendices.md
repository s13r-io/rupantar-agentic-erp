# Rupantar AI — Appendices

## Reference Material for Meeting Discussion

**March 2026 | Confidential**

---

> **Usage note:** The chairman may never read these. Team members use them during the discussion meeting for reference. The Full Proposal contains all conclusions; these appendices contain the underlying detail.

---

# Appendix A: Full Vertical Deep Dives (All 20)

> Each vertical below includes: addressable shops, current penetration, market reality, what we build, and key agent features. The 5 T1 ★ verticals receive full treatment in the Full Proposal (Section 4.2). All 20 are reproduced here for meeting reference.

---

## A.01 — Billing, POS & Invoicing

| | |
|---|---|
| **Addressable Shops** | ~50M |
| **Current Penetration** | 15–20% |
| **Existing Leaders** | Tally (38%), Vyapar (13%), Marg (11%), Busy (9%), MyBillBook (7%) |

**Market Reality.** Tally's dominance is accountant-driven, not shopkeeper-driven. Vyapar and MyBillBook have traction on mobile but still require a UI interaction for every bill. 80%+ of India's shops remain on paper because no product meets them via voice in their own language.

**What We Build.** Voice-first Billing Agent — shopkeeper speaks an order in Hindi/Hinglish, agent generates a GST-compliant bill, identifies the customer, applies pending discounts or credit, and sends it via WhatsApp. Zero screen interaction.

**Key Agent Features:**
- **Voice Billing** — Parses spoken orders (Hindi/Hinglish/regional) into structured bills — handles local aliases, unit variations, combo deals
- **Smart Scan** — Photo or barcode → auto-identifies SKU, fetches price, adds to bill
- **Customer Memory** — Recognises returning customers by phone number or UPI ID — auto-applies saved price, credit, preferred items
- **GST Engine** — Auto-assigns HSN codes and tax slabs, generates e-invoice for B2B buyers, validates bill
- **Day Close Agent** — Tallies cash + UPI + credit sales, flags discrepancies, sends WhatsApp summary
- **Offline Sync** — Queues transactions during outage, syncs with conflict resolution on reconnect

---

## A.02 — Inventory Management

| | |
|---|---|
| **Addressable Shops** | ~10–15M with meaningful stock |
| **Current Penetration** | 8–12% (bundled with POS) |
| **Existing Leaders** | Marg ERP, GoFrugal, Tally — all bundled. No standalone. |

**Market Reality.** Shop owners discover stockouts when a customer asks for something. Inventory is tracked on paper or memory. The AI opportunity is to make stockouts predictable 3–5 days in advance and auto-resolve without owner action.

**What We Build.** Autonomous Stock Intelligence Agent — monitors real-time inventory, predicts stockouts, auto-generates purchase orders confirmed by one WhatsApp reply.

**Key Agent Features:**
- **Live Stock Tracker** — Deducts on every sale — handles loose-weight items, variants, combo packs
- **Stockout Predictor** — Uses 90-day velocity + festival calendar + local events to flag items running out in 3–5 days
- **Auto-Reorder** — Generates PO to preferred supplier at reorder level; owner approves with "haan"
- **Expiry Watchdog** — For pharma, grocery, FMCG — alerts 30/15/7 days before expiry
- **Shrinkage Detective** — Compares expected vs counted stock; categorises variance as theft, breakage, or error
- **New Product Intake** — Owner photos new delivery → agent extracts details via vision, creates catalogue entry

---

## A.03 — Accounting & GST Compliance

| | |
|---|---|
| **Addressable Shops** | ~10M GST-registered shops |
| **Current Penetration** | 18–22% |
| **Existing Leaders** | Tally (47%), Busy (11%), Zoho Books (7%), ClearTax (6%) |

**Market Reality.** Tally dominates because CAs use it. Most small shops pay a CA ₹5,000–15,000/year for manual GST filing. The AI opportunity is to auto-maintain books from every transaction and auto-file returns — making the CA redundant for routine compliance.

**What We Build.** Autonomous Compliance Agent — silently posts every transaction to the right ledger, prepares GSTR-1 and GSTR-3B, reconciles purchase data, and files with one WhatsApp approval.

**Key Agent Features:**
- **Auto-Bookkeeper** — Every sale, purchase, expense auto-posts from billing/payment data — zero manual entry
- **GST Filing Agent** — Month-end: prepares GSTR-1 + GSTR-3B, reconciles with GSTR-2A, files with one approval
- **e-Way Bill Agent** — Auto-generates for goods movement above ₹50K
- **Expense Capture** — Owner photos receipt → agent extracts amount, vendor, date, posts to expense head
- **P&L Narrator** — Monthly 60-second Hindi voice note: "aapka is mahine ₹18,500 profit hua, GST ₹2,100 file hoga"
- **Deadline Agent** — 7/3/1-day reminders with status "ready to file" or "data missing"

---

## A.04 — Digital Payments & UPI

| | |
|---|---|
| **Addressable Shops** | ~50M accept digital payments |
| **Current Penetration** | 60–70% |
| **Existing Leaders** | Paytm (30%), PhonePe (30%), BharatPe (12%), Google Pay (10%) |

**Market Reality.** UPI acceptance is solved — soundboxes reached even semi-literate vendors. The gap is intelligence on top of payments: reconciling who paid, following up on unpaid balances, and predicting cash flow.

**What We Build.** Payment Intelligence Layer — reconciliation and cash-flow intelligence sitting on top of existing UPI.

**Key Agent Features:**
- **Payment Reconciler** — Parses UPI SMS/webhook — matches every credit to open order or customer
- **Collection Agent** — Sends personalised WhatsApp reminders at optimal times, escalates with days overdue
- **Cash Flow Forecast** — Projects 14/30-day cash position from expected collections, supplier dues, expenses
- **Fraud Flag** — Detects fake payment screenshots, duplicate transaction IDs, screen-recorded confirmations
- **Day Settlement** — Matches expected vs received cash + UPI, identifies over/short

---

## A.05 — Credit Ledger (Khata / Udhar)

| | |
|---|---|
| **Addressable Shops** | ~25–30M credit-extending shops |
| **Current Penetration** | 20–30% |
| **Existing Leaders** | Khatabook (40%), OkCredit (25%), Vyapar (20%) — all free tiers; weak monetisation |

**Market Reality.** Khatabook and OkCredit raised $275M+ combined and couldn't monetise because a free digital ledger creates no stickiness. The AI layer converts the khata into an active collection engine — making it worth paying for.

**What We Build.** Intelligent Credit Agent — manages the full credit lifecycle from entry to collection. Builds a credit profile connecting the shop to working capital loans.

**Key Agent Features:**
- **Voice Credit Entry** — "Ram ne 500 liya" → records, timestamps, links to Ram's profile
- **Smart Reminder** — Sends reminders at optimal times based on customer's known pay cycle
- **Pattern Analyser** — Learns when each customer pays; auto-schedules reminders
- **Credit Limit Advisor** — Flags customers approaching unsafe credit levels
- **Early Warning** — Identifies deteriorating payment behaviour before bad debt
- **Loan Connector** — Analyses 6-month transaction history → creditworthiness score → NBFC partner

---

## A.06 — Restaurant & F&B POS

| | |
|---|---|
| **Addressable Shops** | ~7.5M food service establishments |
| **Current Penetration** | 5–8% (~400–600K) |
| **Existing Leaders** | Petpooja (45%), Posist (10%), Rista (8%), GoFrugal (6%) |

**Market Reality.** Petpooja has strong SMB coverage at ₹10K/year. The AI opportunity goes beyond POS: intelligent KOT prioritisation, aggregator reconciliation, and predictive inventory-to-menu management. 6.5M+ dhabas and tea stalls remain completely unaddressed.

**What We Build.** Restaurant Co-Manager Agent — accepts orders across all channels, manages kitchen queue by prep time, auto-reconciles Swiggy/Zomato payouts, sends owner a morning brief.

**Key Agent Features:**
- **Multi-Channel Order Hub** — Counter, Swiggy, Zomato, WhatsApp, QR — queues by actual prep time
- **Kitchen Intelligence** — Routes to correct station, batches similar orders, estimates ready-time
- **Aggregator Reconciler** — Daily: compares expected vs paid, flags commission discrepancies
- **Menu Engineer** — Weekly: identifies high-profit/low-effort vs low-profit/high-effort dishes
- **86 Manager** — Cross-references inventory against menu — auto-marks unavailable items on all platforms
- **Morning Brief** — Yesterday's revenue, top dishes, delivery ratings, today's prep list via WhatsApp

---

## A.07 — Pharmacy & Chemist Software

| | |
|---|---|
| **Addressable Shops** | ~1.2M registered + ~300K unregistered chemists |
| **Current Penetration** | 30–40% |
| **Existing Leaders** | Marg ERP (38%), GoFrugal (13%), Pharmsoft (9%), hCue (5%) |

**Market Reality.** Pharmacy is best-penetrated because regulatory complexity forces adoption. The AI layer adds clinical safety (drug interactions), proactive patient management, and ABDM integration.

**What We Build.** Pharmacy Intelligence Agent — billing + compliance + clinical guardrails. Prescription reading via WhatsApp photo, drug interaction checking, chronic-patient refill reminders.

**Key Agent Features:**
- **Prescription Reader** — Customer sends photo → extracts drugs + doses, checks against dispensed items
- **Drug Interaction Check** — Multi-drug prescriptions — checks database before dispensing, not after
- **Expiry Action Agent** — 30-day: auto-generates return request; 7-day: donation/disposal alert
- **Chronic Refill Agent** — BP, diabetes, thyroid patients — WhatsApp reminder 5 days before run-out
- **Auto-Procurement** — Sales velocity + stock → daily PO to distributor via WhatsApp
- **ABDM Connector** — Links dispensing to ABHA ID; digital prescription pull; compliance prep

---

## A.08 — Salon, Spa & Beauty

| | |
|---|---|
| **Addressable Shops** | ~2M salons and beauty parlours |
| **Current Penetration** | 3–5% (~60–100K) |
| **Existing Leaders** | Zenoti (premium), Dingg (SMB, ~8K), MioSalon (~10K) |

**Market Reality.** ~95% of neighbourhood salons use paper appointment books and mental recall. The AI agent captures and scales the owner's personal memory so client experience survives staff turnover.

**What We Build.** Client Memory & Revenue Agent — bookings via WhatsApp/voice, full service history, empty-slot outreach, staff commission tracking.

**Key Agent Features:**
- **Booking Agent** — WhatsApp, voice, Instagram DM — checks stylist availability, confirms, reminds 24 hrs before
- **Client Memory** — Service history, colour formulas, preferred stylist, skin/hair type, product preferences
- **Empty Slot Filler** — Detects gaps → personalised outreach ("Priya, 5 weeks ho gaye, touch-up karein?")
- **Staff Commission Tracker** — Daily/monthly commission per staff by services + products + tips
- **Review Generator** — Post-service: WhatsApp request for Google/Justdial review with next-visit discount

---

## A.09 — B2B Procurement / Supply Chain

| | |
|---|---|
| **Addressable Shops** | ~15M+ shops that restock regularly |
| **Current Penetration** | 5–8% |
| **Existing Leaders** | Udaan (dominant, ₹5,706Cr FY24), Ninjacart (agri), Jumbotail (South) |

**Market Reality.** 85% of FMCG procurement happens through traditional distribution: salesman visits, phone orders, paper invoices. Udaan has B2B ecommerce scale but hasn't solved in-store procurement intelligence.

**What We Build.** Smart Procurement Agent — monitors stock, places orders with best-priced distributor, tracks trade schemes, disputes short deliveries.

**Key Agent Features:**
- **Smart Ordering** — Optimal PO based on velocity, events, credit — routes to best-priced distributor
- **Delivery Verification** — Compares received vs PO — flags shortages/wrong items/damage before delivery person leaves
- **Supplier Invoice Checker** — Matches invoice to PO and delivery note — flags discrepancies
- **Trade Scheme Tracker** — Monitors active buy-X-get-Y schemes; ensures shop claims maximum benefit
- **Credit Manager** — Tracks credit limit/outstanding per distributor — alerts before exhaustion

---

## A.10 — Online Store / eCommerce Enablement

| | |
|---|---|
| **Addressable Shops** | ~5–7M shops attempting online sales |
| **Current Penetration** | 5–7% |
| **Existing Leaders** | Shopify (D2C), Dukaan (~3M registered), Bikayi (~5L), ONDC |

**Market Reality.** Most SMBs create an online store and abandon within 60 days — catalog goes stale, orders missed, queries unanswered. The AI agent makes the online channel zero-effort.

**What We Build.** Online Store Manager Agent — auto-syncs offline catalog, answers queries 24/7, processes orders, runs promotions.

**Key Agent Features:**
- **Catalog Sync** — Mirrors offline inventory to online; marks out-of-stock in real-time
- **24/7 Query Agent** — Handles all customer questions on WhatsApp, website, Instagram DM
- **Order Processor** — Confirms, sends acknowledgment, books courier, generates label, tracks delivery
- **Promo Campaign Agent** — Weekly promotions based on excess stock and local events
- **ONDC Agent** — Maintains seller listings across buyer apps, manages ratings, handles lifecycle

---

## A.11 — Fashion, Garments & Apparel

| | |
|---|---|
| **Addressable Shops** | ~4–5M garment shops |
| **Current Penetration** | 5–8% (mostly chains) |
| **Existing Leaders** | Ginesys (chains), Logic ERP (~5K SME), Unicommerce (online) |

**Market Reality.** The core problem is the size-colour inventory matrix — every design has 12–40 variants. No affordable product solves this for standalone shops under ₹25,000/year. Dead season-end inventory is the biggest profit killer.

**What We Build.** Fashion Intelligence Agent — variant-level tracking, dead stock identification 3 weeks before season-end, targeted markdowns, next-season buying advice.

**Key Agent Features:**
- **Matrix Tracker** — Variant level (style × size × colour) — low vs overstocked
- **Dead Stock Alert** — Designs/variants unsold for 14/21/30 days — recommends markdown timing
- **Season Buying Advisor** — Based on previous season sell-through, recommends next cycle quantities
- **Bundle Optimizer** — Identifies products bought together — creates combos to move slow items
- **Returns Analyser** — Tracks returns by supplier and style — flags high-defect suppliers

---

## A.12 — Electronics Repair & Mobile Shops

> Full deep dive in Full Proposal Section 4.2.

| | |
|---|---|
| **Addressable Shops** | ~4–5M mobile and electronics repair shops |
| **Current Penetration** | <3% IMEI-specific |
| **Existing Leaders** | No SMB leader. Generic billing only. |
| **Score** | 90% (T1 ★) |

**What We Build.** Mobile Repair OS — customer WhatsApps damaged phone photo → digital job card, device identification, repair tracking, parts ordering, customer updates. Entire workflow via WhatsApp.

---

## A.13 — Grocery / Kirana Store OS

> Full deep dive in Full Proposal Section 4.2.

| | |
|---|---|
| **Addressable Shops** | ~12M kirana stores |
| **Current Penetration** | 8–12% |
| **Existing Leaders** | Vyapar, Khatabook, Udaan — all point solutions |
| **Score** | 90% (T1 ★) |

**What We Build.** Zero-UI Kirana OS — entire ERP via one WhatsApp number. Billing, khata, stock, ordering, delivery, daily report — all voice and WhatsApp.

---

## A.14 — HR & Payroll

| | |
|---|---|
| **Addressable Shops** | ~3–5M shops with 5+ paid staff |
| **Current Penetration** | 5–8% (10+ employee firms) |
| **Existing Leaders** | GreytHR (~25K companies), Keka (5K+), Kredily (20K+) |

**Market Reality.** For shops with 5–50 staff: attendance on paper, salary calculation on WhatsApp, PF filing once a year. The AI agent makes this invisible.

**What We Build.** Invisible HR Agent — runs attendance, payroll, compliance in background. Surfaces only for approvals and anomalies. Salary via UPI on salary day.

**Key Agent Features:**
- **Smart Attendance** — WhatsApp/QR/face scan check-in — handles late marks, half-days, overtime
- **Payroll Calculator** — Base, allowances, PF/ESI/TDS, advances — Hindi payslip
- **Salary Disbursement** — UPI transfer to each staff on salary day, confirms receipt
- **PF/ESI Filing** — Monthly ECR + ESIC challan — files with digital signature
- **Compliance Calendar** — Minimum wage, bonus, annual returns — advance warnings

---

## A.15 — Customer Loyalty & CRM

> Full deep dive in Full Proposal Section 4.2.

| | |
|---|---|
| **Addressable Shops** | ~50M shops with repeat customers |
| **Current Penetration** | <2% |
| **Existing Leaders** | Reelo (F&B), WhatsApp Business (informal), Capillary (enterprise) |
| **Score** | 87% (T1 ★) |

**What We Build.** Hyper-Personalisation Agent — replicates the shopkeeper's memory at scale. Personal outreach, birthday offers, win-back campaigns, referral tracking.

---

## A.16 — Logistics & Last-Mile Delivery

| | |
|---|---|
| **Addressable Shops** | ~5–8M shops doing home delivery |
| **Current Penetration** | 3–5% |
| **Existing Leaders** | Shiprocket/Delhivery (ecomm). Hyperlocal entirely manual. |

**Market Reality.** Most neighbourhood delivery is WhatsApp voice calls and personal bike riders with no tracking.

**What We Build.** Hyperlocal Delivery Agent — assigns orders by route proximity, WhatsApp-based customer tracking (no app), multi-drop route optimisation, failed delivery rescheduling.

**Key Agent Features:**
- **Smart Assignment** — Optimal delivery person by current location, pending orders, zone expertise
- **WhatsApp Tracking** — Live tracking link via WhatsApp — updates at pickup, enroute, delivery
- **Route Optimizer** — 5–10 simultaneous orders — optimal sequence by addresses and traffic
- **Failed Delivery Handler** — Contacts customer via WhatsApp, captures alternative instructions, reschedules
- **COD Tracker** — Tracks undeposited cash per delivery staff — flags overdue deposits

---

## A.17 — WhatsApp Commerce

> Full deep dive in Full Proposal Section 4.2.

| | |
|---|---|
| **Addressable Shops** | ~50M — WhatsApp is universal |
| **Current Penetration** | 20–30% informal; API <2% |
| **Existing Leaders** | WhatsApp Business, Interakt, AiSensy |
| **Score** | 83% (T1 ★) |

**What We Build.** Full-Stack WhatsApp Commerce Agent — complete commerce lifecycle on WhatsApp: catalog, voice ordering, payment, tracking, support — in customer's language, 24/7.

---

## A.18 — Auto Repair & Garage Management

> Full deep dive in Full Proposal Section 4.2.

| | |
|---|---|
| **Addressable Shops** | ~5M automobile workshops and garages |
| **Current Penetration** | <1% |
| **Existing Leaders** | No clear leader |
| **Score** | 90% (T1 ★) |

**What We Build.** Garage OS — digital job cards from vehicle photos, fault diagnosis, parts ordering, customer updates at every milestone. Entire flow via WhatsApp.

---

## A.19 — Hardware & Construction Retail

| | |
|---|---|
| **Addressable Shops** | ~2–3M hardware and building material shops |
| **Current Penetration** | <5% |
| **Existing Leaders** | Tally (generic only) |
| **Score** | 80% (T1) |

**Market Reality.** Hardware billing is complex: prices vary by customer relationship (contractor vs retail), quantity, payment mode. A contractor ordering across 3 sites on credit is impossible on Tally without custom development.

**What We Build.** Contractor Relationship Agent — contractor-specific rate cards, site-wise material tracking, multi-site billing, purchase bill digitisation, material calculator.

**Key Agent Features:**
- **Dynamic Rate Card** — Contractor-specific pricing without manual lookup
- **Site-wise Tracker** — Materials per construction site — enables site-wise billing and dispute resolution
- **Contractor Credit Manager** — Outstanding per contractor across sites — monthly statements, limit alerts
- **Purchase Bill Digitiser** — Owner photos supplier invoice → extracts items, quantities, rates, GST
- **Material Calculator** — "100 sq ft plastering" → required materials + quote

---

## A.20 — Education & Coaching Centres

| | |
|---|---|
| **Addressable Shops** | ~3M centres + 7–8M solo tutors |
| **Current Penetration** | 10–15% organised; <1% solo tutors |
| **Existing Leaders** | ClassPlus, Teachmint/Extramarks, SimpliFee, Fedena |

**Market Reality.** The organised market is served. The white space is 7–8 million solo tutors and small classes — collecting fees in cash, maintaining registers, communicating via WhatsApp groups.

**What We Build.** Tutor OS — fee collection, attendance, parent communication, student progress via WhatsApp. No separate app for parents.

**Key Agent Features:**
- **Fee Collection Agent** — Monthly reminder, receipt on payment, overdue tracking
- **Attendance Tracker** — Students mark via WhatsApp/location — alert parents of absent students
- **Parent Broadcast** — Homework, test dates, schedule changes to correct parent groups
- **Progress Report Agent** — Marks via voice/text → scorecards → monthly parent report in simple language
- **Enrollment Agent** — Prospective parent inquiry via WhatsApp → qualification → demo scheduling → follow-up

---

# Appendix B: Partner Programme Detail

## B.1 Full Tier Structure

| Tier | Name | Entry Criteria | Shop Portfolio | Technical Capability | Revenue Earning |
|---|---|---|---|---|---|
| T0 | Referral Agent | Register on app; 2-hr intro module | Refers only; no deployment | No technical skill | ₹200 one-time per activated referral |
| T1 | AI Shop Starter | 2-day certified training; 50-question assessment; 5 deployments within 60 days | 5–25 active shops | Deploys standard bundles from library; no custom flows | 15% recurring + ₹500 per new activation |
| T2 | AI Shop Builder | T1 + 3-day Builder training + visual flow certification; 25+ active shops | 25–150 active shops | Builds custom flows using visual builder; multi-agent configurations | 22% recurring + ₹1,000 per activation + own-priced customisation fees |
| T3 | AI Shop Architect | T2 + Pro Code certification; 150+ shops; 3 community templates rated 4+ | 150–500 active shops | Writes custom agent nodes (Python/JS); builds vertical solutions; trains T1/T2 | 30% recurring + ₹2,000 per activation + template marketplace royalties |
| T4 | Regional Master | Invite only; 10+ sub-partners; 500+ network shops; ₹25L annual revenue | 500+ shops across sub-partner network | Full platform access; runs training; co-develops verticals | 35% own shops + 5% override on sub-partner revenue + equity discussion |

## B.2 Complete Income Model Breakdown

| Income Stream | Mechanism | T0 | T1 | T2 | T3 | T4 |
|---|---|---|---|---|---|---|
| Subscription Commission | 15–30% of shop's monthly subscription | — | 15% | 22% | 30% | 35% |
| New Activation Fee | Per new shop live + 1 week active | — | ₹500 | ₹1,000 | ₹2,000 | ₹2,000 |
| Customisation Fees | For custom flows beyond standard bundles | — | — | Partner-priced (0% Rupantar cut) | Partner-priced | Partner-priced |
| Template Royalties | ₹50–₹200 per deployment of published template | — | — | — | Yes | Yes |
| AMC | ₹3,000–₹8,000/year per shop (partner keeps 100%) | — | — | Yes | Yes | Yes |
| Sub-Partner Override | % of sub-partner revenue | — | — | — | — | 5% |

**Worked example — T2 Partner with 100 shops:**

| Stream | Calculation | Monthly Income |
|---|---|---|
| Subscription Commission | 100 × ₹599 × 22% | ₹13,178 |
| Activation Fees | 20 new shops × ₹1,000 | ₹20,000 |
| Customisation | 5 implementations × ₹5,000 avg | ₹25,000 |
| Template Royalties | 2 templates × 100 deployments × ₹100 | ₹20,000 |
| AMC | 30 shops × ₹5,000/yr ÷ 12 | ₹12,500 |
| **Total** | | **₹90,678/month** |

## B.3 Training Curriculum (8 Modules)

| Module | Duration | Format | Content | Required For |
|---|---|---|---|---|
| M0: AI Basics for Shop Doctors | 3 hours | Video + quiz on mobile | What AI agents are vs apps. How WhatsApp-native agents work. How to explain AI to a semi-literate shopkeeper in 2 minutes without using the word "AI." | All tiers — mandatory |
| M1: Shop Pain Discovery | 4 hours | Role-play + facilitator | 15-question pain discovery interview. Mapping pain to agent type. Handling objections: "bahut complicated lagta hai," "pehle se Tally hai." | Tier 1+ |
| M2: Standard Bundle Deployment | 6 hours | Hands-on lab (sandbox shops) | Partner mobile app. Deploying 5 starter bundles: Kirana OS, Restaurant, Pharmacy, Salon, Billing+Khata. Configuring WhatsApp, catalog, language, tone. | Tier 1+ |
| M3: Visual Flow Builder | 2 days (14 hours) | Workshop + hands-on lab | Full builder interface. Connecting trigger → logic → action nodes. Configuring LLM prompts for shop context. Testing flows. Deploying to live shops. | Tier 2+ |
| M4: Vertical Specialisation | 1 day each | Vertical-specific deep-dive | Pharmacy: drug compliance + ABDM. Restaurant: aggregator reconciliation. Fashion: matrix inventory. Garage: job card + parts chain. Hardware: rate card + contractor billing. | Tier 2+ |
| M5: Portfolio Management | 4 hours | Dashboard + mentorship | Health dashboard. Upsell signals. Handling agent failures. Monthly review cadence. Referral mechanics: turning 5 shops into 50 via word-of-mouth. | Tier 2+ |
| M6: Pro Code SDK | 3 days | Developer workshop (Python/JS) | Building custom agent nodes. Publishing to marketplace. Non-standard API integrations. Community template contribution guidelines. | Tier 3+ |
| M7: Train the Trainer | 2 days | Train-the-trainer workshop | Running Tier 1 certification locally. Quality assessment. Managing sub-partner network. Regional go-to-market strategy. | Tier 4 only |

## B.4 Certification Requirements

Each tier requires passing a practical assessment — not a written test.

| Tier | Requirement | Assessment |
|---|---|---|
| T1 | 5 live shops with Shop Health Score >70% | Deploy 5 shops from sandbox to live; health score measured over 30 days |
| T2 | One custom flow deployed and active | Build and deploy a custom visual flow for a real shop; verified functional |
| T3 | One community template with 10+ deployments | Publish a template to the marketplace; achieve 10+ deployments by other partners with ≥4.0 rating |
| T4 | Invite only | Demonstrated revenue, sub-partner recruitment, regional impact |

---

# Appendix C: Unit Economics (All Scenarios)

## C.1 Per-Shop Unit Economics — Three Scenarios

| Metric | Conservative | Base Case | Optimistic |
|---|---|---|---|
| Average Monthly Subscription | ₹399 | ₹599 | ₹899 |
| Partner Commission (avg 22%) | ₹88 | ₹132 | ₹198 |
| Net Revenue to Rupantar | ₹311 | ₹467 | ₹701 |
| Cloud / LLM / API Costs per shop | ₹80 | ₹100 | ₹130 |
| Gross Profit per Shop per Month | ₹231 | ₹367 | ₹571 |
| **Gross Margin %** | **~58%** | **~61%** | **~64%** |
| Customer Acquisition Cost (partner) | ₹800 | ₹600 | ₹400 |
| Payback Period | 3.5 months | 1.6 months | 0.7 months |
| 12-Month LTV (net of commissions + COGS) | ₹2,772 | ₹4,404 | ₹6,852 |
| **LTV / CAC Ratio** | **3.5×** | **7.3×** | **17.1×** |

## C.2 Revenue Streams

| Revenue Stream | Model | Rupantar Net (after partner commission) |
|---|---|---|
| Shop Subscription (SaaS) | ₹299–₹1,499/month per shop | ~75–85% net |
| Agent Builder Platform Fee | ₹0 (T1) / ₹999/month (T2+) | 100% |
| Marketplace Royalties | 30% Rupantar / 70% template author | 30% of marketplace revenue |
| Vertical Add-on Modules | Premium agents (ABDM, GST e-invoice, aggregator reconciliation) | ~60–70% gross margin after API costs |
| B2B Intelligence Layer | Anonymised market data sold to FMCG brands and banks | 100% (after 1L+ active shops) |
| Embedded Financial Services | Working capital, insurance, BNPL via NBFC partners | 0.5–2% referral commission |

## C.3 Sensitivity Analysis

Key variables that affect unit economics:

| Variable | -20% Impact | -10% Impact | +10% Impact | +20% Impact |
|---|---|---|---|---|
| **ARPU (₹599 base)** | Gross margin: ~56% | Gross margin: ~59% | Gross margin: ~63% | Gross margin: ~66% |
| **LLM costs (₹100/shop base)** | Gross margin: ~64% | Gross margin: ~63% | Gross margin: ~60% | Gross margin: ~58% |
| **Partner commission (22% base)** | Gross margin: ~65% | Gross margin: ~63% | Gross margin: ~60% | Gross margin: ~57% |
| **Monthly churn (target <5%)** | LTV drops ~20% | LTV drops ~10% | LTV improves ~10% | LTV improves ~20% |

**Key takeaway:** The business is profitable across all reasonable scenarios. Even at -20% ARPU and +20% LLM costs simultaneously, gross margin remains >50% and LTV/CAC >2.0×.

## C.4 Comparable Benchmarks

| Benchmark | Metric | Source |
|---|---|---|
| Tally TDP network | 50K dealers → ₹900Cr revenue (₹1.5L revenue/dealer/year) | Tally Solutions public financials |
| Khatabook | $275M+ raised, 30M downloads, unable to monetise | PitchBook, TechCrunch |
| Fintech DSA income | ₹15–25K/month at 20 active clients | Industry benchmark |
| Zoho partner commissions | 15–30% recurring | Zoho partner programme |
| Petpooja ARPU | ₹10K/year (~₹833/month) | Petpooja public data |
| Vyapar churn (self-serve) | ~60–70% annual churn (estimate) | Industry observation |
| Tally TDP churn (partner-supported) | ~15–20% annual churn (estimate) | Tally dealer network analysis |

---

# Appendix D: Competitive Response Playbook

## D.1 Framework

For each potential competitor: what they could do, why it's structurally hard, and what Rupantar does if they try.

## D.2 Tally Solutions

**What they could do:** Add WhatsApp integration, voice commands, or AI features to their existing product.

**Why it's structurally hard:** Tally's 30-year architecture is accountant-driven and screen-first. Their user base (CAs and accountants) would resist a shift to voice-first, WhatsApp-native interaction. More importantly, their TDP partner network is incentivised to sell Tally licenses — not to become AI implementation specialists. Retraining 50,000 TDPs for a fundamentally different product philosophy would take 24+ months.

**Rupantar's response:** Position as complementary, not competing, in early stages. Target shops that Tally doesn't serve (the 80% on paper). Over time, Tally shops using Rupantar for WhatsApp-native operations alongside Tally for CA-facing compliance creates a dual-use pattern that is sticky for both.

## D.3 Zoho

**What they could do:** Build WhatsApp-native agents for their existing ERP suite (Zoho Books, Zoho Inventory, etc.).

**Why it's structurally hard:** Zoho's DNA is screen-first, English-first, SMB-to-enterprise. Building a zero-UI, vernacular, voice-first product for India's kirana stores is a fundamentally different product philosophy — not a feature addition. Their product-organisational structure optimises for horizontal SMB software across geographies, not deep vertical specialisation for Indian retail.

**Rupantar's response:** Speed. By the time Zoho recognises this market as worth entering, Rupantar has 50,000+ shops and 5,000+ partners. The partner network is the moat — Zoho would need to build one from scratch.

## D.4 PhonePe / Google Pay

**What they could do:** Expand from payments to merchant operations (billing, inventory, CRM).

**Why it's structurally hard:** Their DNA is payments-first. Merchant operations is a different product category with different acquisition, retention, and support dynamics. PhonePe's merchant base is broad but shallow — they know a payment happened, not what was sold, to whom, at what price, on credit or cash. The data depth required for operational AI doesn't exist in their current data model.

**Rupantar's response:** Integration, not competition. Rupantar's payment reconciliation agent sits on top of PhonePe/Google Pay — we make their payment data more valuable to the merchant, not less. Partnership is more likely than direct competition.

## D.5 Google (Gemini + WhatsApp Business API)

**What they could do:** Build a generic "AI agent for businesses" product using Gemini + WhatsApp.

**Why it's structurally hard:** Google builds horizontal platforms, not vertical-specific products for Indian kirana stores. Their strength is technology (Gemini) not distribution (they have no field sales force visiting shops). Even if they built the product, distribution would require the partner network Rupantar is building — and they can't replicate that quickly.

**Rupantar's response:** Use Gemini as one of multiple LLM providers. If Google builds a horizontal agent platform, Rupantar's vertical templates and partner network can run on it. The moat is the data and distribution, not the LLM.

## D.6 Meta (WhatsApp Parent)

**What they could do:** Build native WhatsApp business features that compete with Rupantar's agents.

**Why it's structurally hard:** Meta's WhatsApp Business API is a platform play — they want as many developers building on it as possible. Building their own vertical-specific agents would alienate their developer ecosystem. Their incentive is to make the API more powerful, not to compete with API users.

**Rupantar's response:** Close partnership with WhatsApp Business API team. If Meta builds AI features, they'll be horizontal (like chatbot templates). Rupantar's vertical depth and partner distribution remain differentiated.

## D.7 Reliance / Jio

**What they could do:** Leverage JioPhone user base and Reliance Retail partnerships to build a merchant operations tool.

**Why it's structurally hard:** Reliance's focus is consumer (JioMart, JioPhone) and organised retail (Reliance Retail). The 50M unorganised kirana market requires a field-force distribution model — which Reliance doesn't have for this segment. Their existing retail partnerships are with organised chains, not individual kirana stores.

**Rupantar's response:** If Reliance enters, Rupantar with 50K+ partners and 2L+ shops becomes an acquisition target, not a casualty. The partner network is a distribution asset that Reliance cannot build quickly.

## D.8 A Well-Funded Startup

**What they could do:** Copy the Rupantar model with more capital and a fresh brand.

**Why it's structurally hard:** They start with zero shops, zero partners, zero vernacular NLP data, and zero community templates. Even with unlimited capital, building the vernacular NLP depth takes years of real shop interaction data. The partner network takes 12–18 months to establish at scale. The community template library takes months of organic growth.

**Rupantar's response:** Speed and depth. Rupantar's 18-month head start means a competitor entering in 2028 faces a company with 2L+ shops, 10K+ partners, and NLP trained on millions of real transactions. The data moat compounds every month.

---

# Appendix E: Regulatory, Compliance & Data Governance Framework

## E.1 DPDP Act Compliance

The Digital Personal Data Protection Act (2023) governs how Rupantar handles personal data.

| Requirement | Rupantar's Approach |
|---|---|
| **Consent** | Explicit, granular consent for each data processing purpose — not blanket consent |
| **Data minimisation** | Collect only what is needed for agent functionality; no speculative data collection |
| **Purpose limitation** | Data collected for billing is not used for marketing without separate consent |
| **Storage limitation** | Data retained only as long as the shop is an active customer; defined retention periods per data type |
| **Data deletion** | Shop owners can request full data deletion via WhatsApp; completed within 30 days |
| **Data portability** | Shops can export their data in structured format at any time |
| **Grievance redressal** | Dedicated data grievance officer; WhatsApp-based grievance mechanism for shops |
| **Data fiduciary obligations** | Rupantar acts as data fiduciary, not data owner — this is architecturally embedded, not a policy overlay |

## E.2 GST Data Handling

| Requirement | Rupantar's Approach |
|---|---|
| **GSTN compliance** | All GST filing via official GSTN APIs; no data stored outside GSTN-approved systems |
| **E-invoice generation** | Compliant with GST e-invoice schema (Version 1.x); IRN generation via GSTN portal |
| **Record retention** | GST records retained for minimum 8 years as per GST Act |
| **Audit trail** | Complete agent decision audit trail for GST examinations |

## E.3 AI Governance Readiness

India is drafting AI governance regulations. Rupantar's architecture is designed for compliance:

| Principle | Implementation |
|---|---|
| **Explainability** | Every agent decision is traceable — input, NLP output, action taken, verification result |
| **Human oversight** | High-stakes actions (GST filing, orders >₹500) require explicit human approval |
| **Fairness** | Agent pricing and recommendations are not discriminatory; same inputs produce same outputs |
| **Accountability** | Clear data lineage: which data, from which shop, used for which model training or output |
| **Safety** | Confidence thresholds prevent agents from taking actions when certainty is below defined levels |

## E.4 Data Localisation

All Indian shop data is stored on Indian servers (AWS Mumbai / GCP Mumbai). No Indian shop data is processed or stored outside India. LLM inference for Indian shops routes through India-hosted API endpoints.

## E.5 Data Governance Framework

### Data Ownership

> **All shop data belongs to the shopkeeper.** Rupantar is a data fiduciary, not a data owner. This is not a policy — it is embedded in the architecture.

### Customer Data Rights

| Right | Mechanism |
|---|---|
| **Access** | Shop owner can request a summary of all data held via WhatsApp ("mera data dikao") |
| **Correction** | Data correction requests processed within 7 days |
| **Deletion** | Full account and data deletion within 30 days of request |
| **Portability** | Structured data export (JSON/CSV) available on demand |
| **Withdrawal of consent** | Consent for any data-sharing purpose can be withdrawn at any time; processing stops within 48 hours |

### Data Sharing Principles

- **Aggregated and anonymised only.** All shared data (brand intelligence, NBFC credit scoring) is aggregated and anonymised. Individual shop or customer data is never sold or shared.
- **Explicit opt-in required.** Every data-sharing decision (brand intelligence, NBFC partnership) requires explicit shopkeeper opt-in.
- **Transparency.** Shop owners can see exactly what data is shared, with whom, and for what purpose.
- **Commercial fairness.** If data generates revenue for Rupantar (brand intelligence, NBFC commissions), the shopkeeper receives a share of that revenue or a corresponding service benefit.

### Consent Architecture

```
Level 0: Core agent functionality
  → Billing, inventory, credit — shop data processed by agents
  → Consent: implicit in service subscription

Level 1: Analytics and reporting
  → P&L insights, sales trends, stock recommendations
  → Consent: explicit opt-in (default: on at signup, can be turned off)

Level 2: Data products (brand intelligence)
  → Anonymised demand signals shared with FMCG brands
  → Consent: explicit opt-in (default: off, shop opts in for revenue share)

Level 3: Financial services
  → Transaction data shared with NBFC for credit scoring
  → Consent: explicit per-transaction opt-in (default: off)
```

## E.6 Industry Body Engagement Strategy

| Body | Purpose | Status |
|---|---|---|
| **IAMAI** (Internet and Mobile Association of India) | AI governance policy input; industry best practices | Planned — Phase 1 |
| **FICCI** (Federation of Indian Chambers of Commerce) | SMB digitisation policy; retail sector advocacy | Planned — Phase 1 |
| **MeitY** (Ministry of Electronics and IT) | Startup advisory panel; AI regulation input | Planned — Phase 2 |
| **RBI Innovation Hub** | Fintech partnership framework; NBFC engagement | Planned — Phase 2 |
| **NPCI** (National Payments Corporation of India) | UPI integration; payment data standards | Planned — Phase 1 |

Proactive engagement with regulators and industry bodies ensures Rupantar shapes emerging rules rather than being surprised by them.

---

**March 2026 | Confidential**
