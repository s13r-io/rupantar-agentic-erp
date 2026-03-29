# Rupantar AI — Appendices

## Reference Material for Meeting Discussion

**March 2026 | Confidential**

---

# Appendix A: Full Vertical Deep Dives (All 20)

*Source for all figures and narrative in this appendix: `docs/Rupantar_AI_Master_Proposal.md`, Part 2 — Market Landscape (summary table lines 41–62; vertical sections lines 66–555).*

---

### A.01 — Billing & POS

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~50M** addressable | **15–20%** | Tally **38%**, Vyapar **13%**, Marg **11%**, Busy **9%**, MyBillBook **7%** (est. share among software users) |

**Market Reality**  
Tally's dominance is accountant-driven, not shopkeeper-driven. Vyapar and MyBillBook have traction on mobile but still require a UI interaction for every bill. **80%+** of India's shops remain on paper because no product meets them via voice in their own language.

**What we build**  
**Voice-first Billing Agent** — shopkeeper speaks an order in Hindi/Hinglish; the agent generates a GST-compliant bill, identifies the customer, applies pending discounts or credit, and sends it via WhatsApp, with zero screen interaction for the owner.

**Key agent features**

- **Voice Billing:** Parses spoken orders (Hindi/Hinglish/regional) into structured bills — local aliases, unit variations, combo deals
- **Smart Scan:** Photo or barcode → auto-identifies SKU, fetches price, adds to bill
- **Customer Memory:** Recognises returning customers by phone or UPI ID — saved price, outstanding credit, preferred items
- **GST Engine:** HSN/tax slabs, e-invoice for B2B above threshold, validation before print
- **Day Close Agent:** End-of-day cash + UPI + credit tally, discrepancy flags, ledger post, WhatsApp summary
- **Offline Sync:** Queue during outage; sync with conflict resolution when online

---

### A.02 — Inventory

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~50M** addressable (**10–15M** with meaningful stock) | **8–12%** (bundled with POS) | Marg ERP, GoFrugal, Tally — bundled; **no standalone SMB inventory product** |

**Market Reality**  
Owners discover stockouts when the customer asks. Inventory is on paper or memory. The opportunity is to make stockouts predictable **3–5 days** ahead and auto-resolve them without heavy owner action.

**What we build**  
**Autonomous Stock Intelligence Agent** — monitors inventory from every sale, predicts stockouts using velocity and seasonality, auto-generates purchase orders confirmed with a single WhatsApp “haan.”

**Key agent features**

- **Live Stock Tracker:** Deducts on sale; loose weight, variants (size/colour), combo packs
- **Stockout Predictor:** **90-day** velocity + festival calendar + local events → SKUs at risk in **3–5 days**
- **Auto-Reorder:** PO to preferred supplier at reorder level; WhatsApp routing; one-reply approval
- **Expiry Watchdog:** Batch expiry; **30 / 15 / 7**-day alerts; markdown or return suggestions
- **Shrinkage Detective:** Expected vs counted after cycle count — theft, breakage, measurement error
- **New Product Intake:** Photo of delivery → vision extraction, catalogue entry, suggested price

---

### A.03 — Accounting & GST

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~10M** shops with GST registration | **18–22%** (GST filing software) | Tally **47%**, Busy **11%**, Zoho Books **7%**, ClearTax **6%**, Vyapar **5%** |

**Market Reality**  
Tally dominates because CAs use it. Many small shops pay a CA **₹5,000–15,000/year** for manual GST work. The opportunity is auto-books from every transaction and auto-filed returns, shrinking routine CA dependency.

**What we build**  
**Autonomous Compliance Agent** — posts transactions to ledgers, prepares GSTR-1 and GSTR-3B, reconciles purchases, files after one owner confirmation; monthly plain-Hindi P&L via WhatsApp voice note.

**Key agent features**

- **Auto-Bookkeeper:** Sale, purchase, expense auto-post from billing/payment — zero manual entry
- **GST Filing Agent:** GSTR-1 + GSTR-3B; GSTR-2A reconcile; mismatch flags; one WhatsApp approval to file
- **e-Way Bill Agent:** Above **₹50K** movement — generate from PO, monitor expiry
- **Expense Capture:** Receipt photo → amount, vendor, date, expense head
- **P&L Narrator:** Monthly **~60-second** Hindi voice summary of profit, GST, etc.
- **Deadline Agent:** **7 / 3 / 1**-day reminders with ready-to-file vs data-missing status

---

### A.04 — Digital Payments

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~50M** shops accepting digital payments | **60–70%** | Paytm **30%**, PhonePe **30%**, BharatPe **12%**, Google Pay **10%**, Pine Labs (POS terminals) |

**Market Reality**  
UPI acceptance is largely solved — soundboxes reach many vendors. The gap is reconciliation and cash-flow intelligence: who paid, follow-ups on unpaid balances, forecasts. A new acceptance layer vs UPI giants is not the play.

**What we build**  
**Payment Intelligence Layer** — reconciliation and cash-flow on top of existing UPI: match credits to orders, follow up on unpaid amounts, forecast **next 14-day** cash position.

**Key agent features**

