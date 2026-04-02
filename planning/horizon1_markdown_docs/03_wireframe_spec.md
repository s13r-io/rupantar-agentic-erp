# Screen-by-Screen Wireframe Spec
## Rupantar Horizon 1 Prototype — Kirana Ops

This is a **build-ready v1 wireframe spec**. It is intended for product, design, and engineering teams to translate the Horizon 1 blueprint into a concrete clickable prototype.

The prototype is optimized around:
- one vertical: **Kirana**
- one deployment model: **partner-led**
- one shopkeeper interface: **WhatsApp-like**
- one observer mode: **side-by-side explanation**
- one trust model: **confidence + approval + memory + audit**

---

# 0. Product framing

## Prototype name
**Rupantar Horizon 1 Prototype — Kirana Ops**

## Prototype purpose
Demonstrate that:
- a kirana owner can run common daily workflows through WhatsApp-like chat, voice notes, and photos
- a partner can configure and deploy the system quickly
- the system behaves like an operational assistant, not just a chatbot
- the product can be explained credibly to investors, internal stakeholders, and pilot partners

## Vertical for v1
**Kirana only**

## Agent bundle visible in observer/partner mode
- Orchestrator
- Billing
- Inventory
- Credit / Khata
- Procurement / Reorder
- Daily Summary
- Memory

## Role modes
- Shopkeeper
- Partner
- Observer
- Demo Operator / Admin

---

# 1. Global wireframe rules

## Devices
- **Desktop** for Observer, Partner, Admin: 1440 x 1024
- **Mobile frame** for Shopkeeper: 390 x 844 inside desktop shell for demos

## Language rules
- Observer and Partner screens: **English**
- Shopkeeper screens: **Hinglish by default**
- Optional switch for Hindi/English preview
- Tone should feel operational, not overly futuristic

## Core UX rules
1. The shopkeeper sees **one assistant identity**, not multiple bots.
2. Every monetary or stock-affecting action ends in one of three states:
   - auto-complete with confirmation
   - approval required
   - clarification needed
3. Every completed action writes to state:
   - bill state
   - inventory state
   - customer balance state
   - session log
4. Every important action produces a human-readable result card.
5. Partner actions must feel faster than traditional ERP onboarding.
6. Observer mode must make the invisible logic visible.

## Common labels used across the prototype
- “Sandbox”
- “Live”
- “Needs approval”
- “Clarification needed”
- “Low confidence”
- “Memory used”
- “Action completed”
- “Draft created”
- “Not sent yet”

## Confidence logic shown in UI
- **High confidence**: system can draft action immediately
- **Medium confidence**: system drafts, then asks for approval
- **Low confidence**: system asks clarification before drafting

---

# 2. Shared data model used by multiple screens

## Shop object
- `shop_id` — system string, auto-generated
- `shop_name` — text
- `owner_name` — text
- `phone_number` — Indian mobile number
- `city` — text
- `language` — enum: Hindi / Hinglish / English / Gujarati
- `vertical` — enum, fixed to Kirana in v1
- `gst_status` — enum: GST / Non-GST
- `business_hours` — text/time range
- `summary_time` — time
- `deployment_status` — enum: Draft / Sandbox / Live

## Product object
- `product_id` — system string
- `display_name` — text
- `aliases` — array of text
- `category` — enum
- `unit_type` — enum: piece / kg / gram / litre / loose
- `pack_size` — text
- `selling_price` — numeric
- `current_stock` — numeric
- `reorder_threshold` — numeric
- `reorder_quantity` — numeric
- `preferred_supplier_id` — relation

## Customer object
- `customer_id` — system string
- `display_name` — text
- `aliases` — array of text
- `phone_number` — optional
- `credit_enabled` — boolean
- `outstanding_balance` — numeric
- `reminder_after_days` — numeric
- `approval_limit_override` — optional numeric

