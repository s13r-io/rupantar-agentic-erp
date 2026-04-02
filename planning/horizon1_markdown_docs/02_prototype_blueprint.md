# Prototype Blueprint
## Rupantar Horizon 1 Prototype — Kirana Ops

## One-line goal
Prove that a small retailer can run daily operations through **WhatsApp + voice**, while a partner can configure and deploy that system quickly enough for the partner-distribution thesis to feel real.

---

# 1. What this prototype is trying to prove

The prototype should prove **five things**, in this order:

## 1) Shopkeepers can operate through WhatsApp, not a traditional app
The strongest experiential claim is that the shopkeeper uses **voice notes, photos, and one-word replies**, with no complicated UI.

## 2) The product is not “a chatbot”
The system should clearly feel like an **operational assistant**:
- it understands intent,
- chooses the right internal agent,
- takes an action,
- updates records,
- asks for approval when uncertain,
- and confirms the result.

## 3) A partner can configure it without engineers
The prototype must make that believable:
- choose bundles
- enter shop data
- set thresholds and rules
- test before deployment
- go live

## 4) Kirana is a credible first wedge
Kirana exercises:
- billing
- inventory
- credit
- procurement
- daily summary

## 5) Horizon 1 can be narrower than the full vision
The prototype should feel like a focused wedge, not the whole platform.

---

# 2. Who the prototype is for

## A. Shopkeeper
This user must feel:
- “I can actually use this”
- “I do not need training”
- “It understands how I talk”
- “I stay in control when money or stock is involved”

## B. Partner / AI Shop Doctor
This user must feel:
- “I can deploy this at a customer site”
- “I can configure this without calling engineers”
- “I can maintain a portfolio of shops”
- “This can become a repeatable income stream”

## C. Observer / Sponsor / Investor
This user must feel:
- “The idea is more concrete than a deck”
- “The product is more than an LLM wrapper”
- “The distribution thesis is real”
- “There is a credible path from prototype to pilot”

## D. Internal demo operator (optional)
This role can:
- reset demo data
- trigger scenarios
- switch between happy-path and edge-case flows
- recover demo state

---

# 3. Prototype positioning

## Recommended stance
Do **not** present this as “the AI platform.”

Present it as:

**“A Horizon 1 kirana operations prototype showing how a partner deploys a WhatsApp-native assistant for billing, inventory, khata, reorder, and daily summary.”**

That framing is:
- easier to understand
- more credible
- more demoable
- truer to Horizon 1

---

# 4. Prototype architecture in plain language

The prototype should have **four surfaces**.

## Surface 1: Shopkeeper interface
A browser-based **WhatsApp-like conversation view** that supports:
- text
- voice note playback / upload
- photo upload
- quick reply buttons
- approval requests

## Surface 2: Partner console
A lightweight **Config Studio + deployment console** for:
- new shop setup
- bundle selection
- catalog and customer input
- rule setting
- sandbox testing
- deployment
- shop health review

## Surface 3: Observer / demo view
A side-by-side explanation layer showing:
- what the shopkeeper sees
- what the partner configured
- what the agents are doing internally
- what business outcome was produced

## Surface 4: Internal orchestration / replay view
This is where the invisible intelligence becomes visible:
- detected intent
- selected agent(s)
- confidence
- memory used
- records updated
- approvals requested
- output sent

---

# 5. User roles and permissions

## Role 1: Shopkeeper
Can:
- send voice notes
- send text
- send photos
- confirm or reject actions
- ask for summaries
- check credit and stock
- approve reorder suggestions

Cannot:
- see internal agents
- see confidence scores
- see raw logs
- edit rules or bundle

## Role 2: Partner
Can:
- create a new shop
- choose vertical and bundle
- upload catalog
- enter customers / credit data
- define supplier thresholds
- set language and tone
- define approval rules
- test workflows
- deploy
- monitor shop health
- edit context after deployment

Cannot:
- change deep platform internals
- modify global agent logic in v1
- access multi-tenant admin tools

## Role 3: Observer
Can:
- watch guided scenarios
- compare before vs after
- inspect audit trails
- inspect memory and confidence
- view outcome metrics
- switch between roles in demo mode

Cannot:
- change live shop data unless explicitly in demo operator mode

## Role 4: Demo operator
Can:
- reset scenario state
- preload outputs
- toggle real/simulated features
- switch demo tracks
- recover demo if speech/OCR fails

---

# 6. Exact screen list

## A. Common / Entry Screens