- **Payment Reconciler:** UPI SMS/webhook → match credit to order or customer
- **Collection Agent:** Personalised WhatsApp reminders (timing, escalation by days overdue)
- **Cash Flow Forecast:** **14 / 30-day** projections from collections, supplier dues, recurring expenses
- **Fraud Flag:** Fake screenshots, duplicate IDs, screen-recorded confirmations before goods release
- **Day Settlement:** Cash + UPI vs expected; over/short; surplus transfer option

---

### A.05 — Credit Ledger

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~25–30M** credit-extending shops | **20–30%** digital khata | Khatabook **40%**, OkCredit **25%**, Vyapar **20%** (free tiers; weak monetisation per proposal) |

**Market Reality**  
Khatabook and OkCredit raised **$275M+** combined (per proposal) without strong monetisation because a free digital ledger alone lacks stickiness. An AI layer turns khata into an active collection engine worth paying for.

**What we build**  
**Intelligent Credit Agent** — voice credit entry, smart WhatsApp reminders, credit profiles, and path to working-capital connectivity.

**Key agent features**

- **Voice Credit Entry:** e.g. “Ram ne 500 liya” → recorded, timestamped, linked to profile
- **Smart Reminder:** Timing by pay cycle; tone adapts to days overdue
- **Pattern Analyser:** Learns when each customer pays; schedules reminders
- **Credit Limit Advisor:** Flags unsafe exposure from history and frequency
- **Early Warning:** Deteriorating payment behaviour before bad debt
- **Loan Connector:** **6-month** history → score → NBFC pre-approved working capital

---

### A.06 — Restaurant F&B

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~7.5M** food service establishments | **5–8%** (**~400–600K**) | Petpooja **45%** of software users (**1L+** outlets), Posist/Restroworks **10%**, Rista/DotPe **8%** |

**Market Reality**  
Petpooja has SMB coverage around **₹10K/year**. The opportunity extends to co-manager behaviour: KOT prioritisation, Swiggy/Zomato reconciliation, predictive inventory-to-menu. **6.5M+** dhabas and tea stalls remain unaddressed.

**What we build**  
**Restaurant Co-Manager Agent** — multi-channel orders, kitchen queue by prep time, daily aggregator reconciliation, morning brief on operations and prep.

**Key agent features**

- **Multi-Channel Order Hub:** Counter, Swiggy, Zomato, WhatsApp, QR — kitchen queue by prep time, not FIFO
- **Kitchen Intelligence:** Station routing, batching, ready-time estimates, server alerts
- **Aggregator Reconciler:** Daily expected vs paid; commission discrepancies; dispute raises
- **Menu Engineer:** Weekly high/low profit-effort dish insights; pricing/menu suggestions
- **86 Manager:** Inventory vs menu — mark unavailable across channels when ingredients out
- **Morning Brief:** Yesterday revenue, top dishes, delivery ratings, today’s prep list

---

### A.07 — Pharmacy

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~1.2M** registered chemists + **~300K** unregistered | **30–40%** | Marg **38%**, GoFrugal **13%**, Pharmsoft **9%**, hCue **5%**, eVitalRx **4%** |

**Market Reality**  
High penetration driven by regulatory complexity (Schedule H, expiry, licences). The add-on layer is clinical safety (interactions), proactive patient management, and **ABDM (Ayushman Bharat)** integration.

**What we build**  
**Pharmacy Intelligence Agent** — billing/compliance plus prescription reading, interaction checks, chronic refill reminders **5 days** before run-out.

**Key agent features**

- **Prescription Reader:** Photo → drugs/doses; cross-check; brand-to-generic consent flags
- **Drug Interaction Check:** Multi-drug vs interaction database before dispensing
- **Expiry Action Agent:** **30 days** → return/markdown; **7 days** → donation/disposal alert
- **Chronic Refill Agent:** BP/diabetes/thyroid — reminder **5 days** before run-out; reorder by reply
- **Auto-Procurement:** Velocity + stock → daily PO to distributor via WhatsApp
- **ABDM Connector:** ABHA-linked records; digital prescription pull; compliance readiness

---

### A.08 — Salon & Spa

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~2M** salons and beauty parlours | **3–5%** (**~60–100K**) | Zenoti (premium chains), Dingg (Indian SMB, **~8K**), MioSalon (**~10K**), Invoay |

**Market Reality**  
**~95%** of neighbourhood salons use paper appointments, WhatsApp bookings, and recall for preferences. The agent scales the owner’s personal memory so client experience survives staff turnover.

**What we build**  
**Client Memory & Revenue Agent** — bookings via WhatsApp/voice, service history and colour formulas, empty-slot outreach, staff commissions without spreadsheets.

**Key agent features**

- **Booking Agent:** WhatsApp, voice, Instagram DM — availability, confirm, **24 hr** reminder, reschedule
- **Client Memory:** History, colour formulas, stylist preference, skin/hair type, product prefs
- **Empty Slot Filler:** Gaps → personalised outreach (e.g. due-for-visit prompts)
- **Staff Commission Tracker:** Daily/monthly by services, products, tips → payslip
- **Review Generator:** Post-service WhatsApp for Google/Justdial review; guided flow; discount hook

---

### A.09 — B2B Procurement

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~15M+** shops restocking from distributors | **5–8%** | Udaan (dominant; **₹5,706 Cr** revenue FY24 per proposal; acquired ShopKirana Jul 2025), Ninjacart (agri), Jumbotail (South) |

