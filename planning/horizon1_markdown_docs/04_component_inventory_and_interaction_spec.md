# Component Inventory and Interaction Spec
## Rupantar Horizon 1 Prototype — Kirana Ops

This is a **build-facing specification** for the prototype’s reusable UI components, interaction rules, audit model, and seed data. It is intended for product, design, frontend, prototyping, and demo-ops teams.

The system is deliberately optimized for the early Horizon 1 wedge:
- kirana only
- WhatsApp-like shop experience
- partner-led setup
- visible trust mechanisms
- stateful billing / inventory / khata / reorder / summary logic

---

# 1. Scope and design intent

This spec assumes the prototype includes:
- a **Shopkeeper chat experience** that looks and behaves like WhatsApp,
- a **Partner deployment console** that behaves like a lightweight Config Studio,
- an **Observer mode** that makes hidden logic visible,
- and an **Admin/demo layer** for resetting and replaying flows.

It is deliberately **not** a full platform design system for all 160+ agents or all future verticals.

---

# 2. Naming convention

## Component ID format
`cmp.<family>.<name>`

Examples:
- `cmp.shell.app-header`
- `cmp.nav.role-card`
- `cmp.form.text-input`
- `cmp.card.bill-preview`
- `cmp.chat.message-user`
- `cmp.chat.quick-reply-chip`
- `cmp.audit.timeline-row`

## Event ID format
`evt.<domain>.<action>`

Examples:
- `evt.ui.role_selected`
- `evt.partner.shop_created`
- `evt.ai.intent_detected`
- `evt.ai.bill_drafted`
- `evt.approval.requested`
- `evt.clarification.resolved`

## State naming format
Use snake_case enums:
- `draft`
- `awaiting_approval`
- `clarification_needed`
- `completed`
- `failed`

---

# 3. Component inventory

## 3.1 Foundation components

### `cmp.foundation.text`
Variants:
- display
- heading_l
- heading_m
- heading_s
- body_l
- body_m
- body_s
- label
- meta
- mono

Props:
- variant
- weight
- color_role
- truncate
- align

### `cmp.foundation.icon`
Required v1 icons:
- voice
- image
- bill
- stock
- rupee
- summary
- warning
- success
- pending
- error
- info
- customer
- supplier
- memory
- approval
- replay
- settings

Props:
- name
- size
- tone
- decorative:boolean

### `cmp.foundation.status-chip`
Variants:
- live
- sandbox
- draft
- healthy
- needs_attention
- pending
- approval_required
- clarification_needed
- low_confidence
- completed
- failed
- simulated

### `cmp.foundation.badge`
Examples:
- 3 min
- 2 pending
- Kirana
- High

### `cmp.foundation.divider`
Variants:
- horizontal
- vertical
- inset

### `cmp.foundation.avatar`
Use:
- Shopkeeper
- Assistant
- Partner
- Observer annotations

### `cmp.foundation.tooltip`
Use for explaining confidence, memory used, etc.

### `cmp.foundation.skeleton`
Use for:
- chat card loading
- audit log loading
- dashboard loading

### `cmp.foundation.empty-state`
Examples:
- No shops yet
- No exceptions right now
- No memory entries found
- No low-stock items today

---

## 3.2 Layout and navigation components

### `cmp.shell.app-header`
Structure:
- left: product logo + page title
- center: breadcrumb
- right: utility actions

Props:
- title
- breadcrumb_items[]
- actions[]

### `cmp.shell.sidebar-nav`
Sections for partner:
- Portfolio
- New Shop
- Sandbox
- Health
- Exceptions
- Context
- Rules

States:
- default
- active
- hovered
- collapsed

### `cmp.shell.mobile-chat-frame`
Used in shopkeeper mode and observer canvas.

Structure:
- status bar
- chat header
- messages area
- quick actions
- composer

### `cmp.nav.role-card`
Props:
- role_name
- description
- primary_cta
- icon
- featured:boolean

States:
- default
- hover
- pressed
- disabled

### `cmp.nav.scenario-card`
Props:
- title
- subtitle
- duration
- tags[]
- primary_cta
- secondary_cta

### `cmp.nav.stepper`
Props:
- steps[]
- current_step
- allow_jump_back:boolean
- allow_jump_forward:boolean

---

## 3.3 Form input components

### `cmp.form.text-input`
Props:
- label
- placeholder
- value
- required
- helper_text
- error_text
- max_length