### Screen 01 — Landing / Role Selector
Purpose:
- choose how to enter the prototype

Must show:
- Shopkeeper
- Partner
- Observer
- Demo Operator
- selected vertical: Kirana
- “Start guided demo”
- “Explore manually”

### Screen 02 — Scenario Launcher
Purpose:
- start prebuilt stories

Must show:
- Morning billing rush
- Low stock + reorder
- Payment received
- Supplier invoice photo
- Daily summary
- Ambiguous request / clarification
- Partner deploy-new-shop

### Screen 03 — Demo State Reset
Purpose:
- reset all seeded records

Must show:
- reset inventory
- reset khata balances
- reset conversation history
- reset agent logs
- reset today’s sales

---

## B. Observer Screens

### Screen 04 — Executive Overview Dashboard
Purpose:
- explain what the prototype covers

Must show:
- one kirana
- one partner
- seven agents
- what problem is being solved
- what is live vs simulated
- what this proves

### Screen 05 — Side-by-Side Live Demo Canvas
Purpose:
- primary demo screen

Layout:
- left: partner/shop snapshot
- center: WhatsApp thread
- right: orchestration/log panel

### Screen 06 — Scenario Timeline
Purpose:
- show interaction sequence

Must show:
- user input
- agent routing
- record updates
- confirmation
- final outcome

### Screen 07 — Agent Log / Audit Trail
Purpose:
- make the system feel accountable

Must show:
- timestamped steps
- agent selected
- confidence level
- memory used
- action performed
- approval needed or not
- success / failure

### Screen 08 — Memory / Context Inspector
Purpose:
- make persistent memory tangible

Must show:
- shop profile
- customer history
- product aliases
- supplier preferences
- reorder thresholds
- language/tone
- learned patterns

### Screen 09 — Before vs After Comparison
Purpose:
- show operational transformation

### Screen 10 — Value / ROI Estimator
Purpose:
- show estimated value

### Screen 11 — Real vs Simulated Transparency Panel
Purpose:
- build credibility

---

## C. Partner Screens

### Screen 12 — Partner Home / Portfolio
Must show:
- shops list
- live / sandbox tags
- health score
- pending exceptions
- low-confidence items
- last activity
- quick actions

### Screen 13 — New Shop Wizard: Basic Details
Inputs:
- shop name
- owner name
- phone number
- location
- GST / non-GST
- operating hours
- language
- WhatsApp number

### Screen 14 — New Shop Wizard: Vertical + Bundle
Must show:
- vertical selected: Kirana
- recommended bundle:
  - Billing
  - Inventory
  - Credit / Khata
  - Procurement
  - Daily Summary
  - Memory
  - Orchestrator
- estimated setup time

### Screen 15 — New Shop Wizard: Catalog Import
Purpose:
- load shop products

### Screen 16 — New Shop Wizard: Customers + Khata
Purpose:
- set credit relationships

### Screen 17 — New Shop Wizard: Suppliers + Reorder Rules
Purpose:
- set procurement context

### Screen 18 — New Shop Wizard: Language + Tone + Trust Rules
Purpose:
- configure interaction style and approval rules

### Screen 19 — Sandbox Test Lab
Purpose:
- run simulated inputs before go-live

### Screen 20 — Deployment / Go Live Summary
Purpose:
- activation step

### Screen 21 — Shop Health Dashboard
Purpose:
- portfolio monitoring

### Screen 22 — Edit Context / Memory
Purpose:
- field maintenance after deployment

### Screen 23 — Exception Queue / Human Review Queue
Purpose:
- route low-confidence or missing-context items for review

### Screen 24 — Lite Rule Builder
Purpose:
- show operational rules without building a full drag-and-drop flow graph

---

## D. Shopkeeper Screens

### Screen 25 — WhatsApp Conversation Home
Central shopkeeper experience.

### Screen 26 — Voice Note Review Card
Shows transcript and extracted intent.

### Screen 27 — Bill Preview Card
Shows customer, items, total, and approval buttons.

### Screen 28 — Stock Result Card
Shows stock left, low-stock warning, and suggested action.

### Screen 29 — Khata / Payment Update Card
Shows old balance, payment received, new balance.

### Screen 30 — Reorder Approval Card
Shows suggested supplier order and asks for approval.

### Screen 31 — Photo Upload + Extraction Preview
Shows extracted items from photo and asks for confirmation.

### Screen 32 — Daily Summary Card
Shows end-of-day value.