**Market Reality**  
**~85%** of FMCG procurement is traditional distribution (salesman, phone, paper). Udaan scaled B2B e-commerce but in-store procurement intelligence for the shop remains under-served.

**What we build**  
**Smart Procurement Agent** — monitors stock, orders from best-priced distributor before stockout; trade schemes; delivery disputes; multi-supplier credit limits.

**Key agent features**

- **Smart Ordering:** PO from velocity, events, credit — route to best-priced distributor
- **Delivery Verification:** Received vs PO before delivery person leaves — shortages, wrong items, damage
- **Supplier Invoice Checker:** Invoice vs PO and delivery note — qty, rate, scheme discrepancies
- **Trade Scheme Tracker:** Buy-X-get-Y and similar — maximise benefit before expiry
- **Credit Manager:** Per-distributor limit and outstanding — alerts before exhaustion

---

### A.10 — Online Store

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~5–7M** attempting online sales | **5–7%** active online stores | Shopify (D2C), Dukaan (**~3M** registered), Bikayi (**~5L**), ONDC-native apps |

**Market Reality**  
Many SMBs abandon online within **~60 days** — stale catalog, missed orders, unanswered queries. The agent makes the channel low-effort: sync, **24/7** queries, order handling, promotions from excess stock.

**What we build**  
**Online Store Manager Agent** — sync offline catalog to ONDC/WhatsApp catalog/Dukaan; answers queries; processes orders; targeted promos from excess stock.

**Key agent features**

- **Catalog Sync:** Real-time mirror; OOS when physical zero; price updates
- **24/7 Query Agent:** WhatsApp, web chat, Instagram — stock/size/delivery/return without owner
- **Order Processor:** Confirm, acknowledge, courier, label, track — owner only on exceptions
- **Promo Campaign Agent:** Weekly promos from excess stock and local events; WhatsApp broadcast content
- **ONDC Agent:** Listings, catalog, ratings, order lifecycle on buyer apps

---

### A.11 — Fashion

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~4–5M** garment shops | **5–8%** (mostly chains) | Ginesys (chains), Logic ERP (**~5K** SME), Unicommerce (online) |

**Market Reality**  
Core pain is size-colour matrix (**12–40** variants per design). No affordable matrix product for standalone shops under **₹25,000/year** per proposal; dead season-end stock hits margins.

**What we build**  
**Fashion Intelligence Agent** — variant-level matrix; dead-stock alerts **3 weeks** before season end; markdowns; next-season buying from sell-through.

**Key agent features**

- **Matrix Tracker:** Style × size × colour — low vs overstocked combinations
- **Dead Stock Alert:** Unsold **14 / 21 / 30** days — markdown timing before season-end
- **Season Buying Advisor:** Prior season sell-through by category/price → next-cycle quantities
- **Bundle Optimizer:** Basket analysis → combos to move slow companions
- **Returns Analyser:** Returns by supplier/style — defect-rate flags for sourcing

---

### A.12 — Electronics Repair

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~4–5M** mobile/electronics repair shops | **<3%** IMEI-specific | **No clear SMB leader** — Marg/Tally for billing only; no job-card/IMEI product per proposal |

**Market Reality**  
**~4 lakh** mobile repair shops (per proposal wording) on handwritten job cards; no durable digital record of repairs, parts, or returns. White space with no dominant incumbent.

**What we build**  
**Mobile Repair OS** — customer WhatsApps damage photo; digital job card, device ID, repair tracking, parts, stage updates — workflow via WhatsApp.

**Key agent features**

- **Job Card Creator:** Photo → make/model, fault, numbered work order, acknowledgment
- **IMEI Verifier:** Stolen-device check before accept; device history
- **Parts Inventory:** By model compatibility; low-stock alerts; distributor orders
- **Status Communicator:** received → diagnosed → parts ordered → ready — WhatsApp at each stage
- **Repair Estimate Agent:** Fault description → price range from historical model/fault data
- **Warranty Handler:** Brand warranty guidance and service-centre tracking

---

### A.13 — Kirana Store OS

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~12M** kirana stores | **8–12%** any software | Vyapar (billing), Khatabook (ledger), Udaan (supply) — point solutions; **no integrated OS** per proposal |

**Market Reality**  
Typical kirana: single owner, **5,000–20,000** SKUs, **50–200** credit customers, **₹15,000–50,000** daily revenue, no computer. Product must minimise behaviour change — **WhatsApp voice**-first.

**What we build**  
**Zero-UI Kirana OS** — full ERP through one WhatsApp number: billing, khata, stock, ordering, delivery coordination, daily report — voice and WhatsApp only.

**Key agent features**

- **WhatsApp Command Centre:** Voice notes and chat for transactions and invoices
- **Delivery Coordinator:** Home delivery — confirm, slot, customer status
- **Customer Relationship Memory:** Patterns, credit, usual items — personalised interactions
- **Festival Stock Agent:** **3–4 weeks** before major festivals — suggested quantities from prior year
- **Micro-Lending Connector:** **6–12 months** data → credit report → NBFC **₹50K–5L**
- **Evening Report:** **~60-second** Hindi voice — sales, credit, top SKUs, cash, tomorrow’s orders