## Supplier object
- `supplier_id` — system string
- `supplier_name` — text
- `phone_number` — text
- `categories_supplied` — array
- `lead_time_days` — numeric
- `preferred_for_products` — array of product_ids

## Interaction object
- `interaction_id` — system string
- `channel` — fixed as chat/voice/photo
- `raw_input` — text / media reference
- `parsed_intent` — text
- `confidence_score` — numeric or band
- `agents_called` — array
- `status` — completed / awaiting approval / clarification needed / failed

## Memory object
- `entity_type` — shop / customer / product / supplier
- `memory_key` — text
- `memory_value` — text
- `source` — config / learned / inferred
- `last_used_at` — timestamp

---

# 3. Screen map for v1

## Entry / observer
01. Landing / Role Selector  
02. Scenario Launcher  
03. Executive Overview  
04. Observer Live Demo Canvas  
05. Audit Trail & Replay Drawer  
06. Memory / Context Inspector  
07. Before vs After / ROI View  
08. Real vs Simulated Transparency Panel

## Partner
09. Partner Portfolio Home  
10. New Shop Wizard — Basic Details  
11. New Shop Wizard — Bundle Selection  
12. New Shop Wizard — Catalog Import  
13. New Shop Wizard — Customers & Khata  
14. New Shop Wizard — Suppliers & Reorder Rules  
15. New Shop Wizard — Language / Tone / Trust Rules  
16. Sandbox Test Lab  
17. Go Live Summary  
18. Shop Health Dashboard  
19. Edit Context & Memory  
20. Exception Queue  
21. Lite Rule Builder

## Shopkeeper
22. WhatsApp Chat Home  
23. Voice Note Review Sheet  
24. Bill Preview & Approval Card  
25. Stock Status & Reorder Card  
26. Payment / Khata Update Card  
27. Photo Extraction Preview  
28. Daily Summary Card  
29. Clarification / Fallback Card

## Internal / demo operator
30. Session Inspector  
31. Demo Reset & Seed Data Control

---

# 4. Shared layout patterns

## Pattern A — Desktop shell
Used on screens 01–21, 30–31.
- Top header
- Left nav or stepper
- Main content panel
- Optional right drawer
- Sticky footer for primary CTA

## Pattern B — Mobile chat frame
Used in screens 22–29 and embedded inside Observer Live Demo Canvas.
- Chat header
- Message stream
- Composer
- Context cards inserted in-thread
- Bottom action buttons

## Pattern C — Wizard shell
Used for 10–17.
- Title
- Stepper
- Main form
- Sticky footer: “Back” / “Save draft” / “Continue”

---

# 5. Screen-by-screen wireframe spec

## 01. Landing / Role Selector
**Role:** all  
**Device:** desktop  
**Purpose:** entry into the prototype

### Layout
- Top left: Rupantar logo
- Top right: “Reset demo data”
- Center hero block
- Below hero: 3 large role cards + 1 small admin card
- Footer: version text

### Exact UI content
**Hero title:**  
“Rupantar Horizon 1 Prototype”

**Hero subtitle:**  
“Kirana operations through WhatsApp + voice”

**Helper text:**  
“This prototype shows how a partner deploys a WhatsApp-native assistant for billing, inventory, khata, reorder, and daily summary.”

**Role cards**
1. **Shopkeeper**  
   “Use the assistant like a store owner would.”  
   CTA: “Enter as Shopkeeper”

2. **Partner**  
   “Configure and deploy a shop bundle.”  
   CTA: “Enter as Partner”

3. **Observer**  
   “See the live demo, internal logic, and business value.”  
   CTA: “Enter as Observer”

4. **Demo Operator**  
   “Reset scenarios and control test state.”  
   CTA: “Enter as Admin”

**Footer copy:**  
“Prototype scope: Kirana only · Horizon 1 · v1”

---

## 02. Scenario Launcher
**Role:** observer, admin  
**Device:** desktop  
**Purpose:** choose demo track quickly

