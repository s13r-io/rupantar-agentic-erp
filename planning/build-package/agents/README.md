# Agent Prompts — Rupantar H1 Prototype

Specialized Claude Code prompts for **review phases** during the build. They supplement the sprint prompts — they do not replace them.

---

## Usage

1. Open a Claude Code session in the **app repo** (`rupantar-h1-prototype`)
2. Paste the contents of `build_brief.md` first (same as sprint workflow)
3. Paste the contents of the relevant agent prompt file
4. Let the agent run its checklist and produce its report

---

## When to use each agent

| Agent | File | When | Duration | Required? |
|---|---|---|---|---|
| Sprint Reviewer | `sprint_reviewer.md` | After completing Sprint N, before starting Sprint N+1 | 5–10 min | Recommended |
| Eval Runner | `eval_runner.md` | After Sprint 4, before declaring demo-ready | 20–30 min | **Required** |
| UI Auditor | `ui_auditor.md` | After Sprint 4 polish; optionally after Sprint 1 or 2 | 10–15 min | Recommended |

---

## Recommended workflow

```
Sprint 0 → Sprint Reviewer → Sprint 1 → Sprint Reviewer → Sprint 2 → Sprint Reviewer →
Sprint 3 → Sprint Reviewer → Sprint 4 → UI Auditor → Eval Runner → Demo Ready
```

---

## Agents NOT included (and why)

| Agent | Why excluded |
|---|---|
| **Architect** | `build_brief.md` already serves as architectural context. A separate architect agent would create conflicting guidance. |
| **Code Reviewer** | Claude Code already reviews its own output during each sprint session. A separate reviewer would duplicate effort. |
| **Testing Agent** | The Eval Runner covers post-build verification. Development-time unit tests are out of scope for a 20-hour prototype. |
| **Fixture Designer** | `fixture_map.md` already specifies all fixture mappings. The developer implements them directly — no separate agent needed. |