---

### A.14 — HR & Payroll

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~3–5M** shops with **5+** paid staff | **5–8%** of shops with **10+** employees | GreytHR (**~25K** companies), Keka (**5K+**), Kredily (**20K+**, free tier), Razorpay Payroll |

**Market Reality**  
For **5–50** staff shops: paper attendance, informal salary math, sporadic PF compliance. Agent makes attendance and payroll ambient — WhatsApp check-in, auto payslip, PF challan automation.

**What we build**  
**Invisible HR Agent** — attendance, payroll, compliance in background; owner sees approvals and anomalies; salary disbursement via UPI on pay day.

**Key agent features**

- **Smart Attendance:** WhatsApp, QR, or face scan — late, half-day, overtime
- **Payroll Calculator:** Base, allowances, PF/ESI/TDS, advances — Hindi payslip
- **Salary Disbursement:** Pay-day UPI to each staff; receipt confirm; failure flags
- **PF/ESI Filing:** Monthly ECR/ESIC with digital signature — minimal manual work
- **Compliance Calendar:** Labour deadlines — min wage, bonus, annual returns — advance warnings

---

### A.15 — Customer Loyalty CRM

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~50M** shops with repeat customers | **<2%** | Reelo (F&B), WhatsApp Business broadcasts (informal), Capillary (enterprise) |

**Market Reality**  
Shopkeepers excel at personal loyalty but scale breaks past **100–200** customers. The agent extends that warmth to **1,000+** customers with timed, personal outreach.

**What we build**  
**Hyper-Personalisation Agent** — profiles from transactions; right-moment outreach; repeat visits via personal (not generic) messages.

**Key agent features**

- **Customer 360:** History, preferences, price sensitivity, payment habits
- **Intelligent Outreach:** Per-customer timing (e.g. usual Friday order → Friday morning nudge)
- **Birthday/Occasion Agent:** Offers on actual favourite products
- **Win-Back Agent:** Missed usual cycle → personalised “we miss you” + relevant offer
- **Referral Engine:** Post-positive interaction — code, reward chain, auto-credit
- **Campaign Analyst:** Uplift vs baseline by segment — feeds next campaigns

---

### A.16 — Logistics

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~5–8M** shops doing home delivery | **3–5%** | Shiprocket/Delhivery (e-commerce, organised); **hyperlocal neighbourhood manual** per proposal |

**Market Reality**  
Most neighbourhood delivery is WhatsApp calls and informal riders — no tracking; “where is my order?” unanswered. Agent adds professional delivery ops **without a new customer app**.

**What we build**  
**Hyperlocal Delivery Agent** — assign by proximity; WhatsApp live tracking link; multi-drop routes; failed-delivery rescheduling.

**Key agent features**

- **Smart Assignment:** By location, pending orders, zone familiarity
- **WhatsApp Tracking:** Live link — pickup, en route, delivered updates
- **Route Optimizer:** **5–10** simultaneous orders — sequence by address/traffic
- **Failed Delivery Handler:** WhatsApp customer contact; alternatives; same-day reschedule
- **COD Tracker:** Undeposited COD per rider; overdue flags; daily collection report

---

### A.17 — WhatsApp Commerce

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~50M** (WhatsApp universal) | **20–30%** informal; **API layer <2%** | WhatsApp Business free (**50M+** Indian business users per proposal); Interakt, AiSensy, Wati.io (API) |

**Market Reality**  
WhatsApp is India’s de facto commerce channel informally. AI converts it into an autonomous channel: catalog, order, payment, tracking, support — automated, in the customer’s language.

**What we build**  
**Full-Stack WhatsApp Commerce Agent** — catalog, voice-note orders, payment, tracking, support — Hindi/Hinglish/regional, **24/7**.

**Key agent features**

- **Conversational Catalog:** Natural-language browse with photos, prices, availability
- **Voice Order Agent:** Voice notes → transcribe, intent, confirm in natural language
- **Multilingual Agent:** Auto-detect Hindi, Tamil, Telugu, Marathi, Bengali — respond in kind
- **Automated FAQ:** **~90%** of common queries without owner
- **WhatsApp Payment:** UPI link post-confirm → receipt → paid → fulfillment
- **Broadcast Manager:** Segment, personalise, send time, open tracking

---

### A.18 — Auto Garage

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~5M** workshops and garages | **<1%** | **No clear leader**; Workshop360, GarageKey early stage **<500** active garages each per proposal |

**Market Reality**  
**5 million** garages (per proposal) on memory, handwritten job cards, calls — no durable vehicle history, parts tracking, or customer comms system. Large latent demand, weak incumbent set.

**What we build**  
**Garage OS** — vehicle photo or problem description → digital job card, progress, parts, milestone WhatsApp updates, billing — minimal paperwork.

**Key agent features**

- **Digital Job Card:** Photo → OCR registration, make/model, issue, work order
- **Fault Diagnosis Assistant:** Voice symptoms → fault database suggestions by make/model
- **Parts Ordering:** Identify spares; local supplier WhatsApp; order and ETA tracking
- **Customer Update Agent:** Milestones — received, diagnosed, parts ordered, under repair, ready
- **Vehicle History Keeper:** Full service record per registration on return visits
- **Workshop Capacity Manager:** Active vs waiting — realistic completion dates