### Exact UI content
**Page title:**  
“Choose a demo scenario”

**Scenario cards**
1. **Morning rush billing**  
   “Voice note → bill → stock update → khata update”  
   Badge: “3 min”

2. **Low stock + reorder**  
   “See inventory trigger a supplier draft”  
   Badge: “2 min”

3. **Payment received**  
   “Update khata and show balance change”  
   Badge: “90 sec”

4. **Supplier invoice photo**  
   “Photo → item extraction → stock update”  
   Badge: “2 min”

5. **Daily summary**  
   “Auto-generated summary at day end”  
   Badge: “90 sec”

6. **Ambiguous request / clarification**  
   “Show safe recovery when the assistant is unsure”  
   Badge: “2 min”

7. **Partner deploy new shop**  
   “Blank shop → configured → tested → live”  
   Badge: “5 min”

### Filters
- Audience
- Flow type
- Duration
- Happy path / edge case

---

## 03. Executive Overview
**Role:** observer  
**Device:** desktop  
**Purpose:** orient viewer before demo

### Exact UI content
**Title:**  
“What this prototype covers”

**Three columns**
1. **Shopkeeper experience**  
   “One WhatsApp-like assistant. Voice notes, photos, and simple approvals.”

2. **Partner deployment**  
   “A partner configures the shop bundle, loads context, tests flows, and goes live.”

3. **Internal intelligence**  
   “Observer mode reveals routing, confidence, memory, and audit trail.”

**What this proves**
- “A kirana owner can use a zero-UI workflow.”
- “A partner can configure the system without engineers.”
- “The system behaves like an operational agent, not a chatbot.”
- “Horizon 1 can start with a narrow wedge and still feel real.”

CTA:
- “Open Live Demo Canvas”

---

## 04. Observer Live Demo Canvas
**Role:** observer  
**Device:** desktop  
**Purpose:** main demo screen

### Layout
Three columns:
- **Left:** shop snapshot + partner snapshot
- **Center:** mobile chat frame
- **Right:** internal orchestration feed

### Exact UI content
**Header**
- Title: “Live Demo Canvas”
- Subheader: “Scenario: Morning rush billing”
- Buttons: “Switch scenario” / “Pause” / “Restart”

**Left column**
- Shop: Shree Ganesh Kirana
- Owner: Ramesh Patel
- City: Surat
- Language: Hinglish
- Status chip: Live

**Active bundle**
- Billing
- Inventory
- Khata
- Reorder
- Daily Summary
- Memory
- Orchestrator

**Today before this interaction**
- Sales today: ₹6,120
- Cash: ₹4,380
- Credit: ₹1,740
- Low-stock items: Sunflower Oil, Parle-G

**Right column**
Sample rows:
- “10:14 AM · Orchestrator · Detected: create bill + update khata + adjust stock · High”
- “10:14 AM · Billing Agent · Draft bill created · Medium”
- “10:14 AM · Memory Agent · Mapped ‘Ram’ → ‘Ram bhai’ · High”
- “10:15 AM · Approval Gate · Amount > ₹500 · Approval required”

Bottom toggles:
- Show raw input
- Show parsed intent
- Show memory usage
- Show business state changes

---

## 05. Audit Trail & Replay Drawer
**Role:** observer, admin  
**Device:** desktop drawer  
**Purpose:** explain what happened step-by-step

### Exact UI content
**Title:**  
“Audit trail”

**Helper text:**  
“Replay how the assistant interpreted the request, what it changed, and where approval was required.”

**Per-step fields**
- Step number
- Timestamp
- Raw input
- Intent detected
- Agents called
- Confidence
- Memory used
- Record changes
- User-visible output
- Final status

Buttons:
- Replay from start
- Jump to this step
- Download demo log
- Pin to canvas

---

## 06. Memory / Context Inspector
**Role:** observer, partner  
**Device:** desktop  
**Purpose:** show persistent context