States:
- default
- focused
- filled
- error
- disabled

### `cmp.form.phone-input`
Format:
- Indian mobile pattern

### `cmp.form.currency-input`
Use for:
- price
- outstanding balance
- approval thresholds

### `cmp.form.numeric-input`
Use for:
- stock
- thresholds
- lead time

### `cmp.form.dropdown`
Use for:
- language
- category
- unit type
- vertical

### `cmp.form.multi-select`
Use for:
- categories supplied
- preferred items

### `cmp.form.token-input`
Use for aliases.

Behavior:
- enter/comma creates chip
- duplicate prevention
- case-insensitive dedupe

### `cmp.form.checkbox`
### `cmp.form.radio-group`
### `cmp.form.toggle`
### `cmp.form.time-picker`
### `cmp.form.time-range-picker`
### `cmp.form.file-dropzone`
### `cmp.form.inline-editable-table`

---

## 3.4 Chat and card components

### `cmp.chat.header`
Fields:
- assistant name
- status text

### `cmp.chat.message-user`
Props:
- message_id
- text
- timestamp
- state

States:
- sent
- parsing
- linked_to_card
- failed

### `cmp.chat.message-assistant`
Props:
- text
- timestamp
- tone
- linked_card_optional

### `cmp.chat.message-voice`
Props:
- audio_duration
- waveform_placeholder
- transcription_state

States:
- recording
- uploading
- transcribing
- ready
- failed

### `cmp.chat.message-image`
Props:
- thumbnail
- filename
- analysis_state

States:
- uploading
- extracting
- preview_ready
- failed

### `cmp.chat.quick-reply-chip`
Examples:
- Haan
- Nahi
- Confirm bill
- Cancel
- Ram bhai
- Hotel Ram

### `cmp.chat.composer`
Elements:
- text field
- send button
- voice button
- attach button

States:
- empty
- typing
- recording
- attachment_selected
- disabled during commit

---

## Card inventory

### `cmp.card.info`
Use:
- welcome card
- explanation card
- informational answers

### `cmp.card.bill-preview`
Fields:
- customer_name
- items[]
- quantities
- prices
- total
- payment_mode
- approval_reason_optional

Actions:
- Confirm bill
- Edit items
- Cancel

### `cmp.card.stock-status`
Fields:
- product_name
- stock_remaining
- threshold
- is_low_stock
- suggested_action_optional

Actions:
- Order draft dikhao
- Abhi nahi

### `cmp.card.reorder-draft`
Fields:
- supplier_name
- items[]
- estimated_total
- reason
- approval_required

Actions:
- Approve order
- Change quantity
- Cancel

### `cmp.card.khata-update`
Fields:
- customer_name
- old_balance
- payment_received_optional
- new_balance
- note_optional

Actions:
- Send receipt note
- Done

### `cmp.card.photo-extraction`
Fields:
- image_thumbnail
- extracted_items[]
- confidence_notes[]
- unresolved_items[]

Actions:
- Confirm stock add
- Edit
- Cancel

### `cmp.card.daily-summary`
Fields:
- sales_total
- cash_total
- credit_total
- dues_received
- pending_dues_count
- low_stock_items[]
- recommendation_line

Actions:
- Voice mein sunao
- Detail bhejo
- Theek hai

### `cmp.card.clarification`
Fields:
- question
- options[]
- fallback_note_optional

Actions:
- option buttons
- cancel

### `cmp.card.exception`
Fields:
- type
- severity
- description
- related_shop
- suggested_next_action

Actions:
- Resolve
- Open session
- Ignore

### `cmp.card.metric-kpi`
Fields:
- label
- value
- delta_optional
- status_optional

### `cmp.card.truth-panel-item`
Fields:
- label
- category
- description_optional

### `cmp.card.audit-step`
Fields:
- step_number
- timestamp
- agent_name
- action
- confidence_band
- memory_used[]
- state_changes[]
- status

---

## 3.5 Observer-specific components

### `cmp.observer.live-canvas`
Three-pane layout:
- left snapshot
- center mobile embed
- right orchestration timeline

### `cmp.observer.timeline-row`
Fields:
- time
- agent_name
- action_summary
- confidence_band
- status_chip

### `cmp.observer.memory-panel`
Tabs:
- shop
- customers
- products
- suppliers
- learned patterns

### `cmp.observer.before-after-comparison`
### `cmp.observer.roi-estimator`
### `cmp.observer.truth-panel`

---