---

### A.19 — Hardware Retail

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~2–3M** hardware / building material shops | **<5%** | Tally (generic accounting); **no dedicated affordable SMB hardware product** per proposal |

**Market Reality**  
Pricing varies by relationship (contractor vs retail), quantity, and payment mode. Multi-site contractor orders on credit exceed what generic accounting handles without custom work.

**What we build**  
**Contractor Relationship Agent** — contractor price books, multi-site outstanding, daily challans, itemised site-wise billing.

**Key agent features**

- **Dynamic Rate Card:** Contractor-specific negotiated rates vs walk-in MRP
- **Site-wise Tracker:** Deliveries per construction site per project — billing and disputes
- **Contractor Credit Manager:** Outstanding across sites; monthly statements; limit alerts
- **Purchase Bill Digitiser:** Supplier invoice photo → line items, qty, rates, GST → books
- **Material Calculator:** Task description → material quantities and quote

---

### A.20 — Education & Coaching

| Addressable Shops | Current Penetration | Existing Leaders |
|---|---|---|
| **~3M** coaching centres + **7–8M** solo tutors | **10–15%** organised centres; **<1%** solo tutors | ClassPlus, Teachmint/Extramarks, SimpliFee (micro-tutors), Fedena (school ERP) |

**Market Reality**  
Organised coaching is relatively served. White space: **7–8M** solo/small tutors — cash fees, manual registers, WhatsApp groups. A **₹199/month**-class tool (per proposal) for reminders and parent comms could scale widely.

**What we build**  
**Tutor OS** — fees, attendance, parent comms, progress via WhatsApp; tutor sends marks to agent; agent reports to parents — no separate parent/student app required.

**Key agent features**

- **Fee Collection Agent:** Monthly reminders, receipt on payment, overdue by student, tutor report
- **Attendance Tracker:** WhatsApp/location marks; register; absent alerts to parents
- **Parent Broadcast:** Homework, tests, schedule changes to correct groups
- **Progress Report Agent:** Marks via voice/text → scorecards → monthly parent report in simple language
- **Enrollment Agent:** Prospect on WhatsApp → qualify, demo scheduling, follow-up for conversion

---

### Appendix A — Document source

| Claim domain | Primary source |
|---|---|
| Penetration bands, leader shares, addressable counts, agent names, feature bullets | `Rupantar_AI_Master_Proposal.md`, Part 2 (lines 37–555) |
| B2B leader revenue / M&A note | Same file, Area 09 table (lines 268–270) |
| Khatabook + OkCredit funding context (Appendix A.05 cross-ref) | Same file, Part 5 (line 627) — used only where proposal repeats figure |

---

# Appendix B: Partner Programme Detail

*Source: `docs/Rupantar_AI_Master_Proposal.md`, Part 5 (lines 625–666) and Part 6 (lines 669–684).*

---

### B.1 Partner tier structure (T0–T4)

| Tier | Name | Entry criteria | Shop portfolio | Technical capability | Revenue earning |
|---|---|---|---|---|---|
| **T0** | Referral Agent | Register on app; **2-hr** intro module | Refers only; no deployment | None required | **₹200** one-time per referred shop that **activates** |
| **T1** | AI Shop Starter | **2-day** certified training; **50-question** assessment; **5 deployments** within **60 days** | **5–25** active shops | Standard bundles from library; **no** custom flows | **15%** recurring commission + **₹500** per new activation |
| **T2** | AI Shop Builder | T1 + **3-day** Builder training + visual flow certification; **25+** active shops | **25–150** active shops | Custom flows (visual builder); multi-agent configs | **22%** recurring + **₹1,000** per activation + **own-priced** customisation fees |
| **T3** | AI Shop Architect | T2 + Pro Code certification; **150+** shops; **3** community templates rated **4+** | **150–500** active shops | Custom agent nodes (Python/JS); vertical solutions; trains T1/T2 | **30%** recurring + **₹2,000** per activation + **template marketplace royalties** |
| **T4** | Regional Master | Invite only; **10+** sub-partners; **500+** network shops; **₹25L** annual revenue | **500+** shops across sub-partner network | Full platform access; runs training; co-develops verticals with Rupantar | **35%** own shops + **5%** **override** on sub-partner revenue + **equity discussion** |

**Source:** Part 5, Partner Tier Structure table (lines 648–654).

---

### B.2 Partner income model — streams and worked example (T2, 100 shops)

| Income stream | Mechanism | Example (T2 partner, **100** active shops) |
|---|---|---|
| **Subscription commission (recurring)** | **22%** of each shop’s monthly subscription while active | **100 × ₹599 × 22% = ₹13,178/month** recurring |
| **New activation fee** | **₹1,000** per shop live with **first week** of active agent usage | **20** new shops/month × **₹1,000 = ₹20,000/month** |
| **Customisation fees** | Partner sets price for custom flows; **0%** platform take | **5 × ₹5,000 = ₹25,000/month** |
| **Template royalties** | **₹50–₹200** per deployment when others use a published template | **2** templates × **100** deployments × **₹100 = ₹20,000/month** |
| **AMC (annual maintenance contract)** | Partner offers **₹3,000–₹8,000/year** per shop; **0%** platform take | **30** shops × **₹5,000/yr → ₹12,500/month** equivalent |
| **Total (illustrative)** | Sum of above example lines | **~₹90,000/month gross**; proposal notes scale toward **₹1.5–2L/month** at **200** shops |