### Exact UI content
**Title:**  
“Memory and context”

Tabs:
- Shop
- Customers
- Products
- Suppliers
- Learned patterns

Sample content:
- “Ram bhai usually buys on credit.”
- “Owner prefers Hinglish summaries.”
- “‘Tel’ is ambiguous: sunflower oil or groundnut oil.”
- “Sunflower oil threshold = 6 units.”
- “Summary delivery time = 9:00 PM.”

---

## 07. Before vs After / ROI View
**Role:** observer  
**Device:** desktop  
**Purpose:** convert demo into business value

### Exact UI content
**Title:**  
“Operational impact snapshot”

**Before**
- Billing on paper
- Stock checked manually
- Credit tracked in notebook
- No end-of-day summary
- Reorders depend on memory

**After**
- Bill drafted from voice
- Inventory updates automatically
- Khata updated in-thread
- Low stock surfaced before stockout
- Daily summary auto-generated

**Estimated value box**
- Time saved per bill: ~2–3 min
- Credit balance always visible: Yes
- Low-stock items caught today: 2
- Pending dues surfaced: 3 customers

Small note:
“Values shown are demo estimates, not production benchmarks.”

---

## 08. Real vs Simulated Transparency Panel
**Role:** observer  
**Device:** desktop  
**Purpose:** build trust

### Exact UI content
**Title:**  
“What is real in this prototype?”

**Real**
- Catalog, stock, and khata are stateful
- Bills update inventory
- Partner setup changes live behavior
- Summaries are generated from current state

**Assisted / hybrid**
- Voice transcription
- Intent parsing
- Invoice extraction
- Confidence scoring

**Simulated**
- Real WhatsApp delivery
- Real supplier message sending
- Real payment confirmation from UPI
- Offline sync engine
- Marketplace / SDK / ecosystem modules

---

## 09. Partner Portfolio Home
**Role:** partner  
**Device:** desktop  
**Purpose:** portfolio entry point

### Exact UI content
**Header:**  
“Good morning, Neha”

**Subheader:**  
“You manage 12 shops”

**KPIs**
- Live shops
- Sandbox shops
- Shops with pending exceptions
- Shops needing attention today

Buttons:
- Add new shop
- Open sandbox lab
- View exception queue

---

## 10. New Shop Wizard — Basic Details
**Role:** partner  
**Device:** desktop  
**Purpose:** create shop

### Exact UI content
**Title:**  
“Create a new shop”

**Helper text:**  
“This should take 8–10 minutes in demo mode.”

### Fields
- **Shop name** — text, required, placeholder “Shree Ganesh Kirana”
- **Owner name** — text, required, placeholder “Ramesh Patel”
- **WhatsApp number** — phone, required, placeholder “+91 98765 43210”
- **City / area** — text, required, placeholder “Surat”
- **GST status** — radio: GST / Non-GST
- **Business hours** — time range, default “08:00 AM – 10:00 PM”
- **Preferred language** — dropdown, default “Hinglish”
- **Summary time** — time picker, default “09:00 PM”

Buttons:
- Back
- Save draft
- Continue

---

## 11. New Shop Wizard — Bundle Selection
**Role:** partner  
**Device:** desktop  
**Purpose:** choose kirana bundle

### Exact UI content
**Title:**  
“Choose an agent bundle”

**Top note:**  
“For v1, Kirana is the recommended starting vertical.”

**Recommended bundle card:**  
“Kirana Core Bundle”

Included agents:
- Billing
- Inventory
- Credit / Khata
- Reorder
- Daily Summary
- Memory
- Orchestrator

Estimated setup time:
“10 minutes”

---

## 12. New Shop Wizard — Catalog Import
**Role:** partner  
**Device:** desktop  
**Purpose:** load products

### Exact UI content
**Title:**  
“Load shop products”

**Helper text:**  
“For the prototype, start with the top 20–50 fast-moving products.”

