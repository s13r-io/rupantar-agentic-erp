# UI Style Brief — Rupantar H1 Prototype

## Design intent

Modern, clean, demo-friendly enterprise UI. The prototype must feel like a real product at a quick glance, not a developer scaffold. Two distinct visual registers: shopkeeper (warm, conversational) and partner/observer (neutral, professional).

---

## Color palette

| Role | Primary accent | Background | Surface |
|---|---|---|---|
| Shopkeeper chat | Green — `#25D366` (WhatsApp-inspired, not exact) | `#ECE5DD` (WhatsApp chat bg) | White message bubbles |
| Partner console | Slate — `#1E293B` for nav | `#F8FAFC` (off-white) | White cards |
| Observer canvas | Neutral gray | `#F1F5F9` | White panels |
| System status chips | Green = live · Yellow = pending · Red = failed · Blue = simulated | | |

Brand accent (Rupantar): `#16A34A` (green-600 in Tailwind). Use for primary CTAs, active nav, confirmation states.

---

## Typography

- Font: `Inter` (Google Fonts, already in Next.js defaults)
- Body: 14px / `text-sm`
- Labels and chips: 12px / `text-xs`
- Card headings: 16px / `text-base font-semibold`
- Page headings: 20–24px / `text-xl font-bold`
- Monospace (logs, JSON): `font-mono text-xs`

---

## Density and layout

- Partner/Observer: desktop 1440px wide, content max-width `1200px`, `gap-4` grid
- Shopkeeper: mobile frame `390×844px` rendered inside a desktop shell for demos
- Cards: `rounded-xl`, `shadow-sm`, `p-4`, no border unless interactive
- Form fields: `rounded-lg`, `border border-slate-200`
- Use cards over tables wherever possible (doc 02 principle)

---

## Chat / shopkeeper specifics

- Assistant bubble: white, left-aligned, `rounded-2xl rounded-tl-none`
- User bubble: green-100, right-aligned, `rounded-2xl rounded-tr-none`
- Timestamp: `text-xs text-slate-400` below each bubble
- Quick reply chips: outlined, `rounded-full`, green border, small
- Action cards (bill preview, stock card, etc.): white card with green header strip, full-width in thread
- Voice note: waveform placeholder (static SVG), play button, duration label

---

## Interaction states (for all clickable elements)

- Default → Hover: subtle `bg-slate-50` lift
- Active/selected: green-600 border or background
- Disabled: `opacity-40 cursor-not-allowed`
- Loading: shadcn/ui Skeleton component

---

## Status chip colors

| Status | Color |
|---|---|
| Live | `bg-green-100 text-green-700` |
| Sandbox | `bg-blue-100 text-blue-700` |
| Draft | `bg-slate-100 text-slate-600` |
| Needs approval | `bg-yellow-100 text-yellow-700` |
| Clarification needed | `bg-orange-100 text-orange-700` |
| Low confidence | `bg-red-100 text-red-600` |
| Completed | `bg-green-50 text-green-600` |
| Simulated | `bg-purple-100 text-purple-600` |

---

## What to avoid

- Dark mode (not in scope for v1)
- Heavy drop shadows or glassmorphism
- Animations beyond `transition-colors duration-150`
- Exact WhatsApp clone (inspired by, not replica — avoids IP issues)
- Icon-only navigation (always pair icons with labels in partner/observer)