**Source:** Part 5, Partner Income Model table (lines 658–665).

---

### B.3 Training curriculum (M0–M7)

| Module | Duration | Format | Content | Required for |
|---|---|---|---|---|
| **M0:** AI Basics for Shop Doctors | **3 hours** | Video + mobile quiz | Agents vs apps; WhatsApp-native agents; shop need; explain value in **2 minutes** without saying “AI” | **All tiers** — before any deployment |
| **M1:** Shop Pain Discovery | **4 hours** | Role-play + facilitator | **15-question** pain interview; map pain to agent type; first wins; objections (complexity, existing Tally, connectivity) | **T1+** |
| **M2:** Standard Bundle Deployment | **6 hours** | Hands-on lab (sandbox) | Partner app onboarding; **5** starter bundles (Kirana OS, Restaurant, Pharmacy, Salon, Billing+Khata); WhatsApp number, catalog, language, tone | **T1+** |
| **M3:** Visual Flow Builder | **2 days (14 hours)** | Workshop + lab | Builder UI; trigger → logic → action; LLM prompts for shop context; test; deploy; error handling | **T2+** |
| **M4:** Vertical Specialisation (pick **1–3**) | **1 day** each | Vertical deep-dive | Pharmacy: compliance + ABDM; Restaurant: aggregator reconciliation; Fashion: matrix inventory; Garage: job card + parts; Hardware: rate card + contractor billing | **T2+** |
| **M5:** Portfolio Management | **4 hours** | Dashboard + mentorship | Health dashboard; upsell signals; agent failures; monthly shop review; referrals (**5 → 50** word-of-mouth) | **T2+** |
| **M6:** Pro Code SDK | **3 days** | Developer workshop (Python/JS) | Custom nodes; marketplace publish; non-standard APIs; community template guidelines | **T3+** |
| **M7:** Train the Trainer | **2 days** | Train-the-trainer | Local T1 certification; quality assessment; sub-partner network; regional GTM | **T4 only** |

**Source:** Part 6, training table (lines 673–682). Delivery note from proposal: Hindi + regional languages, mobile-first, simulation-heavy (lines 671–672).

---

### B.4 Certification requirements

Certification is **practical**, not exam-only. **T1** requires **5 live shops** deployed with **Shop Health Score >70%**. **T2** requires building and deploying **one custom flow**. **T3** requires publishing **one community template** with **10+** deployments. The design intent is competent operators, not certificate-only completion.

**Source:** Part 6, certification model block (line 684).

---

### Appendix B — Document source

| Section | Lines in `Rupantar_AI_Master_Proposal.md` |
|---|---|
| Partner problem statement, field-force table, **2%** conversion target | 625–644 |
| Tier structure | 648–654 |
| Income model + T2 example | 656–665 |
| Training philosophy + M0–M7 + certification | 669–684 |

---

# Appendix C: Unit Economics (All Scenarios)

**Purpose:** Reference for chairman discussion — stabilised per-shop economics (Year 2+), revenue composition, sensitivity levers, and external benchmarks. Figures below trace to `Rupantar_AI_Master_Proposal.md` Part 8 unless noted.

## C.1 Per-shop unit economics — three scenarios (full row set)

| Metric | Conservative | Base case | Optimistic |
| --- | --- | --- | --- |
| Average monthly subscription | **₹399** | **₹599** | **₹899** |
| Partner commission (avg **22%**) | **₹88** | **₹132** | **₹198** |
| Net revenue to Rupantar | **₹311** | **₹467** | **₹701** |
| Cloud / LLM / API cost per shop | **₹80** | **₹100** | **₹130** |
| Gross profit per shop per month | **₹231** | **₹367** | **₹571** |
| Gross margin % | **~58%** | **~61%** | **~64%** |
| Customer acquisition cost (partner model) | **₹800** | **₹600** | **₹400** |
| Payback period | **3.5** months | **1.6** months | **0.7** months |
| **12-month LTV** (net of commissions + COGS) | **₹2,772** | **₹4,404** | **₹6,852** |
| **LTV / CAC** | **3.5×** | **7.3×** | **17.1×** |

**Context (sourced):** Master proposal notes direct, app-based SMB SaaS CAC **₹1,500–₹3,000** vs partner-model CAC **₹400–₹800**; shops with a dedicated implementation partner churn **~70% less** than self-service users (benchmark framed as Tally TDP-supported vs Vyapar self-serve in master proposal).

---

## C.2 Sensitivity analysis (key variables)

Illustrative ranges holding other assumptions steady; use for scenario planning, not as forecasts.