Tabs:
- Upload CSV
- Manual entry
- Use sample catalog

Manual entry fields:
- Product name
- Alias
- Category
- Unit type
- Pack size
- Selling price
- Opening stock
- Reorder threshold
- Preferred supplier

---

## 13. New Shop Wizard — Customers & Khata
**Role:** partner  
**Device:** desktop  
**Purpose:** set up credit customers

### Exact UI content
**Title:**  
“Set up customers and khata”

**Helper text:**  
“For the prototype, add only regular credit customers and common aliases.”

Table columns:
- Customer name
- Alias
- Phone
- Credit enabled
- Current outstanding
- Reminder timing
- Approval override

---

## 14. New Shop Wizard — Suppliers & Reorder Rules
**Role:** partner  
**Device:** desktop  
**Purpose:** set procurement context

### Exact UI content
**Title:**  
“Add suppliers and reorder logic”

Supplier fields:
- Supplier name
- Phone number
- Categories supplied
- Preferred items
- Lead time

Rule section:
- “When stock goes below threshold, draft reorder”
- “Always require owner approval”
- “Use preferred supplier if available”

---

## 15. New Shop Wizard — Language / Tone / Trust Rules
**Role:** partner  
**Device:** desktop  
**Purpose:** configure trust and behavior

### Exact UI content
**Title:**  
“Set language, tone, and trust rules”

Card 1: Language & tone
- Preferred language
- Summary tone
- Short vs detailed responses

Card 2: Approval rules
- Bills above ₹500 require confirmation
- All supplier orders require approval
- Credit updates do not auto-send reminders without approval

Card 3: Clarification rules
- Ask if multiple products match a phrase
- Ask if multiple customers match a name
- Never guess when confidence is low

---

## 16. Sandbox Test Lab
**Role:** partner  
**Device:** desktop  
**Purpose:** test before go-live

### Exact UI content
**Title:**  
“Sandbox Test Lab”

Scenario buttons:
- Test voice bill
- Test stock query
- Test payment update
- Test invoice photo
- Test daily summary
- Test ambiguous request

Center note:
“This test uses sandbox state. No live records will be affected.”

Right results headings:
- Input
- Output
- Agents used
- Confidence
- Result

---

## 17. Go Live Summary
**Role:** partner  
**Device:** desktop  
**Purpose:** activation checkpoint

### Exact UI content
**Title:**  
“Ready to go live”

Sections:
- Shop details
- Active agents
- Catalog loaded
- Customers loaded
- Suppliers loaded
- Rules configured
- Sandbox passed

Checklist:
- Shop details complete
- At least 10 products added
- At least 1 credit customer added
- Approval thresholds reviewed
- Sandbox tested

Primary CTA:
- Go live

Secondary CTA:
- Back to sandbox

---

## 18. Shop Health Dashboard
**Role:** partner  
**Device:** desktop  
**Purpose:** monitor live usage

### Exact UI content
**Title:**  
“Shree Ganesh Kirana — Health Dashboard”

KPIs:
- Bills today
- Credit sales today
- Dues collected today
- Low-stock alerts
- Pending clarifications
- Pending approvals

Recent activity:
- “10:15 AM — Bill confirmed for Ram bhai”
- “10:18 AM — Low stock detected: Sunflower Oil”
- “10:19 AM — Reorder awaiting approval”

Health labels:
- Healthy
- Needs follow-up
- Risk of disengagement

---

## 19. Edit Context & Memory
**Role:** partner  
**Device:** desktop  
**Purpose:** maintain shop after deployment

### Exact UI content
**Title:**  
“Edit shop context”

Tabs:
- Products
- Customers
- Suppliers
- Shop preferences
- Learned memory

Actions:
- Add product
- Edit price
- Update stock threshold
- Change supplier
- Add customer
- Add alias
- Change reminder timing
- Save changes
- Retest in sandbox
- Push live

---