## 3.6 Partner dashboard components

### `cmp.partner.portfolio-table`
Columns:
- shop
- status
- health
- last active
- exceptions
- actions

### `cmp.partner.wizard-shell`
Includes:
- title
- helper copy
- stepper
- body
- sticky footer

### `cmp.partner.health-feed`
Event types:
- bill created
- stock low
- reorder awaiting approval
- summary delivered
- clarification unresolved

### `cmp.partner.context-tabs`
Tabs:
- products
- customers
- suppliers
- preferences
- learned memory

### `cmp.partner.exception-table`
### `cmp.partner.rule-builder-row`

---

## 3.7 Feedback and system components

### `cmp.system.toast`
Examples:
- Changes saved
- Shop is live
- Rule updated

### `cmp.system.banner`
Examples:
- This action is simulated in v1
- Sandbox state only
- Low-confidence extraction needs review

### `cmp.system.modal`
Use for:
- reset demo
- reset shop state
- discard changes

### `cmp.system.loading-state`
Examples:
- Transcribing voice note…
- Extracting items from photo…
- Generating summary…

---

# 4. Card types and exact field models

## Card Type 1 — Welcome Card
**ID:** `cmp.card.info.welcome`

Fields:
- title
- body
- quick_actions[]

## Card Type 2 — Voice Review Card
**ID:** `cmp.card.voice-review`

Fields:
- transcript
- detected_customer
- detected_items[]
- payment_mode
- confidence_band
- actions[]

## Card Type 3 — Bill Preview Card
**ID:** `cmp.card.bill-preview`

Fields:
- customer_name
- items[] = `{name, qty, unit, price}`
- subtotal
- payment_mode
- approval_reason_optional
- actions[]

## Card Type 4 — Stock Status Card
**ID:** `cmp.card.stock-status`

Fields:
- product_name
- stock_remaining
- stock_unit
- threshold
- is_low_stock
- suggested_action_optional
- actions[]

## Card Type 5 — Reorder Draft Card
**ID:** `cmp.card.reorder-draft`

Fields:
- supplier_name
- items[]
- estimated_total
- reason
- approval_required
- actions[]

## Card Type 6 — Khata Update Card
**ID:** `cmp.card.khata-update`

Fields:
- customer_name
- old_balance
- payment_received_optional
- new_balance
- follow_up_optional
- actions[]

## Card Type 7 — Photo Extraction Card
**ID:** `cmp.card.photo-extraction`

Fields:
- image_ref
- extracted_items[]
- low_confidence_items[]
- actions[]

## Card Type 8 — Daily Summary Card
**ID:** `cmp.card.daily-summary`

Fields:
- sales_total
- cash_total
- credit_total
- dues_received
- pending_dues_count
- low_stock_items[]
- recommendation
- actions[]

## Card Type 9 — Clarification Card
**ID:** `cmp.card.clarification`

Fields:
- question
- options[]
- context_note_optional
- actions[]

## Card Type 10 — Exception Card
**ID:** `cmp.card.exception`

Fields:
- exception_type
- severity
- description
- recommended_fix
- actions[]

## Card Type 11 — KPI Card
**ID:** `cmp.card.metric-kpi`

Fields:
- label
- value
- secondary_optional
- trend_optional

## Card Type 12 — Audit Step Card
**ID:** `cmp.card.audit-step`

Fields:
- step_number
- timestamp
- agent_name
- action
- confidence_band
- memory_used[]
- state_changes[]
- status

---

# 5. Stepper states and interaction rules

## Step states
- locked
- available
- current
- completed
- warning
- error
- skipped
- disabled

## Meanings
- `locked` — cannot enter yet
- `available` — reachable but not started
- `current` — active step
- `completed` — validation passed
- `warning` — passable, but recommendations missing
- `error` — validation failed
- `skipped` — optional step skipped
- `disabled` — intentionally unavailable in v1

## Default transition flow
`locked → available → current → completed`

## Validation failure flow
`current → error`

## Partial but acceptable
`current → warning → completed`

## Navigation rules
- can go backward to completed steps
- cannot jump forward into locked steps
- Continue disabled on error
- Continue enabled on warning, but show prompt

## Stepper visuals
- locked: muted number
- available: plain number
- current: emphasized highlight
- completed: checkmark
- warning: amber dot/icon
- error: red icon
- disabled: grey label

## Step-level validation examples

### Step 1 — Basic details
Required:
- shop_name
- owner_name
- phone_number
- city
- language
- summary_time