| Variable | Range tested | Impact on gross margin | Impact on LTV / CAC |
| --- | --- | --- | --- |
| Average subscription | **₹299**–**₹899**/mo | **58%**–**64%** | **3.5×**–**17.1×** |
| Partner commission | **15%**–**35%** | Drops **~3 pp** per **+5 pp** commission | LTV drops **~15%** per **+5 pp** commission increase |
| Cloud / LLM cost per shop | **₹50**–**₹200**/mo | **54%**–**66%** | **2.8×**–**20×** |
| Monthly churn rate | **5%**–**15%** | Minimal direct (margin on remaining base) | LTV drops **40%+** at **15%** vs **5%** |
| Activation cost per shop | **₹300**–**₹1,200** | No impact on gross margin | CAC band directly sets payback; higher CAC compresses LTV/CAC |

---

## C.3 Revenue streams — model, net take, activation timeline

| Revenue stream | Model | Rupantar net (after partner / variable costs) | Activation timeline |
| --- | --- | --- | --- |
| Shop subscription (SaaS) | **₹299–₹1,499**/mo per shop by vertical + agent count | **~75–85%** net after partner commission | **Phase 0+** — core from first paid shops |
| Agent Builder platform fee | **₹0** Tier 1 (earn-only); **₹999**/mo Tier 2+ builders | **100%** — no partner cut on platform fee | **Phase 1–2** — as builder tiers and certification scale |
| Marketplace royalties | Rupantar **30%** / author **70%** per community template deployment | **30%** of marketplace revenue | After marketplace + community template volume |
| Vertical add-on modules | Premium agents with external API cost (e.g. ABDM, GST e-invoice, aggregator reconciliation) | **~60–70%** gross margin after API costs | Rolling — per module GA and partner attach |
| B2B intelligence layer | Aggregated, anonymised market signals to FMCG / banks | **100%** (second-order; no partner share on this line) | After **1L+** active shops (per master proposal gating) |
| Embedded financial services | Working capital, insurance, BNPL via NBFC partners; commission on disbursals | **0.5–2%** referral on disbursals | After **6–12 months** transaction history + NBFC integrations *(aligned to full proposal financial-services gating)* |

**Source:** Revenue stream definitions and percentages — `Rupantar_AI_Master_Proposal.md` Part 8 (Revenue Streams table).

---

## C.4 Comparable benchmarks (external analogues)

| Analogue | Economics / pricing signal | Source / basis in Rupantar docs |
| --- | --- | --- |
| **Tally TDP channel** | Ecosystem-scale revenue **~₹900 Cr** with **~50K** partner footprint — proof of reseller-led SMB attach at national scale | Cited in `Rupantar_AI_Full_Proposal.md` appendix as **Tally Solutions public financials**; same figures in executive materials |
| **Zoho** | Profitable India-headquartered SaaS at scale; partner / consulting economics support enterprise and mid-market — **not** a micro-SMB field-certification layer at **50M**-shop granularity | Qualitative benchmark in master proposal “comparable channel programme” note; competitive positioning in full proposal |
| **Fintech DSA structures** | **~3M+** bank DSAs in India — recurring, activity-linked income for distribution of regulated products; validates “earn on portfolio” field economics | Field-force sizing — `Rupantar_AI_Full_Proposal.md` (Existing Field Force table); economics described as benchmark class in master proposal data note |
| **Petpooja (restaurant vertical)** | Typical SaaS band **~₹10K/yr** for POS / restaurant stack — vertical SaaS pricing anchor for India SMB | `Rupantar_AI_Full_Proposal.md` competitive / market tables |

**Narrative:** These analogues do not forecast Rupantar’s outcome; they show that **partner-paid CAC**, **subscription ARPU in the hundreds–low thousands per month**, and **vertical SaaS annual pricing ~₹10K** are already established in India. Rupantar’s differentiation is WhatsApp-native, voice-first delivery and partner income tied to **operational** agents, not a claim of uniqueness in “having a channel.”

---

# Appendix D: Competitive Response Playbook

**Purpose:** Structured reference for “what if they move?” — per-competitor moves, structural constraints, and Rupantar responses. Grounded in `Rupantar_AI_Reframed_Objective_Risks.md` §8 (competitive threats) and expanded per chairman briefing needs.

## D.1 Per-competitor analysis