## 20. Exception Queue
**Role:** partner  
**Device:** desktop  
**Purpose:** human review queue

### Exact UI content
**Title:**  
“Exception queue”

Types:
- Ambiguous customer name
- Ambiguous product alias
- Low-confidence invoice read
- Missing supplier mapping
- Reorder draft not approved
- Summary failed to send

Columns:
- Type
- Shop
- Severity
- Created at
- Suggested action
- Resolve button

Severity chips:
- Low
- Medium
- High

---

## 21. Lite Rule Builder
**Role:** partner  
**Device:** desktop  
**Purpose:** show configurable logic without full flow builder

### Exact UI content
**Title:**  
“Rules”

**Helper text:**  
“v1 supports simple operational rules. Full visual flow building is out of scope for this prototype.”

Rule examples:
1. If stock < threshold → draft reorder
2. If bill type = credit → update khata
3. If bill total > ₹500 → ask approval
4. At 9 PM → send daily summary

---

## 22. WhatsApp Chat Home
**Role:** shopkeeper  
**Device:** mobile  
**Purpose:** core shopkeeper experience

### Exact UI content
Header:
- Assistant name: Rupantar Assistant
- Status text: Shop Ops Active

First message:
“Namaste Ramesh bhai 👋  
Main aapka Rupantar Assistant hoon. Aap mujhe voice note ya message bhej sakte ho. Main bill bana sakta hoon, stock check kar sakta hoon, khata update kar sakta hoon, aur aaj ka summary bhej sakta hoon.”

Quick chips:
- Bill banao
- Stock check
- Khata dekho
- Aaj ka summary

Composer placeholder:
“Message type karo ya voice note bhejo…”

Attachment options:
- Camera
- Photo
- Voice note

---

## 23. Voice Note Review Sheet
**Role:** shopkeeper  
**Device:** mobile  
**Purpose:** confirm transcription and parsed intent

### Exact UI content
Title:
“Maine yeh samjha”

Transcript:
“Ram ko 2 kilo regular chawal, 1 litre sunflower tel aur 3 Parle-G ka bill. Udhar mein.”

Detected items:
- Regular chawal — 2 kg
- Sunflower oil — 1 L
- Parle-G — 3 pcs

Detected customer:
- Ram bhai

Payment mode:
- Credit / Udhar

Buttons:
- Sahi hai
- Edit karo
- Cancel

---

## 24. Bill Preview & Approval Card
**Role:** shopkeeper  
**Device:** mobile  
**Purpose:** approve billing action

### Exact UI content
Card title:
“Draft bill ready”

Customer:
“Ram bhai”

Items:
- Regular chawal — 2 kg — ₹120
- Sunflower oil 1L — 1 — ₹160
- Parle-G — 3 — ₹30

“Total: ₹310”

Buttons:
- Confirm bill
- Edit items
- Cancel

Success:
“Bill bana diya ✅  
Ram bhai ka naya balance ₹2,160 ho gaya.  
Stock bhi update ho gaya.”

---

## 25. Stock Status & Reorder Card
**Role:** shopkeeper  
**Device:** mobile  
**Purpose:** stock + reorder

### Exact UI content
Card title:
“Stock update”

Example:
“Basmati rice 5kg: 3 packs bache hain.  
Yeh low stock mein hai.”

Suggested order:
“Suggested order: 12 packs from Bharat Traders  
Estimated value: ₹1,680”

Buttons:
- Order draft dikhao
- Abhi nahi

Order draft state:
“Order abhi send nahi hua hai. Aapke approval ka wait hai.”

Buttons:
- Approve order
- Quantity change karo
- Cancel

---

## 26. Payment / Khata Update Card
**Role:** shopkeeper  
**Device:** mobile  
**Purpose:** update customer payment

### Exact UI content
Card title:
“Khata updated”

Message:
“Ram bhai ne ₹500 diye.”

Balance lines:
- Purana balance: ₹2,160
- Naya balance: ₹1,660

