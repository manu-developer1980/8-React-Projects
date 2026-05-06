# BRIEF — p01-ops-dashboard (operations / sales dashboard)

**Stack:** React + **Vite** + **Tailwind CSS 4** (no exceptions).

Goal: lock scope, decisions, and **edge cases** for a portfolio-ready MVP; avoid perfectionism.

**Language:** all user-facing copy, mock data, and README for this app are **English**.

---

## 1. One-line summary

**Shippable outcome:**  
A **front-end only** operations dashboard with **5 KPIs** (sales + progress vs target + a light inventory signal), an **orders table** filterable by **text** (customer / id / reference) and **date range**, backed by coherent **in-memory mock data**.

---

## 2. Context and motivation

- **Problem / opportunity:** Surface **sales**, a sense of **progress vs targets**, and a simple **inventory pressure** signal (no real ERP) to practice dense layouts, derived state, and filters.
- **Audience:** Professional portfolio; fictional user = internal ops / sales lead.
- **Why now:** Solidify modern React (hooks, derived state, table, UI states) with a closed MVP aligned with `GUIA_8_PROYECTOS.md` (project 1).

---

## 3. User stories (max 4 for MVP)

Format: *As a … I want … so that …*

| # | Story | Acceptance criteria (measurable) |
|---|-------|-----------------------------------|
| 1 | As an ops lead I want **a KPI block on load** so I can orient in seconds. | **5 cards** with numeric (or %) values and labels; at least one compares **actual vs target** for the current month (fixed mock or derived from orders). |
| 2 | As an ops lead I want to **filter the orders table by date range** (from / to) so I can narrow analysis. | Changing dates lists only orders whose `date` falls **inclusively** in the range; if the range is invalid (end \< start), show a **message** and do not apply the filter until fixed. |
| 3 | As an ops lead I want **text search** on the table to find orders by customer, id, or reference. | One search field filters `customer` (case-insensitive), order `id`, or `reference`; empty search = no text filter; **combines** with the date filter. |
| 4 | As an ops lead I want to **understand when there is no data** or filters yield zero rows so I do not mistake it for a bug. | **Global empty:** friendly message if mock ever returned no rows (avoid in seed); **zero after filters:** explicit copy e.g. “No orders match…” + hint to widen dates or clear search; optional **short simulated loading** on first paint. |

**Explicitly out of scope**

- Auth, roles, real backend, API, persistence.
- Order edit/create; **CSV export** (post-MVP “plus” per guide).
- Heavy charts, maps, real-time notifications.
- Detailed stock table (only aggregated mock KPI, e.g. integer “SKUs on low stock”).
- i18n / multiple languages (English-only UI for portfolio).

---

## 4. Critical flows (mental sketch)

1. **Happy path:** User opens app → sees layout (header + KPIs + filters + table) → mock loads (or brief skeleton) → sees default month orders → adjusts dates and/or text → table and KPIs derived from filtered subset update immediately.
2. **Secondary:** User applies filters that yield **0 rows** → reads empty-filter message → clicks “Clear filters” (or equivalent) → returns to default visible set.
3. **Correction:** User sets **end date before start date** → validation message → no recalculation until valid (no auto-swap in MVP).

---

## 5. Data and contracts

- **Source:** **Mock JSON** under `src/data/` (`orders.json`, `monthly-targets.json`, `inventory-summary.json`) imported in the app; no network fetch in MVP. Optional `setTimeout` 300–500 ms on first load to practice loading state.
- **Main entities:**

| Entity | Minimal fields | Notes |
|--------|----------------|--------|
| `Order` | `id`, `date` (ISO `YYYY-MM-DD`), `customer`, `amountEUR` (number), `status` (short enum), `reference` (string) | Table source; `status` read-only; MVP filters: dates + text only. |
| `MonthlyTarget` | `month` (`YYYY-MM`), `targetRevenueEUR`, `label` | Static list; KPI “% of revenue target” = sum of filtered or calendar-month orders / `targetRevenueEUR` (per agreed rule in README). |
| `InventorySummary` (mock) | `lowStockSkuCount` (number) | Single KPI “SKUs on low stock”; no stock grid in MVP. |

- **Validation:**  
  - Dates: `type="date"` inputs; if both set and `end < start`, show error and **do not** apply date filter until valid.  
  - If one bound empty: treat as **open** on that side (document in README).  
  - Text search: trim; no hard max; empty = no text filter.

---

## 6. UI states (required)

| Block | Empty | Loading | Error | Success |
|-------|-------|---------|-------|---------|
| KPIs | no (always mock) | optional (yes) | no | yes |
| Filters (dates + text) | n/a | no | yes (invalid range) | yes |
| Orders table | yes (zero rows) | optional (yes) | no | yes |

---

## 7. Edge cases and limits

### 7.1 Data and network

| Situation | Expected behaviour | In MVP? |
|-----------|-------------------|---------|
| Empty list | “No orders” only if global mock is empty (avoid in seed). | yes (defined) |
| Empty body but 200 | N/A (no HTTP). | no |
| Network error / timeout | N/A unless fetch is simulated; if so: message + **manual** retry button. | optional / default no |
| Unexpected response shape | N/A. | no |
| Manual vs auto retry | If failed simulated load: **manual** only. | optional |

