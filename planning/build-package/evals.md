# Evaluation Guide — Rupantar H1 Prototype

The prototype is evaluated across three tiers. All three must pass before the prototype is considered demo-ready.

---

## Tier 1 — Product Truth

*Can each role complete their core job?*

### Shopkeeper eval
Run these with a fresh tester who has not seen the prototype before:

| Test | Pass condition |
|---|---|
| Complete a voice bill with no coaching | Tester creates a bill and confirms it within 3 attempts |
| Ask a stock question | Correct stock shown; low-stock warning appears if applicable |
| Record a payment | Khata balance updates correctly |
| Handle an ambiguous input | Tester selects from clarification options without confusion |
| Receive daily summary | Tester can explain what happened today from the summary card |

**Pass bar:** 4 of 5 tests pass on first attempt with a new tester.

### Partner eval
Run with someone who has read the build brief but not practiced:

| Test | Pass condition |
|---|---|
| Deploy a new shop from scratch | Shop is live in under 15 minutes |
| Modify a product price post-deployment | Price updated and pushed live |
| Identify and resolve an exception | Exception queue item resolved |
| View shop health after 5 shopkeeper interactions | Health dashboard reflects real data |

**Pass bar:** All 4 tests pass.

### Observer / investor eval
Run the 5-minute demo for someone who knows nothing about the product:

| Test | Pass condition |
|---|---|
| Can they explain the product back? | They describe it as "more than a chatbot" |
| Do they understand the partner layer? | They can articulate why it's important |
| Do they believe the state is real? | They ask about the DB, not about the demo script |

**Pass bar:** All 3 pass.

---

## Tier 2 — Engineering Truth

*Is the state model honest?*

Run this checklist after completing all 7 flows from `acceptance_criteria.md`:

| Check | How to verify |
|---|---|
| Inventory mutations are persistent | Check DB after billing: `SELECT current_stock FROM Product WHERE shop_id = 'shop_shree_ganesh_kirana'` |
| Khata balance is correct | `SELECT outstanding_balance FROM Customer WHERE display_name = 'Ram bhai'` |
| Audit events exist for every action | `SELECT COUNT(*) FROM AuditEvent WHERE session_id = '<session>'` — expect ≥ 5 per flow |
| Simulated actions are flagged | All `ReorderDraft` and `Message` with WhatsApp delivery show `simulated_sent` status |
| Demo reset is complete | After `POST /api/v1/demo/reset`, re-query all above — values should match seed values |
| API response envelope is consistent | Every API response has `{ success, data, meta: { request_id, simulated }, errors }` |

**Pass bar:** All 6 checks pass.

---

## Tier 3 — Demo Truth

*Can you run a confident demo?*

### 5-minute demo checklist

Run the demo 3 times in a row without touching seed data between runs:

- [ ] Run 1: voice bill → ambiguity → confirm → stock update
- [ ] Run 2: low stock → reorder approval
- [ ] Run 3: payment received → daily summary

**Pass bar:** All 3 runs complete without a dead screen, loading error, or manual database patch.

### 15-minute walkthrough checklist

- [ ] Shopkeeper journey (voice bill, payment, summary) — 4.5 min
- [ ] Partner deployment journey (wizard → go-live) — 3 min
- [ ] Trust / memory / explainability (audit trail, memory inspector) — 2.5 min
- [ ] Beyond happy path (ambiguity flow, clarification) — 2 min
- [ ] Business/distribution lens (shop health, portfolio) — 1.5 min
- [ ] Real vs simulated honesty panel — 1.5 min

**Pass bar:** All 6 sections complete with real data and no fabricated screens.

### Reset reliability

- [ ] `POST /api/v1/demo/reset` with `{ reload_seed_data: true }` completes in ≤ 10 seconds
- [ ] All 7 flows can run again from clean state immediately after reset

---

## What "demo-ready" means

The prototype is demo-ready when:
- Tier 1: Product truth — all role evals pass
- Tier 2: Engineering truth — all 6 DB checks pass
- Tier 3: Demo truth — 5-min demo runs 3x clean + reset works

**Not required for demo-readiness:**
- 100% of the 31 screens built (15 critical-path screens suffice)
- Real Claude adapter wired (fixtures are sufficient)
- Multi-language toggle working
- Production-grade error handling

---

## Prototype-to-pilot readiness (next threshold)

The prototype graduates to a pilot when:
- At least 3 real kirana owners have completed Flow 1 and Flow 4 on their own phones
- At least 1 partner has deployed a real shop (not seeded data)
- Demo reset is replaced by a real multi-shop data model
- Real WhatsApp Business API is wired (even for 1 test number)