Optional:
“Receipt note bhejna hai?”

Buttons:
- Haan
- Nahi

If asking balance:
“Ram bhai ka current balance ₹1,660 hai.”

---

## 27. Photo Extraction Preview
**Role:** shopkeeper  
**Device:** mobile  
**Purpose:** preview extracted stock additions from image

### Exact UI content
Card title:
“Photo se yeh items mile”

Helper:
“Please confirm stock add karna hai.”

Rows:
- Sunflower oil 1L — 12 units
- Parle-G — 24 packs
- Toor dal 1kg — 10 packs

Confidence note:
“1 item low confidence mein hai: ‘Refined Oil’”

Buttons:
- Confirm stock add
- Edit
- Cancel

Success:
“Stock add kar diya ✅”

---

## 28. Daily Summary Card
**Role:** shopkeeper  
**Device:** mobile  
**Purpose:** show end-of-day value

### Exact UI content
Card title:
“Aaj ka summary”

Body:
- Total sales: ₹8,540
- Cash: ₹5,900
- Credit: ₹2,640
- Dues received: ₹500
- Low stock: Sunflower oil, Parle-G
- Pending dues: 3 customers

Recommendation:
“Kal subah Bharat Traders ko order draft approve karna useful rahega.”

Buttons:
- Voice mein sunao
- Detail bhejo
- Theek hai

---

## 29. Clarification / Fallback Card
**Role:** shopkeeper  
**Device:** mobile  
**Purpose:** safe fallback when assistant is unsure

### Exact UI content
Case A:
“2 customers mile:  
1. Ram bhai  
2. Hotel Ram  
Kaunsa wala?”

Buttons:
- Ram bhai
- Hotel Ram

Case B:
“‘Tel’ se aapka matlab kaunsa hai?”
- Sunflower oil 1L
- Groundnut oil 1L

Case C:
“Main is order ko bina confirm kiye send karne mein confident nahi hoon. Kya main draft banaun?”

Buttons:
- Draft banao
- Cancel

---

## 30. Session Inspector
**Role:** admin, internal product team  
**Device:** desktop  
**Purpose:** deep debug and replay

### Exact UI content
Title:
“Session inspector”

Sections:
- Raw input
- Parsed intent
- Agent timeline
- State before
- State after
- User output
- Error if any

Buttons:
- Replay session
- Fork from step
- Export JSON

---

## 31. Demo Reset & Seed Data Control
**Role:** admin  
**Device:** desktop  
**Purpose:** reset demo safely

### Exact UI content
Title:
“Demo state controls”

Reset options:
- Reset shop inventory
- Reset customer balances
- Reset conversation history
- Reset partner setup
- Reload seed data
- Switch to another shop seed

Warning:
“This will overwrite current demo state.”

Buttons:
- Reset selected
- Reset all
- Cancel

---

# 6. Exact scenario copy

## Scenario A — Welcome
“Namaste Ramesh bhai 👋  
Main aapka Rupantar Assistant hoon. Aap mujhe voice note ya message bhej sakte ho. Main bill bana sakta hoon, stock check kar sakta hoon, khata update kar sakta hoon, aur aaj ka summary bhej sakta hoon.”

Quick chips:
- Bill banao
- Stock check
- Khata dekho
- Aaj ka summary

## Scenario B — Voice bill on credit
User voice:
“Ram ko 2 kilo chawal, 1 tel aur 3 biscuit ka bill bana do. Udhar mein daal do.”

Voice Review:
“Maine yeh samjha”

Transcript:
“Ram ko 2 kilo regular chawal, 1 litre sunflower tel aur 3 Parle-G ka bill. Udhar mein.”

Detected customer:
“Ram bhai”

Payment mode:
“Credit / Udhar”

Buttons:
- Sahi hai
- Edit karo
- Cancel

Bill Preview:
“Draft bill ready”

