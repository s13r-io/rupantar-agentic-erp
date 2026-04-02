# Horizon 1 Prototype Scope
## Rupantar Horizon 1 Prototype — Kirana Ops

## Purpose
This document defines the **prototype scope for Horizon 1** of the proposed AI platform. The purpose of the prototype is not to prove the entire long-term platform vision. It is to prove the few things that make the concept believable, usable, and commercially testable.

The prototype should prove:

1. A shopkeeper can actually run work through **WhatsApp / voice / photo-led workflows**.
2. A partner can actually **configure and deploy the system without engineers**.
3. The system feels like an **operational agent**, not just a chatbot.
4. Kirana is a credible first wedge for Horizon 1.
5. The concept can be communicated clearly to sponsors, investors, partners, and pilot users.

---

## Core recommendation
Build the prototype around:

- **one vertical**: Kirana
- **one partner flow**
- **one shopkeeper flow**
- **one observer/demo flow**
- **one visible proof of backend intelligence**

The goal is **depth over breadth**.

Do **not** attempt to prototype the entire 160+ agent vision or multiple verticals at equal depth in v1.

---

## Why Kirana for v1
Kirana is the strongest prototype wedge because it naturally combines:

- billing
- inventory
- credit / khata
- procurement / reorder
- daily reporting

It is also:
- easy for audiences to understand quickly
- frequent-use
- operationally rich
- suitable for partner-led deployment
- aligned with Horizon 1 priorities

Second-best option would be auto garage, but kirana is better for a first prototype because it is more relatable and covers more of the operational thesis in one place.

---

## What the prototype should prove

### 1. Shopkeepers can operate through WhatsApp
The most important claim to prove is that the shopkeeper can interact through:

- voice notes
- text
- photos
- short replies like “haan”, “nahi”, “confirm”

without needing to learn a new UI.

### 2. The product is not “just a chatbot”
It should feel like a real operating system assistant:
- it understands intent
- chooses the right internal function/agent
- changes records
- asks for approval when needed
- confirms outcomes

### 3. Partners can deploy it
The prototype must make the partner layer real:
- create shop
- choose bundle
- load context
- set rules
- test
- deploy
- maintain

### 4. Trust is designed into the system
The prototype must visibly show:
- confidence thresholds
- approval requests
- clarification when unsure
- memory/context usage
- audit trail / replay

### 5. Horizon 1 can start narrow
The prototype should communicate:
- one vertical
- one operational bundle
- one deployment model

rather than a broad but shallow “AI platform” story.

---

## Target audiences

### Primary audience
1. **Investors / leadership / internal sponsors**
2. **Pilot partners / resellers / field reps**

### Secondary audience
3. **Pilot shopkeepers**

### Not the main target for v1
- generic consumers
- enterprise buyers
- engineers as a showcase audience

---

## Product surfaces to include

### 1. WhatsApp-style shop interface
This is the emotional center of the prototype.

It should support:
- text messages
- voice notes
- image uploads
- quick reply buttons
- approval requests

### 2. Partner onboarding / configuration console
This is critical to proving the distribution thesis.

It should let a partner:
- create a shop
- choose a bundle
- upload context
- configure simple rules
- test workflows
- deploy live

### 3. Lightweight orchestration / admin layer
This may be partly simulated, but must exist visually.

It should show:
- which internal agent handled the request
- what it did
- confidence
- approval logic
- memory/context used

### 4. Demo / observer mode
This is for sponsors and reviewers.

It should provide:
- guided scenarios
- side-by-side role views
- internal logic visibility
- before/after framing
- value/ROI view

---

## Recommended v1 agents for Kirana

Use only **5–7 agents**, not 160+.

### Recommended v1 bundle
1. Billing agent
2. Inventory agent
3. Credit / Khata agent
4. Procurement / Reorder suggestion agent
5. Daily Summary agent
6. Memory agent
7. Orchestrator agent

### Important UX rule
The **shopkeeper should not see seven bots**.

The shopkeeper should experience **one assistant identity**.  
The observer/admin layer can reveal the internal decomposition.

---

## What should the shopkeeper be able to do

### 1. Create a bill from voice
Example:
“Ram ko 2 kilo chawal, 1 tel, aur 3 biscuit ka bill bana do. Udhar mein daal do.”

System should:
- transcribe
- identify products
- identify customer
- compute bill
- update credit
- ask for approval if needed
- confirm outcome