### Screen 33 — Clarification / Fallback Card
Handles uncertainty.

---

## E. Internal / Admin Screen

### Screen 34 — Event Replay / Session Inspector
Purpose:
- replay a session and inspect transitions

---

# 7. Agents included in v1

Visible to observer/admin:
1. Orchestrator
2. Billing agent
3. Inventory agent
4. Khata/Credit agent
5. Procurement agent
6. Daily Summary agent
7. Memory agent

Visible to shopkeeper:
- only one assistant identity

---

# 8. Seed demo data

## Demo shop
- Shop: Shree Ganesh Kirana
- Owner: Ramesh Patel
- City: Surat
- Language: Hinglish
- GST: No
- Summary time: 9:00 PM

## Customers
- Ram bhai — outstanding ₹1,850
- Shyam — outstanding ₹450
- Meena aunty — cash customer
- Hotel Ganesh — bulk buyer
- Hotel Ram — for ambiguity case

## Suppliers
- Bharat Traders
- Shiv Distributors
- Fresh Mart Supply

## Products
Include 15–20 items such as:
- Basmati rice 5kg
- Regular rice loose
- Atta 10kg
- Sugar 1kg
- Sunflower oil 1L
- Groundnut oil 1L
- Toor dal
- Maggi
- Parle-G
- Bread
- Milk
- Tea powder
- Detergent
- Soap

## Useful aliases
- “chawal” → more than one rice product
- “tel” → more than one oil
- “biscuit” → category ambiguity
- “Ram” → more than one customer candidate

## Rules
- bills above ₹500 need confirmation
- reorders always need approval
- credit reminders only after 7 days
- daily summary at 9 PM
- ambiguous customer/item must ask clarification

---

# 9. Role-by-role flows

## A. Shopkeeper flows

### Flow A1 — First-time welcome
Goal:
- establish trust quickly

### Flow A2 — Voice note bill on credit
Sample:
“Ram ko 2 kilo chawal, 1 tel aur 3 biscuit ka bill bana do. Udhar mein daal do.”

System sequence:
1. Orchestrator detects multi-part intent
2. Billing extracts items
3. Memory maps customer
4. Inventory checks stock
5. Khata prepares credit update
6. Bill Preview appears
7. User confirms
8. Bill is created
9. Inventory and khata update
10. Chat confirms result

### Flow A3 — Ask stock availability
Sample:
“Basmati kitna bacha hai?”

### Flow A4 — Receive customer payment
Sample:
“Ram ne 500 de diye.”

### Flow A5 — Add stock from supplier invoice photo
Upload image → extract items → confirm → update stock.

### Flow A6 — End-of-day summary
Triggered manually or scheduled.

### Flow A7 — Ambiguous input
Examples:
- Which Ram?
- Which oil?

System asks clarification before proceeding.

---

## B. Partner flows

### Flow B1 — Create a new shop
blank shop → bundle → context → rules → test → live

### Flow B2 — Configure trust rules
approval thresholds, reminder timing, language, tone

### Flow B3 — Test before deployment
simulate common workflows

### Flow B4 — Review health after deployment
dashboard visibility

### Flow B5 — Fix a data/context issue
edit products, prices, thresholds, aliases, etc.

---

## C. Observer flows

### Flow C1 — Guided 5-minute demo
### Flow C2 — Deep operator explanation
### Flow C3 — Before vs after / ROI view
### Flow C4 — Real vs simulated review

---

# 10. Feature scope for v1

## Must-have for v1

### Shopkeeper side
- WhatsApp-like thread
- voice-note demo input
- text input
- photo upload input
- bill preview + approval
- stock response
- khata update response
- reorder approval card
- daily summary card
- clarification card

### Partner side
- create shop wizard
- kirana bundle selection
- catalog import/manual entry
- customer/khata setup
- supplier rules
- language/tone rules
- threshold rules
- sandbox test
- go live
- shop health dashboard
- edit context

### Observer side
- side-by-side demo canvas
- audit log
- memory inspector
- before/after value view
- real vs simulated panel

### Platform behaviors
- stateful inventory updates
- stateful khata updates
- basic memory layer
- agent routing view
- confidence + approval logic
- session replay

## Should-have for v1 if time allows
- real speech-to-text on supported phrases
- editable invoice extraction preview
- downloadable bill PDF
- seeded multi-language toggle
- proactive reminder scheduling
- supplier draft order generation
- daily summary audio playback

