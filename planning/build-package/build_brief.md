# Rupantar H1 Prototype — Build Brief

**Paste this file at the start of every Claude Code session before any sprint prompt.**

---

## What you are building

**Rupantar Horizon 1 Prototype — Kirana Ops**

A browser-based prototype proving that:
1. A kirana owner can run daily operations through a WhatsApp-like interface using voice, text, and photos
2. A partner (AI Shop Doctor) can configure and deploy the assistant without engineers
3. The system behaves like an operational assistant — not a chatbot — with real state mutations, confidence-gated approvals, and a full audit trail
4. Horizon 1 can start with a kirana wedge and still feel credible to investors and partners

This is **not** a production system. It is a **demo-reliable prototype** with real business logic and simulated external integrations.

---

## Tech stack — locked, do not deviate

| Layer | Choice |
|---|---|
| Framework | Next.js 14 (App Router) + TypeScript |
| UI | Tailwind CSS + shadcn/ui |
| State | Zustand (5 stores: session, partnerWizard, observer, audit, ui) |
| API | Next.js Route Handlers under `/app/api/v1/` |
| ORM | Prisma |
| Database | PostgreSQL via Neon (use `DATABASE_URL` env var) |
| Auth | No-auth; role passed via URL param `?role=shopkeeper\|partner\|observer\|admin` |
| AI adapters | Fixture-first; real API toggled via `NEXT_PUBLIC_USE_REAL_AI=true` env var |

**Do not introduce:** NestJS, Express, separate backend process, turborepo, Redux, XState, SQLite, Supabase Auth.

---

## Repo structure

```
/app
  /api/v1/           ← All Route Handlers
  /(roles)
    /shopkeeper/     ← Mobile chat UI
    /partner/        ← Partner console
    /observer/       ← Demo canvas
    /admin/          ← Reset + session inspector
  /page.tsx          ← Role selector (landing)
/components
  /chat/             ← Chat shell + message types + cards
  /partner/          ← Wizard steps + forms
  /observer/         ← Canvas + audit + memory panels
  /ui/               ← shadcn/ui re-exports + custom foundations
/lib
  /services/         ← billing.ts, inventory.ts, khata.ts, procurement.ts, summary.ts
  /adapters/         ← voice.ts, invoice.ts, intent.ts (fixture + real API overlay)
  /stores/           ← Zustand store files
  /fixtures/         ← Seeded scenario JSON files
  /seed/             ← seed.ts (Prisma seed script)
/prisma
  /schema.prisma
```

---

## Real vs simulated — hard boundary

| Capability | Mode |
|---|---|
| Shop/product/customer/supplier CRUD | Real |
| Billing calculations | Real |
| Inventory stock mutations | Real |
| Khata balance updates | Real |
| Reorder draft generation | Real |
| Daily summary calculation | Real |
| Audit event logging | Real |
| Rule storage + enforcement | Real |
| Voice transcription | Hybrid (fixture default, real Deepgram STT or browser Web Speech API optional) |
| Intent detection | Hybrid (fixture default, real Claude Haiku API optional) |
| Invoice/photo extraction | Hybrid (fixture default, real Claude Sonnet with vision optional) |
| WhatsApp delivery | Simulated — status: `simulated_sent` |
| Supplier message send | Simulated — status: `draft_created` |
| UPI payment confirmation | Simulated |
| Offline sync | Out of scope |

**Rule:** Every simulated action must carry `"simulated": true` in its API response meta field.

---

## API conventions

- Prefix: `/api/v1/`
- Style: JSON REST
- Envelope:
  ```json
  { "success": true, "data": {}, "meta": { "request_id": "...", "simulated": false }, "errors": [] }
  ```
- Error codes use SCREAMING_SNAKE_CASE: `PRODUCT_NOT_FOUND`, `AMBIGUOUS_CUSTOMER`

---

## Seed data

Demo shop: **Shree Ganesh Kirana** · Owner: Ramesh Patel · City: Surat · Language: Hinglish

Key customers: Ram bhai (₹1,850 outstanding), Shyam (₹450), Meena aunty (cash), Hotel Ganesh, Hotel Ram  
Key products: Basmati rice 5kg, Regular rice loose, Atta 10kg, Sugar 1kg, Sunflower oil 1L, Groundnut oil 1L, Toor dal, Maggi, Parle-G, Bread, Milk, Tea powder  
Ambiguity seeds: "chawal" → 2 products · "tel" → 2 products · "Ram" → 2 customers  
Rules: bill > ₹500 needs approval · reorder always needs approval · daily summary time stored as 9 PM (manual trigger only in H1 — no server-side cron)

---

## What is out of scope for this prototype

Do not build: 160+ agent library · multi-vertical rollout · Pro Code SDK · marketplace · ONDC/ABDM/GST integrations · live UPI reconciliation · production offline sync · full multilingual robustness · production observability stack.

These may appear as greyed-out roadmap items in the UI but must not be implemented.

---

## Reference documents

All spec documents are in `planning/horizon1_markdown_docs/` relative to the parent repo:
- `02_prototype_blueprint.md` — screen list, role flows, demo scenarios
- `03_wireframe_spec.md` — exact UI copy, field definitions, Hinglish text
- `04_component_inventory_and_interaction_spec.md` — component names, state machines, seed data JSON
- `05_developer_handoff_packet.md` — API contracts, Prisma entity list, state machine diagrams

Also in this build-package:
- `ui_style_brief.md` — colors, typography, density, chat bubble spec
- `acceptance_criteria.md` — checkbox-level done criteria for all 7 demo flows
- `data_model_reference.md` — Prisma schema quick-reference, relationships, seed data IDs
- `fixture_map.md` — exact adapter input→output mappings + Hinglish copy registry
- `sprint_dependencies.md` — what each sprint produces/consumes, do-not-break contracts
- `agents/` — post-sprint review agents (sprint reviewer, eval runner, UI auditor)