Items:
- Regular chawal — 2 kg — ₹120
- Sunflower oil 1L — 1 — ₹160
- Parle-G — 3 — ₹30

Total:
₹310

Success:
“Bill bana diya ✅  
Ram bhai ka naya balance ₹2,160 ho gaya.  
Stock bhi update ho gaya.”

## Scenario C — Low stock + reorder
User:
“Sunflower oil kitna bacha hai?”

Assistant:
“Sunflower oil 1L: 4 units bache hain.  
Yeh low stock mein hai.”

“Suggested order: 12 units from Bharat Traders  
Estimated value: ₹1,680”

Buttons:
- Order draft dikhao
- Abhi nahi

## Scenario D — Payment received
User:
“Ram ne 500 de diye.”

Assistant:
“Khata updated ✅  
Purana balance: ₹2,160  
Naya balance: ₹1,660”

“Receipt note bhejna hai?”

Buttons:
- Haan
- Nahi

## Scenario E — Supplier invoice photo
Assistant:
“Photo se yeh items mile.  
Please confirm stock add karna hai.”

Rows:
- Sunflower oil 1L — 12 units
- Parle-G — 24 packs
- Toor dal 1kg — 10 packs
- Refined oil — low confidence

Buttons:
- Confirm stock add
- Edit
- Cancel

## Scenario F — Daily summary
“Aaj ka summary”

- Total sales: ₹8,540
- Cash: ₹5,900
- Credit: ₹2,640
- Dues received: ₹500
- Low stock: Sunflower oil, Parle-G
- Pending dues: 3 customers

“Kal subah Bharat Traders ko order draft approve karna useful rahega.”

Buttons:
- Voice mein sunao
- Detail bhejo
- Theek hai

## Scenario G — Ambiguous request
User:
“Ram ka balance batao.”

Assistant:
“2 customers mile:  
1. Ram bhai  
2. Hotel Ram  
Kaunsa wala?”

Buttons:
- Ram bhai
- Hotel Ram

User:
“Tel order kar do.”

Assistant:
“‘Tel’ se aapka matlab kaunsa hai?”

Buttons:
- Sunflower oil 1L
- Groundnut oil 1L

---

# 7. Suggested Figma frame organization

- `00_Global / Components`
- `01_Entry / Role Selector`
- `01_Entry / Scenario Launcher`
- `02_Observer / Executive Overview`
- `02_Observer / Live Demo Canvas`
- `02_Observer / Audit Drawer`
- `02_Observer / Memory Inspector`
- `02_Observer / ROI View`
- `02_Observer / Truth Panel`
- `03_Partner / Portfolio`
- `03_Partner / Wizard 1 Basic`
- `03_Partner / Wizard 2 Bundle`
- `03_Partner / Wizard 3 Catalog`
- `03_Partner / Wizard 4 Customers`
- `03_Partner / Wizard 5 Suppliers`
- `03_Partner / Wizard 6 Rules`
- `03_Partner / Wizard 7 Sandbox`
- `03_Partner / Wizard 8 Go Live`
- `03_Partner / Health Dashboard`
- `03_Partner / Edit Context`
- `03_Partner / Exception Queue`
- `03_Partner / Rule Builder`
- `04_Shopkeeper / Chat Home`
- `04_Shopkeeper / Voice Review`
- `04_Shopkeeper / Bill Approval`
- `04_Shopkeeper / Stock Reorder`
- `04_Shopkeeper / Payment Khata`
- `04_Shopkeeper / Photo Extraction`
- `04_Shopkeeper / Daily Summary`
- `04_Shopkeeper / Clarification`
- `05_Admin / Session Inspector`
- `05_Admin / Demo Reset`

---

# 8. Final design guidance

Two things matter more than visual polish:

1. The **shopkeeper flow must feel extremely simple**.
2. The **partner flow must feel repeatable**, not magical.

A prototype that only shows AI responses but not partner setup will undersell the thesis badly.