### Step 2 — Bundle
Required:
- kirana core bundle selected

### Step 3 — Catalog
Required:
- at least 10 products  
Warning:
- no reorder thresholds

### Step 4 — Customers
Required:
- at least 1 customer if khata enabled  
Warning:
- no phone numbers

### Step 5 — Suppliers
Required:
- at least 1 supplier  
Warning:
- no preferred supplier mapped

### Step 6 — Rules
Required:
- language/tone selected
- bill approval threshold set

### Step 7 — Sandbox
Required:
- at least 1 test run

### Step 8 — Go Live
Required:
- all previous steps completed

---

# 6. Button hierarchy

## 1. Primary button
Use for the single main action on a page/card.

Examples:
- Continue
- Go live
- Confirm bill
- Approve order
- Run test

States:
- default
- hover
- pressed
- focus
- disabled
- loading

## 2. Secondary button
Examples:
- Back
- Edit items
- Back to sandbox
- View in chat

## 3. Tertiary button
Examples:
- Save draft
- Open memory
- Preview script

## 4. Destructive button
Examples:
- Reset all
- Cancel bill
- Discard changes
- Delete rule

## 5. Quick reply chip
Examples:
- Haan
- Nahi
- Ram bhai
- Hotel Ram
- Theek hai

## 6. Inline text action
Examples:
- Edit
- Replay
- Show raw input
- Download log

## 7. Icon-only button
Examples:
- attach
- voice record
- close modal
- open drawer

## Size variants
- large
- medium
- small
- chip

## Loading label rules
Use meaningful loading copy:
- Running test…
- Going live…
- Saving changes…
- Generating summary…

---

# 7. Message states

## 7.1 User-originated message states

### Text message lifecycle
- draft
- sent
- received
- parsing
- linked_to_action
- failed

### Voice-note lifecycle
- recording
- uploading
- transcribing
- received
- parsing
- linked_to_action
- failed

### Image/photo lifecycle
- uploading
- extracting
- preview_ready
- confirmed
- failed

## 7.2 Assistant response states

### Informational response lifecycle
- drafting
- ready
- shown

### Operational response lifecycle
- draft_ready
- awaiting_approval
- approved
- executing
- completed
- cancelled
- failed

### Clarification response lifecycle
- clarification_needed
- clarification_shown
- clarification_resolved
- cancelled

## 7.3 State transition examples

### Example A — voice bill
`recording → uploading → transcribing → received → parsing → draft_ready → awaiting_approval → approved → executing → completed`

### Example B — ambiguous customer
`received → parsing → clarification_needed → clarification_shown → clarification_resolved → draft_ready → awaiting_approval → approved → completed`

### Example C — invoice photo
`uploading → extracting → preview_ready → confirmed → executing → completed`

## 7.4 Visual treatment rules
- parsing/transcribing/extracting/drafting show subtle animated loading
- awaiting_approval shows persistent status chip and CTA
- completed shows success mark + outcome
- failed shows retry option
- clarification_needed shows concise options

## 7.5 Timeouts and edge cases
If transcription is slow:
- “Voice note process kar raha hoon… thoda wait karein.”

If extraction is low confidence:
- show editable preview rather than hard fail

If action cannot proceed:
- show “Mujhe confirm karna hoga” rather than generic error

---

# 8. Audit event schema

## 8.1 Event envelope
```json
{
  "event_id": "evt_01JH1Q4Y8M8P3T2B4C5D6E7F8G",
  "event_name": "evt.ai.bill_drafted",
  "event_version": "1.0",
  "occurred_at": "2026-03-15T10:14:33.421Z",
  "environment": "prototype",
  "prototype_mode": "observer_live_canvas",
  "scenario_id": "scenario_morning_rush_billing",
  "session_id": "sess_shop_001_20260315_101400",
  "correlation_id": "corr_bill_credit_inventory_001",
  "trace_id": "trace_001",
  "shop_id": "shop_shree_ganesh_kirana",
  "actor": {
    "role": "system",
    "id": "agent_billing",
    "display_name": "Billing Agent"
  },
  "channel": "voice",
  "screen_id": "screen_24_bill_preview",
  "severity": "info",
  "simulated": false,
  "confidence_band": "medium",
  "approval_required": true,
  "payload": {},
  "state_before": {},
  "state_after": {},
  "ui_output_ref": "card_bill_preview_001"
}
```