## Explicitly out of scope for v1
- 160+ agents
- full multi-vertical rollout
- full visual flow builder
- Pro Code SDK
- marketplace
- real ONDC/ABDM/GST integrations
- live UPI reconciliation
- full offline-first sync
- full multilingual speech robustness
- production observability stack
- production-grade compliance flows

---

# 11. What is real vs simulated

## Real in v1
- browser-based WhatsApp-like chat
- seeded, editable shop context
- stateful inventory
- stateful khata ledger
- bill generation logic
- inventory decrement/increment logic
- reorder rule triggers
- daily summary generation from current state
- partner onboarding wizard
- role-based navigation
- audit/replay views

## Assisted / hybrid in v1
- voice transcription
- product/entity extraction
- image/invoice extraction
- confidence scoring
- multi-agent routing explanation
- summary phrasing

## Simulated in v1
- real WhatsApp Business API delivery
- real supplier order placement
- real payment confirmation from UPI
- real offline queue/sync
- 12-language vernacular depth
- automated reminder escalation
- full observability stack
- multi-provider LLM routing
- marketplace, SDK, ecosystem modules

---

# 12. Demo scenarios

## Scenario 1 — Morning rush billing
voice note → bill → stock update → khata update

## Scenario 2 — Low stock detected
inventory → reorder suggestion → approval

## Scenario 3 — Customer payment recorded
payment → balance change → optional receipt

## Scenario 4 — Supplier invoice photo
photo → extraction → confirmation → stock update

## Scenario 5 — End-of-day summary
scheduled summary → business value

## Scenario 6 — Ambiguity handling
uncertain input → clarification → safe continuation

## Scenario 7 — Partner deploys a new shop
partner onboarding flow → live activation

## Scenario 8 — Partner fixes an issue post-live
context maintenance

---

# 13. 5-minute demo script

## 0:00–0:30 — Set the frame
“This prototype proves one Horizon 1 wedge: a kirana can operate through WhatsApp and voice, and a partner can configure that system quickly enough to scale.”

## 0:30–1:00 — Show the three modes
Role Selector → Shopkeeper / Partner / Observer

## 1:00–2:10 — Main shopkeeper flow
Run Scenario 1 on Live Demo Canvas.

## 2:10–3:00 — Show trust and ambiguity
Run Scenario 6.

## 3:00–3:40 — Show low stock to reorder
Run Scenario 2.

## 3:40–4:20 — Show partner setup
Open Sandbox / Go Live flow.

## 4:20–5:00 — Show audit + truth panel
Open Audit Trail + Real vs Simulated.

---

# 14. 15-minute investor / partner walkthrough

## 0:00–1:30 — Thesis and why this wedge
Problem, wedge choice, partner deployment importance.

## 1:30–4:30 — Shopkeeper journey
Run voice bill, payment received, daily summary.

## 4:30–7:00 — Partner deployment journey
Walk through setup and go-live.

## 7:00–9:00 — Trust, memory, explainability
Show audit log and memory inspector.

## 9:00–11:00 — Beyond happy path
Run ambiguity and low-confidence flows.

## 11:00–12:30 — Business/distribution lens
Show shop health and portfolio logic.

## 12:30–13:30 — Real vs simulated honesty
Explain prototype boundaries.

## 13:30–15:00 — Close with decision questions
1. Does this feel usable for a shopkeeper?
2. Does this feel deployable by a partner?
3. Does this feel enough of a wedge to justify a pilot?

---

# 15. Positive inputs

- kirana-first is the right prototype choice
- partner layer should be as prominent as the AI
- confidence thresholds are a major trust asset
- memory makes the system feel differentiated
- side-by-side observer mode is very smart for this stage

---

# 16. Constructive inputs

- do not build the full visual flow builder in v1
- do not try to show too many verticals
- do not let the demo feel too perfect
- be explicit where AI is assisted
- do not expose internal agents to the shopkeeper
- put more effort into context setup than into AI theatrics

---

# 17. Practical build order

1. Observer mode + seeded data + shopkeeper chat mock
2. Billing + inventory + khata state changes
3. Partner setup wizard + sandbox + go-live
4. Audit log + memory inspector + confidence flow
5. Photo extraction + daily summary + exception queue
6. Polish demo tracks and role-switching

---

# Final recommendation
The prototype should feel like a **deployable kirana operating assistant**, not like a futuristic concept deck.

That means:
- one vertical
- one partner workflow
- one shopkeeper workflow
- one clear trust model
- one side-by-side explanation mode