### 7.2 User input

| Situation | Expected behaviour | In MVP? |
|-----------|-------------------|---------|
| Empty fields / no global submit | No global submit; partial dates allowed per §5. | yes |
| Very long input | No hard cap; OK up to ~500 mock orders. | yes |
| Odd chars / spaces | Trim; case-insensitive match on strings. | yes |
| Double click / double submit | No persistence; idempotent filters. | low priority |
| Paste huge text | Same search; small dataset OK in MVP. | yes |

### 7.3 Concurrency and navigation

| Situation | Expected behaviour | In MVP? |
|-----------|-------------------|---------|
| Navigate away while loading | N/A (single-view SPA). | no |
| Back with “half” data | No multi-step flow. | no |
| Refresh mid-flow | Filter state resets (acceptable); document in README. | yes |
| Deep link needing context | Single `/`; no query state in MVP. | no |

### 7.4 Performance and product limits

| Situation | Expected behaviour | In MVP? |
|-----------|-------------------|---------|
| Many rows (100, 1000) | Seed ~118 orders; client filter OK; document “virtualisation out of MVP” if it grows. | yes |
| Slow search/filter | Instant on small mock; debounce optional. | yes |

### 7.5 Minimal accessibility

| Situation | Expected behaviour | In MVP? |
|-----------|-------------------|---------|
| Keyboard only (Tab, Enter, Escape) | Tab through controls; Enter on clear; Escape not required. | yes (basic) |
| Visible focus | Tailwind `focus-visible` on inputs and buttons. | yes |
| Form / group errors legible | Invalid date range message tied to date group (`role="alert"` or adjacent text). | yes |

---

## 8. Technical decisions (tradeoffs)

| Decision | Chosen | Alternative | Why | Cost |
|----------|--------|-------------|-----|------|
| Bundler | Vite + React + TS | CRA, Next | Matches learning path; fast and market-standard. | No SSR |
| Styling | Tailwind CSS 4 | CSS modules, styled | Matches path; fast layout iteration. | Utility-heavy markup |
| UI state | Local `useState` / `useMemo` | Zustand, Redux | Small MVP; derive from filtered list. | Refactor if it grows |
| Routing | Single view | React Router | Not needed for MVP. | Add router if scope grows |
| Orders list (markup/layout) | **TBD** during implementation | `<table>`, CSS Grid row layout, card list | Mobile-first; choose when building the orders slice (see **§9**). | Update §9 + README when fixed |

---

## 9. Decision log (during build — living)

Append a row whenever you lock a choice that matters for the README or interviews. Copy the distilled version into **`README.md`** at MVP close.

| Date | Topic | Decision | Alternatives rejected | Rationale (for README / interview) |
|------|-------|----------|----------------------|-------------------------------------|
| (project start) | Shipping language | UI copy, mock data, README in **English** | Spanish UI | Portfolio targets English-speaking recruiters and roles. |
| (project start) | Responsive strategy | **Mobile-first** layout for all breakpoints | Desktop-first | Matches brief and typical reviewer behaviour (phone first). |
| (project start) | Orders list presentation | **Deferred** — decide when implementing the list | Semantic `<table>` vs grid/card rows | Avoid blocking skeleton work; compare tradeoffs at implementation time. |

---

## 10. Risks and unknowns

| Risk / doubt | If it happens | MVP mitigation |
|--------------|---------------|----------------|
| Scope creep (charts, more entities) | MVP never ships | “Out of scope” list + §11 milestones |
| Confusion “inventory” vs table | Wrong expectations | KPI only; README states it clearly |
| Tailwind 4 setup friction | Slow start | Short spike; follow official v4 docs |

**Allowed spikes (max 90 min each):**

1. Tailwind CSS 4 + Vite (`@tailwindcss/vite` per current docs).
2. (Optional) Minimal simulated load failure to practice retry.

---

## 11. Milestones (incremental)

1. **Minimal vertical slice:** Vite + React + TS + Tailwind; layout + 5 static KPIs + orders list from mock JSON without filters.
2. **Filters:** Date range + text + end ≥ start validation; KPIs derived from filtered orders.
3. **States:** Optional initial loading; “no matches” empty state; §7.5 a11y baseline.
4. **README** (problem, scope, `pnpm|npm run dev`, decisions) + **optional** static deploy (e.g. Vercel / Netlify).

---

## 12. Definition of Done (checklist)

- [ ] Main user-story flow meets acceptance criteria
- [ ] Empty / loading / error states covered where marked “yes” for MVP
- [ ] Edge cases marked “yes” for MVP have defined behaviour (copy + action)
- [ ] `README`: problem, scope, how to run, key decisions (**English**)
- [ ] Build (and lint/typecheck if present) clean
- [ ] (Optional) Deployed demo URL

---

## 13. Open questions

- **None blocking** to start implementation with this document.
- **Post-MVP plus (note in README):** client-only CSV export of filtered rows (`GUIA_8_PROYECTOS.md`).

---

## Appendix: opening questions (reference)

*(Answers are implied in §1–§7; revisit after the first milestone.)*

After the table filters correctly, **re-read §7** and adjust if real behaviour differs.