## 8.2 Required fields
- event_id
- event_name
- event_version
- occurred_at
- environment
- scenario_id
- session_id
- correlation_id
- shop_id
- actor
- channel
- screen_id
- severity
- simulated
- payload

## 8.3 Optional but recommended
- confidence_band
- approval_required
- state_before
- state_after
- ui_output_ref
- trace_id

## 8.4 Actor roles
Allowed:
- shopkeeper
- partner
- observer
- admin
- system
- agent_orchestrator
- agent_billing
- agent_inventory
- agent_khata
- agent_procurement
- agent_summary
- agent_memory

## 8.5 Severity levels
- debug
- info
- warning
- error
- critical

## 8.6 Event domains and examples
### UI / navigation
- evt.ui.role_selected
- evt.ui.scenario_started
- evt.ui.screen_viewed
- evt.ui.drawer_opened

### Partner onboarding
- evt.partner.shop_created
- evt.partner.bundle_selected
- evt.partner.catalog_item_added
- evt.partner.customer_added
- evt.partner.supplier_added
- evt.partner.rules_saved
- evt.partner.sandbox_test_run
- evt.partner.shop_deployed_live

### Shopkeeper input
- evt.shopkeeper.message_text_sent
- evt.shopkeeper.voice_note_uploaded
- evt.shopkeeper.image_uploaded
- evt.shopkeeper.quick_reply_selected

### AI and routing
- evt.ai.transcription_completed
- evt.ai.intent_detected
- evt.ai.memory_lookup_performed
- evt.ai.agent_routed
- evt.ai.bill_drafted
- evt.ai.inventory_adjusted
- evt.ai.khata_updated
- evt.ai.reorder_draft_created
- evt.ai.daily_summary_generated

### Safety / control
- evt.approval.requested
- evt.approval.approved
- evt.approval.rejected
- evt.clarification.requested
- evt.clarification.resolved
- evt.exception.queued
- evt.exception.resolved

### Demo/admin
- evt.demo.state_reset
- evt.demo.seed_data_loaded
- evt.demo.scenario_restarted

## 8.7 Payload examples

### Intent detected
```json
{
  "raw_input": "Ram ko 2 kilo chawal, 1 tel aur 3 biscuit ka bill bana do. Udhar mein daal do.",
  "normalized_input": "Create bill for Ram bhai with 2 kg regular rice, 1 sunflower oil, 3 Parle-G on credit.",
  "detected_intents": [
    "create_bill",
    "update_inventory",
    "update_khata"
  ],
  "candidate_entities": {
    "customer": ["Ram bhai"],
    "products": ["Regular chawal", "Sunflower oil 1L", "Parle-G"],
    "payment_mode": "credit"
  }
}
```

### Bill drafted
```json
{
  "customer_id": "cust_ram_bhai",
  "items": [
    {"product_id": "prod_regular_rice_loose", "qty": 2, "unit": "kg", "price": 60},
    {"product_id": "prod_sunflower_oil_1l", "qty": 1, "unit": "pc", "price": 160},
    {"product_id": "prod_parle_g_small", "qty": 3, "unit": "pc", "price": 10}
  ],
  "bill_total": 310,
  "payment_mode": "credit"
}
```

### Clarification requested
```json
{
  "ambiguity_type": "customer_name",
  "input_text": "Ram ka balance batao",
  "candidates": [
    {"customer_id": "cust_ram_bhai", "display_name": "Ram bhai"},
    {"customer_id": "cust_hotel_ram", "display_name": "Hotel Ram"}
  ],
  "question_shown": "2 customers mile. Kaunsa wala?"
}
```

## 8.8 State before / after strategy
Only include changed state.

Example:
```json
{
  "state_before": {
    "inventory": {"prod_sunflower_oil_1l": 5},
    "khata": {"cust_ram_bhai": 1850}
  },
  "state_after": {
    "inventory": {"prod_sunflower_oil_1l": 4},
    "khata": {"cust_ram_bhai": 2160}
  }
}
```

---

# 9. Seeded data JSON