| Competitor | What they could do | Why it’s structurally hard | What Rupantar does if they try |
| --- | --- | --- | --- |
| **Tally** | Add AI copilot to desktop / cloud accounting | **30-year** desktop product DNA; reseller base is **accounting-trained**, not WhatsApp **operations**-first; retrofitting conversational shop workflows ≠ feature bolt-on | Accelerate **AI Shop Doctor** certification and deployments in **overlapping cities**; win **workflow** proofs (voice billing, daily ops on chat) faster than accounting-centric AI can match |
| **Vyapar** | Add voice / WhatsApp features to app-led SMB product | **App-first** habit and GTM; **no** field partner income architecture comparable to recurring **per-shop** partner attach | Run **side-by-side** accuracy and time-to-value demos on **vernacular** voice; stress-test **partner economics** (partner earns on portfolio, not one-time app install) |
| **Zoho** | Deepen WhatsApp / messaging integrations across suite | **Screen-first**, enterprise-leaning DNA; lacks certified **micro-SMB field** layer at national **density** | **Double down** on **vernacular NLP** + **partner density** in **3–4** core verticals **before** a suite player can pivot GTM and UX |
| **Khatabook / OkCredit** | Expand from free/cheap ledger toward “full ERP” | **Free-product** culture; **$275M+** capital deployed **without** durable monetisation breakthrough at scale *(per executive / full proposal competitive narrative)* | **Convert** engaged users by proving **operational** value (inventory, credit discipline, GST-adjacent flows) **beyond** free ledger — partner-led onboarding reduces self-serve drop-off |
| **PhonePe** | Leverage merchant base for operational / software tools | **Payments** product org and DNA **≠** operations software; building ERP-grade agents cuts across different talent and roadmap | **Integrate** where possible — e.g. **payment reconciliation** intelligence using PhonePe rails — while owning **ops** layer on WhatsApp |
| **Google (Gemini)** | Ship India-specific retail AI surfaces | **No** India retail **field distribution**; weak incentive to build **20-vertical**, shop-grade agent templates | **Speed** to **50K+** partners and template library depth so Rupantar becomes the **distribution** partner a horizontal AI vendor would **route through**, not replace |
| **Reliance / Jio** | Deploy capital; reach **JioPhone** and mass consumer/merchant touchpoints | **Consumer** and connectivity focus **≠** merchant **operations** product depth | **Position** for **partnership** or **strategic combination** if their merchant agenda needs a ready ops-AI layer and certified field network |
| **Well-funded startup** | Copy WhatsApp + voice + partner model | **18-month** head start in **templates**, **partner contracts**, and **vertical** data flywheels — capital buys code, not overnight field trust | **Compound** **community template** moat + **partner income lock-in** faster than capital alone can recreate **trust + vernacular accuracy + portfolio economics** |

## D.2 Living-document note

This playbook is a **living document**, updated **quarterly** with competitive intelligence. The product roadmap retains **optionality** to pivot if a large entrant **fundamentally changes** market dynamics.

---

# Appendix E: Regulatory, Compliance & Data Governance Framework

**Purpose:** Show regulatory posture as **architectural**, not reactive — aligned with `Rupantar_AI_Reframed_Objective_Risks.md` §2 (mitigations: fiduciary, GSTN, auditable AI, localisation, industry engagement) and `Rupantar_AI_Deliverable_Structure.md` Appendix E outline.

## E.1 DPDP Act 2023 — compliance plan (summary)

| Requirement | How Rupantar complies |
| --- | --- |
| Data fiduciary obligations | Registered as **data fiduciary**; **Data Protection Officer (DPO)** appointed with board-visible accountability |
| Consent management | **Explicit opt-in** for collection; **granular** consent for any **sharing** or secondary use |
| Data principal rights | **Deletion**, **correction**, and **portability** supported in-product and via support workflows |
| Data processing limitations | Processing **limited to stated purpose**; **no** secondary use **without** fresh consent |
| Breach notification | **72-hour** notification pathway to **Data Protection Board** (and affected principals as required) upon confirmed breach |

*Note: Obligations apply as rules and Board procedures are notified; legal counsel to align templates and timelines to final subordinate legislation.*

## E.2 GST data handling

All **GST**-related data is processed in line with **GSTN** requirements. **Auto-filing** and e-filing actions run only with the **shopkeeper’s explicit approval**. **E-invoice** generation and transmission follow **GST Network** specifications and audit expectations.

## E.3 AI governance readiness

All **agent decisions** are **auditable**. **Confidence thresholds** block **autonomous** action on **high-stakes** operations (e.g. irreversible financial postings, statutory submissions) without human confirmation where policy requires. **Explainability:** agents **log reasoning traces** (tool calls, retrieved context, policy checks) per action so reviews and regulator-facing narratives are possible. Architecture stays compatible with **emerging** India **AI governance** norms as they crystallise.

## E.4 Data localisation

All **Indian shop and transaction data** reside on **servers in India**. **No cross-border transfer** of identifiable shop/transaction data **without** **explicit consent** and **regulatory** clearance where applicable.

## E.5 Data governance framework

| Principle | Implementation |
| --- | --- |
| Data ownership | All **shop data** belongs to the **shopkeeper**; Rupantar acts as **fiduciary**, not owner |
| Customer rights | **Deletion**, **consent withdrawal**, **portability** (DPDP-aligned) |
| Data sharing | Shared outputs are **aggregated** and **anonymised** where used for B2B intelligence; **raw** identifiable records **not sold** |
| Consent architecture | Every **sharing** decision (brands, NBFC scoring, third-party APIs) requires **explicit shopkeeper opt-in** |
| Audit trail | **Complete decision log** via **Langfuse** / **OpenTelemetry**-class pipelines; **48-hour** replay capability for investigations |

## E.6 Industry engagement strategy

**Membership** in **IAMAI** and **FICCI** committees (fintech / digital economy tracks as relevant); **participation** in **MeitY** startup and digital policy forums where appropriate; **proactive briefings** with **RBI innovation hub** and analogous regulatory sandboxes. **Rationale:** organisations that **engage early** help **shape** rules; those that defer face **surprise** enforcement and standard-setting driven by others.

---

*Confidential — chairman reference. Internal proposal appendices; figures trace to master proposal and risk/deliverable structure documents unless marked illustrative.*

---

*Data note: Market share figures are research-based estimates from public disclosures and industry reports (SaaSBoomi, KenResearch, Mordor Intelligence, MSME Ministry) as of early 2026. All figures are labelled as estimates.*

**March 2026 | Confidential**