### 2. Ask stock questions
Examples:
- “Basmati kitna bacha hai?”
- “Aaj kaunse items low stock mein hain?”

### 3. Add stock from a photo
Upload:
- supplier invoice
- stock photo
- shelf photo

System should:
- extract items
- draft stock updates
- ask for confirmation

### 4. Update khata / credit
Examples:
- “Ram ne 500 de diye”
- “Shyam ka balance batao”

### 5. Receive a daily summary
Summary should include:
- sales
- cash vs credit
- low stock
- pending dues
- suggested action

### 6. Approve or reject actions in one tap
Examples:
- confirm bill
- send reminder
- place order
- cancel

### 7. Speak naturally
The product should support casual, imperfect phrasing rather than command syntax.

---

## What should the partner be able to do

### 1. Create a new shop
Inputs:
- shop name
- owner name
- phone number
- vertical
- language
- GST / non-GST
- hours
- rules

### 2. Choose an agent bundle
For kirana:
- billing
- inventory
- khata
- reorder
- daily summary
- memory
- orchestrator

### 3. Upload / configure context
Including:
- products
- prices
- units
- aliases
- customers
- credit balances
- suppliers
- thresholds

### 4. Set rules
Examples:
- low stock threshold
- approval over ₹500
- reminder after 7 days
- daily summary at 9 PM
- language = Hinglish

### 5. Test before deployment
The partner should simulate workflows before going live.

### 6. Deploy the shop
A visible “Go Live” step is important.

### 7. View shop health
Dashboard examples:
- interactions
- bills created
- low-stock alerts
- confidence issues
- pending confirmations

### 8. Edit context later
Partner should be able to:
- add products
- edit prices
- add aliases
- change thresholds
- update suppliers

---

## What the observer should be able to do

### 1. Run prebuilt scenarios
Examples:
- morning rush billing
- low stock + reorder
- payment received
- supplier invoice photo
- end-of-day summary
- ambiguous request / clarification

### 2. See internal reasoning at a safe level
Not chain-of-thought, but structured system logic:
- intent detected
- agent selected
- memory used
- confidence
- action taken
- record changes

### 3. Compare before vs after
Show operational transformation.

### 4. View ROI proxy
Example:
- time saved
- stockouts prevented
- dues tracked
- records digitized

---

## What should NOT be in v1

Do not try to build:
- 160+ agent library
- multiple verticals in equal depth
- full SDK
- full marketplace
- full ONDC/ABDM/GST integration
- perfect multilingual speech stack
- production offline-first sync
- full observability stack
- deep multi-model routing

These can be simulated or shown as roadmap items.

---

## Success criteria

### For shopkeeper
- can complete 3 common tasks with minimal training
- understands responses instantly
- trusts confirmation flow

### For partner
- can configure a shop in 10–15 minutes in demo mode
- can modify rules/context
- believes the product can scale across many shops

### For sponsor/investor
- can explain the concept back after one demo
- believes it is more than a chatbot
- sees a credible path from prototype to pilot

---

## Positive inputs
These are the strongest ideas worth preserving:
- partner layer is the biggest differentiator
- zero-UI is a powerful narrative
- kirana is a strong proving ground
- internal orchestration visibility is excellent for demos

---

## Constructive inputs
These are important guardrails:
- “AI platform” is too broad as a first prototype framing
- do not over-index on transcription perfection
- Config Studio matters more than a full visual flow builder in v1
- make approval and confidence visible
- build memory into the experience
- include one clear failure-and-recovery flow

---

## Recommended prototype packaging

### Prototype title
**Rupantar Horizon 1 Prototype — Kirana Ops**

### Core modules
- Shopkeeper chat
- Partner setup console
- Orchestrator/log view
- Scenario viewer

### Included agents
- Billing
- Inventory
- Khata
- Reorder
- Daily Summary
- Memory
- Orchestrator

### Demo scenarios
- create bill on credit
- check low stock
- add stock from invoice photo
- receive customer payment
- trigger reorder draft
- end-of-day summary
- low-confidence clarification

### Demo metrics shown
- setup time
- active agents
- interactions today
- low-stock alerts caught
- credit tracked
- time saved estimate

---

## Clean next step recommended
After this scope, the best next artifact is a **prototype blueprint with screens, user roles, and demo scenarios**, followed by a **screen-by-screen wireframe spec** and a **component inventory + interaction spec**.