```json
{
  "meta": {
    "seed_version": "1.0",
    "prototype_name": "Rupantar Horizon 1 Prototype - Kirana Ops",
    "vertical": "kirana",
    "default_language": "Hinglish",
    "generated_for": "observer_partner_shopkeeper_demo"
  },
  "shops": [
    {
      "shop_id": "shop_shree_ganesh_kirana",
      "shop_name": "Shree Ganesh Kirana",
      "owner_name": "Ramesh Patel",
      "phone_number": "+919876543210",
      "city": "Surat",
      "language": "Hinglish",
      "vertical": "kirana",
      "gst_status": "non_gst",
      "business_hours": {"open": "08:00", "close": "22:00"},
      "summary_time": "21:00",
      "deployment_status": "live",
      "assistant_name": "Rupantar Assistant",
      "active_agents": [
        "orchestrator",
        "billing",
        "inventory",
        "khata",
        "procurement",
        "daily_summary",
        "memory"
      ],
      "rules": {
        "bill_approval_threshold_inr": 500,
        "reorder_requires_approval": true,
        "credit_reminder_after_days": 7,
        "clarify_ambiguous_customer": true,
        "clarify_ambiguous_product": true,
        "summary_tone": "hinglish",
        "send_daily_summary_at": "21:00"
      }
    }
  ],
  "products": [
    {
      "product_id": "prod_basmati_rice_5kg",
      "display_name": "Basmati Rice 5kg",
      "aliases": ["basmati", "chawal basmati", "rice basmati"],
      "category": "grains",
      "unit_type": "piece",
      "pack_size": "5kg",
      "selling_price": 690,
      "current_stock": 3,
      "reorder_threshold": 6,
      "reorder_quantity": 12,
      "preferred_supplier_id": "sup_bharat_traders"
    },
    {
      "product_id": "prod_regular_rice_loose",
      "display_name": "Regular Chawal Loose",
      "aliases": ["chawal", "regular chawal", "loose rice"],
      "category": "grains",
      "unit_type": "kg",
      "pack_size": "loose",
      "selling_price": 60,
      "current_stock": 42,
      "reorder_threshold": 20,
      "reorder_quantity": 50,
      "preferred_supplier_id": "sup_bharat_traders"
    },
    {
      "product_id": "prod_atta_10kg",
      "display_name": "Atta 10kg",
      "aliases": ["atta", "gehun atta"],
      "category": "grains",
      "unit_type": "piece",
      "pack_size": "10kg",
      "selling_price": 420,
      "current_stock": 8,
      "reorder_threshold": 5,
      "reorder_quantity": 15,
      "preferred_supplier_id": "sup_bharat_traders"
    },
    {
      "product_id": "prod_sugar_1kg",
      "display_name": "Sugar 1kg",
      "aliases": ["chini", "sugar"],
      "category": "grains",
      "unit_type": "piece",
      "pack_size": "1kg",
      "selling_price": 46,
      "current_stock": 26,
      "reorder_threshold": 12,
      "reorder_quantity": 24,
      "preferred_supplier_id": "sup_bharat_traders"
    },
    {
      "product_id": "prod_sunflower_oil_1l",
      "display_name": "Sunflower Oil 1L",
      "aliases": ["sunflower tel", "oil", "tel", "refined oil"],
      "category": "oil",
      "unit_type": "piece",
      "pack_size": "1L",
      "selling_price": 160,
      "current_stock": 4,
      "reorder_threshold": 6,
      "reorder_quantity": 12,
      "preferred_supplier_id": "sup_bharat_traders"
    },
    {
      "product_id": "prod_groundnut_oil_1l",
      "display_name": "Groundnut Oil 1L",
      "aliases": ["groundnut tel", "peanut oil", "tel"],
      "category": "oil",
      "unit_type": "piece",
      "pack_size": "1L",
      "selling_price": 175,
      "current_stock": 9,
      "reorder_threshold": 5,
      "reorder_quantity": 10,
      "preferred_supplier_id": "sup_bharat_traders"
    },
    {
      "product_id": "prod_toor_dal_1kg",
      "display_name": "Toor Dal 1kg",
      "aliases": ["dal", "toor dal", "arhar dal"],
      "category": "pulses",
      "unit_type": "piece",
      "pack_size": "1kg",
      "selling_price": 130,
      "current_stock": 11,
      "reorder_threshold": 6,
      "reorder_quantity": 18,
      "preferred_supplier_id": "sup_bharat_traders"
    },
    {
      "product_id": "prod_maggi_pack",
      "display_name": "Maggi Pack",
      "aliases": ["maggi", "noodles"],
      "category": "snacks",
      "unit_type": "piece",
      "pack_size": "single",
      "selling_price": 14,
      "current_stock": 36,
      "reorder_threshold": 12,
      "reorder_quantity": 48,
      "preferred_supplier_id": "sup_shiv_distributors"
    },
    {
      "product_id": "prod_parle_g_small",
      "display_name": "Parle-G Small",
      "aliases": ["parle g", "biscuit", "parleg"],
      "category": "snacks",
      "unit_type": "piece",
      "pack_size": "small",
      "selling_price": 10,
      "current_stock": 5,
      "reorder_threshold": 10,
      "reorder_quantity": 24,
      "preferred_supplier_id": "sup_shiv_distributors"
    },
    {
      "product_id": "prod_bread_britannia",
      "display_name": "Britannia Bread",
      "aliases": ["bread"],
      "category": "fresh",
      "unit_type": "piece",
      "pack_size": "1 loaf",
      "selling_price": 45,
      "current_stock": 7,
      "reorder_threshold": 6,
      "reorder_quantity": 20,
      "preferred_supplier_id": "sup_fresh_mart_supply"
    },
    {
      "product_id": "prod_milk_500ml",
      "display_name": "Milk 500ml",
      "aliases": ["milk", "doodh"],
      "category": "fresh",
      "unit_type": "piece",
      "pack_size": "500ml",
      "selling_price": 28,
      "current_stock": 15,
      "reorder_threshold": 10,
      "reorder_quantity": 30,
      "preferred_supplier_id": "sup_fresh_mart_supply"
    },
    {
      "product_id": "prod_tea_powder_250g",
      "display_name": "Tea Powder 250g",
      "aliases": ["chai patti", "tea"],
      "category": "beverages",
      "unit_type": "piece",
      "pack_size": "250g",
      "selling_price": 95,
      "current_stock": 10,
      "reorder_threshold": 5,
      "reorder_quantity": 15,
      "preferred_supplier_id": "sup_shiv_distributors"
    },
    {
      "product_id": "prod_detergent_1kg",
      "display_name": "Detergent 1kg",
      "aliases": ["detergent", "powder"],
      "category": "homecare",
      "unit_type": "piece",
      "pack_size": "1kg",
      "selling_price": 120,
      "current_stock": 9,
      "reorder_threshold": 4,
      "reorder_quantity": 12,
      "preferred_supplier_id": "sup_shiv_distributors"
    },
    {
      "product_id": "prod_bath_soap",
      "display_name": "Bath Soap",
      "aliases": ["soap", "sabun"],
      "category": "personalcare",
      "unit_type": "piece",
      "pack_size": "single",
      "selling_price": 35,
      "current_stock": 20,
      "reorder_threshold": 8,
      "reorder_quantity": 30,
      "preferred_supplier_id": "sup_shiv_distributors"
    }
  ],
  "customers": [
    {
      "customer_id": "cust_ram_bhai",
      "display_name": "Ram bhai",
      "aliases": ["ram", "ram bhai"],
      "phone_number": "+919999111111",
      "credit_enabled": true,
      "outstanding_balance": 1850,
      "reminder_after_days": 7,
      "approval_limit_override": null
    },
    {
      "customer_id": "cust_shyam",
      "display_name": "Shyam",
      "aliases": ["shyam bhai"],
      "phone_number": "+919999222222",
      "credit_enabled": true,
      "outstanding_balance": 450,
      "reminder_after_days": 5,
      "approval_limit_override": null
    },
    {
      "customer_id": "cust_meena_aunty",
      "display_name": "Meena aunty",
      "aliases": ["meena"],
      "phone_number": null,
      "credit_enabled": false,
      "outstanding_balance": 0,
      "reminder_after_days": 0,
      "approval_limit_override": null
    },
    {
      "customer_id": "cust_hotel_ganesh",
      "display_name": "Hotel Ganesh",
      "aliases": ["hotel", "ganesh hotel"],
      "phone_number": "+919999333333",
      "credit_enabled": true,
      "outstanding_balance": 5200,
      "reminder_after_days": 10,
      "approval_limit_override": 2500
    },
    {
      "customer_id": "cust_hotel_ram",
      "display_name": "Hotel Ram",
      "aliases": ["ram hotel", "ram"],
      "phone_number": "+919999444444",
      "credit_enabled": true,
      "outstanding_balance": 900,
      "reminder_after_days": 10,
      "approval_limit_override": null
    }
  ],
  "suppliers": [
    {
      "supplier_id": "sup_bharat_traders",
      "supplier_name": "Bharat Traders",
      "phone_number": "+918888111111",
      "categories_supplied": ["grains", "oil", "pulses"],
      "lead_time_days": 1,
      "preferred_for_products": [
        "prod_basmati_rice_5kg",
        "prod_regular_rice_loose",
        "prod_atta_10kg",
        "prod_sugar_1kg",
        "prod_sunflower_oil_1l",
        "prod_groundnut_oil_1l",
        "prod_toor_dal_1kg"
      ]
    },
    {
      "supplier_id": "sup_shiv_distributors",
      "supplier_name": "Shiv Distributors",
      "phone_number": "+918888222222",
      "categories_supplied": ["snacks", "beverages", "homecare", "personalcare"],
      "lead_time_days": 2,
      "preferred_for_products": [
        "prod_maggi_pack",
        "prod_parle_g_small",
        "prod_tea_powder_250g",
        "prod_detergent_1kg",
        "prod_bath_soap"
      ]
    },
    {
      "supplier_id": "sup_fresh_mart_supply",
      "supplier_name": "Fresh Mart Supply",
      "phone_number": "+918888333333",
      "categories_supplied": ["fresh"],
      "lead_time_days": 1,
      "preferred_for_products": [
        "prod_bread_britannia",
        "prod_milk_500ml"
      ]
    }
  ],
  "memory": [
    {
      "entity_type": "shop",
      "memory_key": "preferred_language",
      "memory_value": "Hinglish",
      "source": "config",
      "last_used_at": "2026-03-15T10:00:00Z"
    },
    {
      "entity_type": "shop",
      "memory_key": "summary_time",
      "memory_value": "21:00",
      "source": "config",
      "last_used_at": "2026-03-15T10:00:00Z"
    },
    {
      "entity_type": "customer",
      "memory_key": "cust_ram_bhai_usually_credit",
      "memory_value": "Ram bhai usually buys on credit.",
      "source": "learned",
      "last_used_at": "2026-03-15T10:15:00Z"
    },
    {
      "entity_type": "product",
      "memory_key": "alias_tel_ambiguous",
      "memory_value": "The word 'tel' may refer to sunflower oil or groundnut oil.",
      "source": "inferred",
      "last_used_at": "2026-03-15T10:16:00Z"
    },
    {
      "entity_type": "product",
      "memory_key": "alias_chawal_prefers_regular",
      "memory_value": "When user says 'chawal' in small basket billing, prefer regular loose rice unless otherwise specified.",
      "source": "learned",
      "last_used_at": "2026-03-15T10:14:00Z"
    }
  ],
  "daily_state": {
    "date": "2026-03-15",
    "sales_total": 8540,
    "cash_total": 5900,
    "credit_total": 2640,
    "dues_received": 500,
    "pending_dues_customers": ["cust_ram_bhai", "cust_shyam", "cust_hotel_ram"],
    "low_stock_products": ["prod_sunflower_oil_1l", "prod_parle_g_small"],
    "recommendation": "Kal subah Bharat Traders ko order draft approve karna useful rahega."
  },
  "chat_seed": {
    "welcome_message": {
      "message_id": "msg_welcome_001",
      "sender": "assistant",
      "type": "text",
      "text": "Namaste Ramesh bhai 👋 Main aapka Rupantar Assistant hoon. Aap mujhe voice note ya message bhej sakte ho. Main bill bana sakta hoon, stock check kar sakta hoon, khata update kar sakta hoon, aur aaj ka summary bhej sakta hoon.",
      "timestamp": "2026-03-15T09:00:00Z"
    },
    "quick_actions": ["Bill banao", "Stock check", "Khata dekho", "Aaj ka summary"]
  }
}
```

---

# 10. Interaction rules tying it together

## Rule 1 — Every operational chat action must end in a card
One of:
- bill preview
- stock/reorder
- khata update
- photo extraction
- clarification
- daily summary

## Rule 2 — Every important card must expose next steps clearly
No hidden critical actions.

## Rule 3 — The shopkeeper never sees agent names
Observer/admin may.

## Rule 4 — Approval-required actions remain persistent in-thread
They should not disappear after new messages arrive.

## Rule 5 — Clarification beats guessing
If ambiguity exists and confidence is low, ask a question rather than guessing.

## Rule 6 — Partner edits should be testable before going live
Every context or rule change should support:
- save
- retest in sandbox
- push live

## Rule 7 — Observer mode should always explain “why”
At minimum:
- intent
- agent used
- memory used
- confidence
- approval state
- result
