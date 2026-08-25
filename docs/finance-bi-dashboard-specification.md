# Finance BI Dashboard Specification

> A complete architecture for a 360-degree finance command center. Covers data model, KPI catalog, dashboard layouts, alert logic, and drill-down paths for CFOs managing multi-entity, multi-site operations.

---

## Table of Contents

1. [Dashboard Architecture Overview](#1-dashboard-architecture-overview)
2. [Data Model & Dimensional Design](#2-data-model--dimensional-design)
3. [Dashboard 1: CFO Executive Cockpit](#3-dashboard-1-cfo-executive-cockpit)
4. [Dashboard 2: P&L Deep Dive](#4-dashboard-2-pl-deep-dive)
5. [Dashboard 3: Cash & Treasury](#5-dashboard-3-cash--treasury)
6. [Dashboard 4: Working Capital Control](#6-dashboard-4-working-capital-control)
7. [Dashboard 5: Multi-Site Scorecard](#7-dashboard-5-multi-site-scorecard)
8. [Dashboard 6: Franchise Network Health](#8-dashboard-6-franchise-network-health)
9. [Dashboard 7: Fleet & Asset Lifecycle](#9-dashboard-7-fleet--asset-lifecycle)
10. [Dashboard 8: Budget & Forecast Tracker](#10-dashboard-8-budget--forecast-tracker)
11. [Alert Engine & Anomaly Detection](#11-alert-engine--anomaly-detection)
12. [KPI Catalog (Complete)](#12-kpi-catalog-complete)
13. [Implementation Roadmap](#13-implementation-roadmap)

---

## 1. Dashboard Architecture Overview

### 1.1 Design Principles

1. **Executive → Operational:** Every dashboard starts with a summary and allows drill-down to transaction level
2. **Exception-based:** Green items compress; red items expand. Show problems first.
3. **Comparative:** Every number appears with its comparison (budget, prior year, prior month, trend)
4. **Actionable:** Every metric must answer "so what?" — linked to an action owner
5. **Self-service:** Business users can filter, slice, export without IT involvement
6. **Mobile-first:** CFO cockpit must render on mobile (alerts + top KPIs on phone)

### 1.2 Dashboard Hierarchy

```
┌─────────────────────────────────────────────────────────────────┐
│                    L0: CFO EXECUTIVE COCKPIT                     │
│  "How are we doing?" — 10 KPIs, traffic lights, 30-second scan │
├─────────────────────────────────────────────────────────────────┤
│  L1: FUNCTIONAL DEEP DIVES                                      │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────────┐   │
│  │ P&L Deep │  │ Cash &   │  │ Working  │  │ Budget &     │   │
│  │ Dive     │  │ Treasury │  │ Capital  │  │ Forecast     │   │
│  └──────────┘  └──────────┘  └──────────┘  └──────────────┘   │
├─────────────────────────────────────────────────────────────────┤
│  L2: OPERATIONAL VIEWS                                          │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐                     │
│  │ Multi-   │  │Franchise │  │ Fleet &  │                     │
│  │ Site     │  │ Network  │  │ Asset    │                     │
│  │ Scorecard│  │ Health   │  │ Lifecycle│                     │
│  └──────────┘  └──────────┘  └──────────┘                     │
├─────────────────────────────────────────────────────────────────┤
│  L3: TRANSACTION DETAIL                                         │
│  (Journal entries, invoices, bank transactions — searchable)    │
└─────────────────────────────────────────────────────────────────┘
```

### 1.3 User Personas & Access

| Persona | Primary Dashboard | Drill-Down Access | Refresh Frequency | Device |
|---------|------------------|:-----------------:|:-----------------:|--------|
| Group CFO | Executive Cockpit | All dashboards | Daily | Desktop + Mobile |
| Group Controller | P&L Deep Dive | All except Fleet | Daily | Desktop |
| Subsidiary Controller | Multi-Site Scorecard (own entity) | Own entity transactions | Daily | Desktop |
| Treasurer | Cash & Treasury | WC + Bank detail | Real-time | Desktop |
| CEO / Board | Executive Cockpit (read-only) | P&L + Budget only | Monthly | Presentation |
| Location Manager | Multi-Site Scorecard (own site) | Own site transactions | Daily | Mobile |
| PE Partner | Executive Cockpit (read-only) | P&L + Cash + Budget | Monthly | PDF export |

---

## 2. Data Model & Dimensional Design

### 2.1 Star Schema

```
                    ┌──────────────┐
                    │  dim_time    │
                    │──────────────│
                    │ date_key     │
                    │ year         │
                    │ quarter      │
                    │ month        │
                    │ week         │
                    │ day          │
                    │ fiscal_year  │
                    │ fiscal_period│
                    │ is_working_day│
                    └──────┬───────┘
                           │
┌──────────────┐   ┌──────┴───────┐   ┌──────────────┐
│ dim_entity   │   │  fact_gl     │   │ dim_account  │
│──────────────│   │──────────────│   │──────────────│
│ entity_key   ├───┤ date_key     ├───┤ account_key  │
│ entity_code  │   │ entity_key   │   │ account_code │
│ entity_name  │   │ account_key  │   │ account_name │
│ country      │   │ location_key │   │ account_L1   │
│ currency     │   │ cost_ctr_key │   │ account_L2   │
│ ownership    │   │ amount_local │   │ account_L3   │
│ consol_method│   │ amount_group │   │ account_L4   │
│ parent_entity│   │ budget_amt   │   │ bs_pl_flag   │
└──────────────┘   │ py_amount    │   │ debit_credit │
                   │ source       │   └──────────────┘
┌──────────────┐   │ je_number    │
│ dim_location │   │ description  │   ┌──────────────┐
│──────────────│   └──────┬───────┘   │dim_cost_ctr  │
│ location_key ├──────────┘     └─────┤ cc_key       │
│ location_code│                      │ cc_code      │
│ location_name│                      │ cc_name      │
│ region       │                      │ department   │
│ city         │                      │ manager      │
│ format       │                      └──────────────┘
│ ownership    │
│ open_date    │
│ sqm          │
│ capacity     │
└──────────────┘

Additional fact tables:
┌────────────────┐  ┌────────────────┐  ┌────────────────┐
│ fact_cash_flow │  │ fact_ar_aging  │  │ fact_fleet     │
│────────────────│  │────────────────│  │────────────────│
│ date_key       │  │ date_key       │  │ date_key       │
│ entity_key     │  │ entity_key     │  │ location_key   │
│ flow_type      │  │ customer_key   │  │ vehicle_id     │
│ amount         │  │ invoice_key    │  │ purchase_cost  │
│ category       │  │ total_amount   │  │ book_value     │
│ (operating/    │  │ current        │  │ depreciation   │
│  investing/    │  │ days_30        │  │ residual_est   │
│  financing)    │  │ days_60        │  │ utilisation_pct│
│ forecast_flag  │  │ days_90        │  │ revenue_mtd    │
│ actual_flag    │  │ days_120_plus  │  │ maintenance_ytd│
└────────────────┘  │ provision      │  │ status         │
                    └────────────────┘  └────────────────┘
```

### 2.2 Key Calculated Measures

```sql
-- Revenue (actual)
SUM(fact_gl.amount_group) WHERE dim_account.account_L1 = 'Revenue'

-- Revenue (budget)
SUM(fact_gl.budget_amt) WHERE dim_account.account_L1 = 'Revenue'

-- EBITDA
SUM(amount_group) WHERE account_L1 IN ('Revenue','COGS','OpEx')
-- (excludes D&A, Finance, Tax)

-- EBITDA Margin
EBITDA / Revenue * 100

-- Variance to Budget (EUR)
Actual - Budget

-- Variance to Budget (%)
(Actual - Budget) / ABS(Budget) * 100

-- Like-for-Like Revenue
SUM(amount_group)
WHERE dim_location.open_date < DATEADD(month, -12, current_date)
AND dim_location.status = 'active'
AND dim_account.account_L1 = 'Revenue'

-- Cash Conversion
Operating_Cash_Flow / EBITDA * 100

-- DSO
(Trade_Receivables / Revenue_Last_90_Days) * 90

-- Revenue per FTE
Revenue / Headcount

-- Revenue per sqm
Revenue / dim_location.sqm
```

### 2.3 Data Refresh Schedule

| Data Source | Refresh Frequency | Latency | Priority |
|-----------|:-----------------:|:-------:|:--------:|
| Bank feeds | Every 4 hours | < 4h | P1 |
| POS transactions | Daily (overnight) | < 24h | P1 |
| GL postings (ERP) | Daily (overnight) | < 24h | P1 |
| Payroll | Monthly (after payroll run) | < 48h | P2 |
| Budget / Forecast | On upload (ad-hoc) | Immediate | P2 |
| Fleet management | Daily | < 24h | P2 |
| Franchise royalty reports | Monthly (T+5) | < 5 days | P3 |
| FX rates (ECB) | Daily | Same day | P1 |
| Headcount (HRIS) | Weekly | < 7 days | P3 |

---

## 3. Dashboard 1: CFO Executive Cockpit

### 3.1 Layout Specification

```
┌─────────────────────────────────────────────────────────────────────┐
│  CFO EXECUTIVE COCKPIT                    [Period: Aug 2026]  [▼]  │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌────────┐ │
│  │REVENUE  │  │ EBITDA  │  │  CASH   │  │   DSO   │  │  FTE   │ │
│  │EUR 1.8M │  │EUR 216K │  │EUR 890K │  │ 42 days │  │  127   │ │
│  │ ▲ +5%   │  │ ▼ -3%   │  │ ▲ +120K │  │ ▲ +4d   │  │ = plan │ │
│  │ [GREEN] │  │ [AMBER] │  │ [GREEN] │  │ [AMBER] │  │[GREEN] │ │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘  └────────┘ │
│                                                                     │
│  ┌──────────────────────────────┐  ┌──────────────────────────────┐│
│  │  REVENUE TREND (12 months)  │  │  EBITDA BRIDGE (vs Budget)   ││
│  │  ┌─────────────────────┐    │  │  Budget    ███████████ 250K  ││
│  │  │    /\    /\   /\    │    │  │  Volume    ██ +40K           ││
│  │  │   /  \  /  \ /  \  │    │  │  Price     █ -15K            ││
│  │  │  /    \/    \/    \ │    │  │  COGS      ██ -35K           ││
│  │  │ /                  \│    │  │  Personnel █ -18K            ││
│  │  │/                    │    │  │  Other     █ -6K             ││
│  │  └─────────────────────┘    │  │  Actual    ████████████ 216K ││
│  │  — Actual  --- Budget       │  │                              ││
│  └──────────────────────────────┘  └──────────────────────────────┘│
│                                                                     │
│  ┌──────────────────────────────┐  ┌──────────────────────────────┐│
│  │  TOP 5 RISKS / RED FLAGS    │  │  KEY DECISIONS PENDING       ││
│  │                              │  │                              ││
│  │  1. EBITDA -3% vs budget    │  │  1. ERP vendor selection     ││
│  │     → Cost overrun in Ops   │  │     Due: 15 Sep              ││
│  │  2. DSO +4 days (43→47)     │  │  2. Franchise renewal (3x)  ││
│  │     → 2 large invoices past │  │     Due: 30 Sep              ││
│  │       due (EUR 85K total)   │  │  3. Capex approval MIL-005  ││
│  │  3. Location CAT-001 loss   │  │     EUR 180K — Board vote    ││
│  │     → CM2 negative 2nd month│  │                              ││
│  └──────────────────────────────┘  └──────────────────────────────┘│
│                                                                     │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │  LOCATION HEATMAP (Bubble = Revenue, Color = EBITDA Margin)   │ │
│  │                                                                │ │
│  │     ●MIL-001    ●ROM-001                                      │ │
│  │   (large,green) (medium,green)   ○CAT-001                     │ │
│  │         ●MIL-002      ●NAP-001   (small,red)                  │ │
│  │       (large,green) (medium,amber)                             │ │
│  │                                                                │ │
│  └────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────┘
```

### 3.2 KPI Tile Logic

| KPI | Source | Comparison | GREEN | AMBER | RED |
|-----|--------|-----------|:-----:|:-----:|:---:|
| Revenue | fact_gl | vs Budget | ≥ 95% | 85-95% | < 85% |
| EBITDA | fact_gl | vs Budget | ≥ 95% | 85-95% | < 85% |
| Cash | Bank feed | vs Prior Month | Increasing or stable | -5% to -15% | < -15% |
| DSO | fact_ar_aging | vs Target (45d) | ≤ 45 days | 45-60 days | > 60 days |
| FTE | HRIS | vs Budget | Within ±5% | ±5-15% | > ±15% |

### 3.3 Drill-Down Paths (Click Behavior)

| Click Target | Drills Into | Filters Applied |
|-------------|-------------|-----------------|
| Revenue tile | P&L Deep Dive → Revenue tab | Current month |
| EBITDA tile | P&L Deep Dive → EBITDA Bridge tab | Current month |
| Cash tile | Cash & Treasury dashboard | Current position |
| DSO tile | Working Capital → AR Aging | Current month |
| FTE tile | P&L Deep Dive → Personnel Cost tab | Current month |
| Location bubble | Multi-Site Scorecard → specific location | All periods |
| Risk item | Linked action plan (external) | — |

---

## 4. Dashboard 2: P&L Deep Dive

### 4.1 Layout

```
┌─────────────────────────────────────────────────────────────────────┐
│  P&L DEEP DIVE           [Entity: ▼ All]  [Period: ▼ Aug 2026]    │
│                           [Location: ▼ All] [View: ▼ vs Budget]    │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │  FULL P&L TABLE (collapsible rows)                            │ │
│  │                                                                │ │
│  │  Account              Actual    Budget   Var EUR  Var%    PY   │ │
│  │  ─────────────────────────────────────────────────────────────  │ │
│  │  ▼ Revenue            1,800K   1,750K   +50K    +2.9%  1,620K│ │
│  │    ├ Product A          900K     880K   +20K    +2.3%    810K│ │
│  │    ├ Product B          650K     620K   +30K    +4.8%    580K│ │
│  │    └ Other              250K     250K      0K    0.0%    230K│ │
│  │  ▼ COGS               (720K)   (700K)  (20K)   -2.9%  (648K)│ │
│  │  ─────────────────────────────────────────────────────────────  │ │
│  │  Gross Profit         1,080K   1,050K   +30K    +2.9%    972K│ │
│  │  Gross Margin           60.0%    60.0%                  60.0%│ │
│  │  ▼ Personnel           (540K)   (510K)  (30K)   -5.9%  (486K)│ │
│  │  ▼ Marketing           (126K)   (130K)   +4K    +3.1%  (113K)│ │
│  │  ▼ Facilities           (90K)    (85K)   (5K)   -5.9%   (81K)│ │
│  │  ▼ Technology           (54K)    (50K)   (4K)   -8.0%   (49K)│ │
│  │  ▼ Other G&A            (54K)    (50K)   (4K)   -8.0%   (49K)│ │
│  │  ─────────────────────────────────────────────────────────────  │ │
│  │  EBITDA                 216K     225K    (9K)   -4.0%    194K│ │
│  │  EBITDA Margin          12.0%    12.9%                  12.0%│ │
│  │                                                                │ │
│  │  [Expand to EBIT / EBT / Net Profit ▼]                       │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                     │
│  ┌────────────────────────────┐  ┌────────────────────────────────┐│
│  │  REVENUE BY SEGMENT       │  │  COST STRUCTURE (% of Revenue) ││
│  │  (stacked bar, 12 months) │  │  (waterfall: Rev → EBITDA)     ││
│  │                            │  │                                ││
│  │  [A] [A] [A] [A] [A]      │  │  Rev 100%                     ││
│  │  [B] [B] [B] [B] [B]      │  │  COGS -40%                    ││
│  │  [O] [O] [O] [O] [O]      │  │  Personnel -30%               ││
│  │  Aug Sep Oct Nov Dec       │  │  Marketing -7%                ││
│  │                            │  │  Other -11%                   ││
│  └────────────────────────────┘  │  EBITDA = 12%                 ││
│                                  └────────────────────────────────┘│
│                                                                     │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │  VARIANCE COMMENTARY (auto-pulled from commentary database)   │ │
│  │                                                                │ │
│  │  Personnel +EUR 30K vs budget: 2 unplanned hires in Ops for   │ │
│  │  seasonal peak (EUR 20K) + overtime in logistics (EUR 10K).   │ │
│  │  Overtime expected to normalise in September. Hires budgeted  │ │
│  │  in reforecast RF2.                                           │ │
│  └────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────┘
```

### 4.2 Interactive Features

| Feature | Behavior |
|---------|----------|
| Click any P&L line | Expands to sub-accounts (up to account L4) |
| Click sub-account | Shows journal entries for that account/period |
| Toggle "vs Budget" / "vs PY" / "vs Prior Month" | All variances recalculate |
| Filter by Entity | P&L shows single entity or consolidated |
| Filter by Location | P&L scoped to specific site |
| Export | Excel (formatted), PDF (board-ready) |

---

## 5. Dashboard 3: Cash & Treasury

### 5.1 Layout

```
┌─────────────────────────────────────────────────────────────────────┐
│  CASH & TREASURY                              [Date: 25 Aug 2026]  │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌───────────────┐  ┌───────────────┐  ┌───────────────┐          │
│  │ TOTAL CASH    │  │ AVAILABLE     │  │ NET DEBT      │          │
│  │ EUR 890K      │  │ LIQUIDITY     │  │ EUR 1.2M      │          │
│  │ ▲ +120K vs PM │  │ EUR 1.89M     │  │ 2.8x EBITDA   │          │
│  │               │  │ (cash+facility)│  │ Covenant: <3.5│          │
│  └───────────────┘  └───────────────┘  └───────────────┘          │
│                                                                     │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │  CASH WATERFALL (Month)                                       │ │
│  │                                                                │ │
│  │  Opening  █████████████████████████████  EUR 770K              │ │
│  │  + Receipts  ████████████████████  EUR 420K                    │ │
│  │  - Payroll     ██████████  (EUR 180K)                         │ │
│  │  - Suppliers   ████████  (EUR 140K)                           │ │
│  │  - Rent        ███  (EUR 45K)                                 │ │
│  │  - Tax         ██  (EUR 30K)                                  │ │
│  │  - Capex       █  (EUR 15K)                                   │ │
│  │  - Loan repay  ██  (EUR 25K)                                  │ │
│  │  +/- Other     █  EUR 5K                                      │ │
│  │  ═══════════════════════════════════                           │ │
│  │  Closing  ██████████████████████████████  EUR 890K             │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                     │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │  13-WEEK CASH FORECAST                                        │ │
│  │  (line chart: actual cash + forecast band)                    │ │
│  │                                                                │ │
│  │  1,000K ─────────────────────────────────────                  │ │
│  │    800K ──────/\──────────────/───────────── Forecast (base)   │ │
│  │    600K ─────/  \────────────/──────────────                   │ │
│  │    400K ────/    ──────────/──────────────── Forecast (stress) │ │
│  │    200K ──────────────────────────────────── Min. buffer       │ │
│  │         W1  W2  W3  W4  W5  W6  W7 ... W13                   │ │
│  │                                                                │ │
│  │  ⚠ Cash dips below EUR 500K buffer in Week 8 (tax payment)   │ │
│  │    → Recommend: accelerate collections by EUR 80K or draw     │ │
│  │      EUR 100K from revolving facility                         │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                     │
│  ┌──────────────────────────────┐  ┌──────────────────────────────┐│
│  │  CASH BY ENTITY             │  │  COVENANT DASHBOARD          ││
│  │                              │  │                              ││
│  │  IT-01:  EUR 320K  [GREEN]  │  │  Net Debt/EBITDA  2.8x  [G] ││
│  │  IT-02:  EUR 180K  [GREEN]  │  │  Interest Cover   4.2x  [G] ││
│  │  IT-03:  EUR 150K  [GREEN]  │  │  Capex Limit      55%   [G] ││
│  │  FR-01:  EUR 240K  [GREEN]  │  │  Min Liquidity    189%  [G] ││
│  │                              │  │  Dividend Gate    BLOCKED[A]││
│  └──────────────────────────────┘  └──────────────────────────────┘│
└─────────────────────────────────────────────────────────────────────┘
```

---

## 6. Dashboard 4: Working Capital Control

### 6.1 Layout

```
┌─────────────────────────────────────────────────────────────────────┐
│  WORKING CAPITAL CONTROL                    [Period: Aug 2026]      │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌────────┐  ┌────────┐  ┌────────┐  ┌──────────────────────────┐ │
│  │  DSO   │  │  DPO   │  │  DIO   │  │  CASH CONVERSION CYCLE  │ │
│  │ 42 days│  │ 51 days│  │ 18 days│  │  42 + 18 - 51 = 9 days  │ │
│  │ ▲ +4d  │  │ ▼ -3d  │  │ = plan │  │  Target: < 15 days [G]  │ │
│  │ [AMBER]│  │ [AMBER]│  │ [GREEN]│  │                          │ │
│  └────────┘  └────────┘  └────────┘  └──────────────────────────┘ │
│                                                                     │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │  ACCOUNTS RECEIVABLE AGING                                    │ │
│  │                                                                │ │
│  │  ████████████████████████████████████ Current   EUR 620K  72% │ │
│  │  ██████████                           1-30 days EUR 120K  14% │ │
│  │  █████                                31-60 days EUR 55K   6% │ │
│  │  ███                                  61-90 days EUR 35K   4% │ │
│  │  ██                                   90+ days   EUR 30K   3% │ │
│  │                                                                │ │
│  │  Total AR: EUR 860K | Provision: EUR 18K (2.1%) | Net: 842K  │ │
│  │                                                                │ │
│  │  ⚠ Top overdue: Acme Corp EUR 45K (75 days) — [View details] │ │
│  │  ⚠ Top overdue: Beta Srl  EUR 28K (62 days) — [View details] │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                     │
│  ┌──────────────────────────────┐  ┌──────────────────────────────┐│
│  │  DSO TREND (12 months)      │  │  TOP 10 OVERDUE INVOICES    ││
│  │  60 ─────────────────────   │  │                              ││
│  │  50 ───────────────/──── T  │  │  Customer   Amount  Days    ││
│  │  40 ──────/\──────/──── A  │  │  Acme Corp  EUR 45K  75 [!] ││
│  │  30 ─────/  \────/──────   │  │  Beta Srl   EUR 28K  62 [!] ││
│  │  20 ────/    \──/──────    │  │  Gamma SpA  EUR 18K  48     ││
│  │     Sep Oct Nov Dec Jan... │  │  Delta SA   EUR 12K  45     ││
│  │                            │  │  ...                        ││
│  └──────────────────────────────┘  └──────────────────────────────┘│
└─────────────────────────────────────────────────────────────────────┘
```

---

## 7. Dashboard 5: Multi-Site Scorecard

### 7.1 Layout

```
┌─────────────────────────────────────────────────────────────────────┐
│  MULTI-SITE SCORECARD                       [Period: Aug 2026]      │
│  [Region: ▼ All]  [Format: ▼ All]  [Sort by: ▼ EBITDA Margin]     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │  LOCATION RANKING TABLE                                       │ │
│  │                                                                │ │
│  │  #  Location    Region   Revenue   CM1%   CM2%   Rev/FTE  LFL │ │
│  │  ── ─────────── ──────── ──────── ────── ────── ─────── ───── │ │
│  │  1  MIL-001     North    EUR 250K 68.0%  22.0%  EUR 25K +8%  │ │
│  │  2  ROM-001     Central  EUR 180K 65.0%  19.5%  EUR 22K +6%  │ │
│  │  3  MIL-002     North    EUR 220K 64.0%  18.0%  EUR 20K +4%  │ │
│  │  4  FLR-001     Central  EUR 140K 62.0%  16.5%  EUR 19K +3%  │ │
│  │  5  TRN-001     North    EUR 130K 60.0%  15.0%  EUR 18K +2%  │ │
│  │  ...                                                           │ │
│  │  ── ─────────── ──────── ──────── ────── ────── ─────── ───── │ │
│  │  24 BAR-001     South    EUR  65K 48.0%   2.0%  EUR 13K -3%  │ │
│  │  25 CAT-001     South    EUR  42K 40.0%  -4.0%  EUR 10K -15% │ │
│  │     ^^^ [RED] Loss-making — closure review triggered          │ │
│  │                                                                │ │
│  │  NETWORK TOTAL: EUR 3.2M  CM1 61.5%  CM2 14.8%  LFL +4.2%   │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                     │
│  ┌──────────────────────────────┐  ┌──────────────────────────────┐│
│  │  REGIONAL COMPARISON        │  │  NEW OPENINGS TRACKER        ││
│  │  (radar chart: 5 metrics)   │  │                              ││
│  │                              │  │  Location  Opened  Rev Ramp ││
│  │        Revenue               │  │  PAD-001   Jun 26  EUR 35K  ││
│  │          ●                   │  │            Target: EUR 80K   ││
│  │     /    |    \              │  │            Ramp:   44% [A]   ││
│  │  LFL    |    CM2%           │  │                              ││
│  │     \    |    /              │  │  VER-001   Jul 26  EUR 22K  ││
│  │          ●                   │  │            Target: EUR 70K   ││
│  │       Rev/FTE               │  │            Ramp:   31% [R]   ││
│  │                              │  │                              ││
│  │  ─ North ─ Central ─ South  │  │  Avg ramp to breakeven: 8mo ││
│  └──────────────────────────────┘  └──────────────────────────────┘│
└─────────────────────────────────────────────────────────────────────┘
```

---

## 8. Dashboard 6: Franchise Network Health

```
┌─────────────────────────────────────────────────────────────────────┐
│  FRANCHISE NETWORK HEALTH                   [Period: Aug 2026]      │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌───────────────────┐ │
│  │FRANCHISE │  │ ROYALTY  │  │ NETWORK  │  │  AT-RISK          │ │
│  │LOCATIONS │  │ INCOME   │  │ REVENUE  │  │  FRANCHISEES      │ │
│  │    35    │  │ EUR 185K │  │ EUR 3.1M │  │     3             │ │
│  │ +2 vs PY │  │ ▲ +8%   │  │ (POS data)│  │ (EBITDA < 5%)    │ │
│  └──────────┘  └──────────┘  └──────────┘  └───────────────────┘ │
│                                                                     │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │  FRANCHISEE PERFORMANCE TABLE                                 │ │
│  │                                                                │ │
│  │  Franchisee     Revenue    Royalty   Growth  Est.EBITDA Status │ │
│  │  ────────────── ────────── ──────── ─────── ────────── ────── │ │
│  │  F-MIL-010      EUR 52K    EUR 3.1K +12%    14.5%      [G]   │ │
│  │  F-ROM-005      EUR 48K    EUR 2.9K  +8%    12.0%      [G]   │ │
│  │  F-TRN-003      EUR 38K    EUR 2.3K  +3%     9.5%      [G]   │ │
│  │  ...                                                           │ │
│  │  F-NAP-008      EUR 22K    EUR 1.3K  -8%     4.2%      [R]   │ │
│  │  F-CAG-002      EUR 18K    EUR 1.1K -15%     2.1%      [R]   │ │
│  │  F-PAL-004      EUR 15K    EUR 0.9K -20%    -1.5%      [R]   │ │
│  │                                                                │ │
│  │  ⚠ F-PAL-004: Negative EBITDA for 3rd consecutive month.     │ │
│  │    Action: Operational audit scheduled. Consider termination.  │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                     │
│  ┌──────────────────────────────┐  ┌──────────────────────────────┐│
│  │  ROYALTY COLLECTION         │  │  FRANCHISE PIPELINE          ││
│  │                              │  │                              ││
│  │  Collected on time:  92%    │  │  Active: 35                  ││
│  │  Late (< 30 days):   5%    │  │  In negotiation: 4           ││
│  │  Late (> 30 days):   3%    │  │  Signed (not open): 2        ││
│  │                              │  │  Renewals due (12mo): 6     ││
│  │  Outstanding royalty:       │  │  Terminations YTD: 1         ││
│  │  EUR 8.5K (4.6% of total)  │  │  Net growth: +3 locations    ││
│  └──────────────────────────────┘  └──────────────────────────────┘│
└─────────────────────────────────────────────────────────────────────┘
```

---

## 9. Dashboard 7: Fleet & Asset Lifecycle

```
┌─────────────────────────────────────────────────────────────────────┐
│  FLEET & ASSET LIFECYCLE                    [Period: Aug 2026]      │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────────────┐  │
│  │  FLEET   │  │  FLEET   │  │UTILISATION│  │ RESIDUAL VALUE  │  │
│  │  SIZE    │  │  VALUE   │  │  RATE     │  │ ACCURACY (LTM)  │  │
│  │   520    │  │ EUR 8.2M │  │   78.5%   │  │   -3.2%         │  │
│  │ (NBV)    │  │ (book)   │  │ Tgt: 80%  │  │ (overestimated) │  │
│  └──────────┘  └──────────┘  └──────────┘  └──────────────────┘  │
│                                                                     │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │  FLEET AGE DISTRIBUTION                                       │ │
│  │                                                                │ │
│  │  0-12 months:  ████████████████████  120 vehicles (23%)        │ │
│  │  13-24 months: ██████████████████████████  160 vehicles (31%) │ │
│  │  25-36 months: ██████████████████  110 vehicles (21%)         │ │
│  │  37-48 months: ██████████████  85 vehicles (16%)              │ │
│  │  49+ months:   █████████  45 vehicles (9%) ⚠ Past target life│ │
│  │                                                                │ │
│  │  Average fleet age: 26.4 months | Target: < 30 months         │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                     │
│  ┌──────────────────────────────┐  ┌──────────────────────────────┐│
│  │  LIFECYCLE PROFITABILITY    │  │  RESIDUAL VALUE TRACKER      ││
│  │  (per vehicle, last 50      │  │  (Estimated vs Actual at     ││
│  │   disposals)                │  │   disposal)                  ││
│  │                              │  │                              ││
│  │  Revenue:      EUR 24,000   │  │  Avg estimate:  EUR 8,000   ││
│  │  Direct costs: (EUR 7,200)  │  │  Avg actual:    EUR 7,744   ││
│  │  Depreciation: (EUR 18,200) │  │  Variance:      -3.2%       ││
│  │  Disposal gain: EUR 1,800   │  │                              ││
│  │  ───────────────────────    │  │  Impact on EUR 8.2M fleet:  ││
│  │  Lifecycle margin: EUR 400  │  │  Potential writedown: 262K  ││
│  │  Lifecycle ROI:     1.5%    │  │                              ││
│  │                              │  │  ⚠ Review residual value   ││
│  │  ⚠ Below target (3.0%)     │  │    assumptions in Q3 close  ││
│  └──────────────────────────────┘  └──────────────────────────────┘│
│                                                                     │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │  UTILISATION BY LOCATION (heatmap)                            │ │
│  │                                                                │ │
│  │  MIL-001 ████████████████████ 92%  [GREEN]                    │ │
│  │  ROM-001 █████████████████  85%  [GREEN]                      │ │
│  │  MIL-002 ████████████████  82%  [GREEN]                      │ │
│  │  FLR-001 ████████████████  80%  [GREEN]                      │ │
│  │  NAP-001 ██████████████  72%  [AMBER]                        │ │
│  │  BAR-001 ████████████  62%  [RED] → Redeploy 8 vehicles      │ │
│  │  CAT-001 ██████████  48%  [RED] → Location closure candidate │ │
│  └────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 10. Dashboard 8: Budget & Forecast Tracker

```
┌─────────────────────────────────────────────────────────────────────┐
│  BUDGET & FORECAST TRACKER                  [FY: 2026]              │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │  YTD ACTUAL vs BUDGET vs FORECAST                             │ │
│  │                                                                │ │
│  │               YTD Act   YTD Bud   Var%    FY Fcst   FY Bud   │ │
│  │  Revenue      12.4M     12.0M    +3.3%    19.2M     18.5M    │ │
│  │  EBITDA        1.6M      1.7M    -5.9%     2.4M      2.7M    │ │
│  │  Cash flow     0.9M      1.1M   -18.2%     1.3M      1.8M    │ │
│  │  Headcount      127       125    +1.6%      135       130     │ │
│  │                                                                │ │
│  │  Revenue: ON TRACK (+3.3% YTD)                                │ │
│  │  EBITDA:  AT RISK (-5.9% YTD) — Cost overruns not yet offset  │ │
│  │  Cash:    OFF TRACK — Working capital absorption + capex       │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                     │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │  MONTHLY PHASING: Actual (bars) vs Budget (line) vs Fcst (▪)  │ │
│  │                                                                │ │
│  │  2.5M ──────────────────────────────────────────────────       │ │
│  │  2.0M ──────────────────────────────────────/──────── Budget   │ │
│  │  1.5M ─────────█──█──█──█──█──█──█──█──▪──▪──▪──▪── Fcst     │ │
│  │  1.0M ──█──█──█──                                             │ │
│  │       Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec          │ │
│  │                                  ▲                             │ │
│  │                              We are here                       │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                     │
│  ┌──────────────────────────────┐  ┌──────────────────────────────┐│
│  │  FORECAST ACCURACY          │  │  GAP-TO-PLAN ACTIONS         ││
│  │  (last 6 months)            │  │                              ││
│  │                              │  │  1. Accelerate collections  ││
│  │  Revenue:  Avg error 2.8%   │  │     → Target: +EUR 80K Q4   ││
│  │  EBITDA:   Avg error 6.1%   │  │  2. Freeze discretionary    ││
│  │  Cash:     Avg error 12.3%  │  │     spend → Save EUR 50K    ││
│  │                              │  │  3. Delay 2 hires to Q1'27 ││
│  │  ⚠ Cash forecast error too │  │     → Save EUR 40K          ││
│  │    high — improve 13-week   │  │  4. Price increase +2% from ││
│  │    model inputs             │  │     Oct → EUR 30K/quarter   ││
│  └──────────────────────────────┘  └──────────────────────────────┘│
└─────────────────────────────────────────────────────────────────────┘
```

---

## 11. Alert Engine & Anomaly Detection

### 11.1 Alert Rules

| Alert | Condition | Severity | Recipient | Channel |
|-------|-----------|:--------:|-----------|---------|
| Revenue miss | MTD revenue < 85% of prorated budget at T+15 | HIGH | CFO, CEO | Email + Dashboard |
| Cash below buffer | Cash balance < EUR 500K | CRITICAL | CFO, Treasurer | Email + SMS |
| DSO spike | DSO increases > 10 days vs prior month | MEDIUM | Controller | Dashboard |
| Location loss | Any location CM2 < 0 for 2+ consecutive months | HIGH | CFO, COO | Email |
| Franchise non-payment | Royalty overdue > 30 days | MEDIUM | Franchise Manager | Email |
| Utilisation drop | Fleet utilisation < 60% at any location | MEDIUM | Fleet Manager | Dashboard |
| Residual value gap | Disposal prices < 90% of estimated residual (rolling 10 disposals) | HIGH | Fleet Manager, CFO | Email |
| Covenant breach risk | Any covenant at > 90% of limit | HIGH | CFO, Treasurer | Email + SMS |
| Budget variance | Any P&L line > ±20% vs budget and > EUR 20K absolute | MEDIUM | Controller | Dashboard |
| Headcount over budget | FTE > 105% of budget | MEDIUM | CHRO, CFO | Dashboard |

### 11.2 Anomaly Detection (Statistical)

Beyond threshold alerts, implement statistical anomaly detection:

```
For each KPI, maintain a rolling 12-month distribution:
  - Mean (μ)
  - Standard deviation (σ)

Flag anomaly when:
  - Current value > μ + 2σ (unusually high)
  - Current value < μ - 2σ (unusually low)

Example:
  Personnel costs: μ = EUR 510K, σ = EUR 25K
  Current month: EUR 580K
  Z-score: (580 - 510) / 25 = 2.8 → ANOMALY (> 2σ)

  Alert: "Personnel costs EUR 580K are 2.8 standard deviations above
          the 12-month average. Investigate before closing."
```

### 11.3 Alert Lifecycle

```
TRIGGERED → ACKNOWLEDGED → INVESTIGATED → RESOLVED / ACCEPTED
    │            │               │              │
    │            │               │              └── CFO accepts as new normal
    │            │               │                  (threshold updated)
    │            │               └── Root cause identified, action taken
    │            └── Owner confirms they've seen it (SLA: 24h)
    └── System detects condition, sends notification
```

---

## 12. KPI Catalog (Complete)

### Financial KPIs

| # | KPI | Formula | Frequency | Target | Owner |
|---|-----|---------|:---------:|--------|-------|
| F1 | Revenue | Sum of revenue accounts | Monthly | Budget | CRO |
| F2 | Revenue Growth (YoY) | (Rev CY - Rev PY) / Rev PY × 100 | Monthly | > 10% | CRO |
| F3 | LFL Revenue Growth | LFL Rev CY / LFL Rev PY - 1 | Monthly | > 5% | CRO |
| F4 | Gross Margin % | (Revenue - COGS) / Revenue × 100 | Monthly | > 60% | COO |
| F5 | EBITDA | Revenue - COGS - OpEx (excl D&A) | Monthly | Budget | CFO |
| F6 | EBITDA Margin % | EBITDA / Revenue × 100 | Monthly | > 12% | CFO |
| F7 | Net Profit Margin % | Net Profit / Revenue × 100 | Monthly | > 5% | CFO |
| F8 | Operating Cash Flow | Cash from operations | Monthly | > 80% of EBITDA | CFO |
| F9 | Free Cash Flow | OCF - Capex | Quarterly | Positive | CFO |
| F10 | Cash Conversion | OCF / EBITDA × 100 | Quarterly | > 80% | CFO |

### Working Capital KPIs

| # | KPI | Formula | Frequency | Target | Owner |
|---|-----|---------|:---------:|--------|-------|
| W1 | DSO | (AR / Revenue) × Days | Monthly | < 45 days | Controller |
| W2 | DPO | (AP / COGS) × Days | Monthly | 45-60 days | Controller |
| W3 | DIO | (Inventory / COGS) × Days | Monthly | < 30 days | COO |
| W4 | CCC | DSO + DIO - DPO | Monthly | < 30 days | CFO |
| W5 | AR Overdue % | AR > 30 days / Total AR × 100 | Monthly | < 15% | Controller |
| W6 | Bad Debt Rate | Write-offs / Revenue × 100 | Quarterly | < 1% | Controller |

### Operational KPIs (Multi-Site)

| # | KPI | Formula | Frequency | Target | Owner |
|---|-----|---------|:---------:|--------|-------|
| O1 | Revenue per Location | Total Revenue / Active Locations | Monthly | Varies | CRO |
| O2 | Revenue per FTE | Revenue / Headcount | Monthly | > EUR 15K | COO |
| O3 | Revenue per sqm | Revenue / Total sqm | Monthly | Varies | COO |
| O4 | CM1 % (Contribution Margin) | (Revenue - Direct Costs) / Revenue | Monthly | > 55% | COO |
| O5 | CM2 % (Location EBITDA) | (CM1 - Location Overheads) / Revenue | Monthly | > 10% | COO |
| O6 | Fleet Utilisation | Rented Days / Available Days × 100 | Daily/Weekly | > 80% | Fleet Mgr |
| O7 | New Opening Ramp | Actual Rev / Target Rev at month N | Monthly | > 70% at M6 | COO |
| O8 | Franchise Compliance | Locations meeting brand standards / Total | Quarterly | > 95% | Franchise |
| O9 | Employee Turnover | Leavers / Avg Headcount × 100 | Quarterly | < 15% | CHRO |
| O10 | Customer NPS | Net Promoter Score | Quarterly | > 40 | CRO |

### Leverage & Covenant KPIs

| # | KPI | Formula | Frequency | Target | Owner |
|---|-----|---------|:---------:|--------|-------|
| L1 | Net Debt / EBITDA | (Total Debt - Cash) / LTM EBITDA | Monthly | < 3.5x | CFO |
| L2 | Interest Coverage | LTM EBITDA / LTM Interest Expense | Monthly | > 3.0x | CFO |
| L3 | Equity Ratio | Total Equity / Total Assets × 100 | Quarterly | > 30% | CFO |
| L4 | Runway | Cash / Monthly Burn Rate | Monthly | > 12 months | Treasurer |

---

## 13. Implementation Roadmap

### Phase 1: Foundation (Month 1-2)

- [ ] Define KPI catalog (approved by CFO)
- [ ] Map data sources to KPIs
- [ ] Build data model (star schema)
- [ ] Connect ERP + Bank + POS data feeds
- [ ] Deploy CFO Executive Cockpit (10 KPIs)
- [ ] Set up daily data refresh

### Phase 2: Deep Dives (Month 3-4)

- [ ] Deploy P&L Deep Dive dashboard
- [ ] Deploy Cash & Treasury dashboard
- [ ] Deploy Working Capital Control dashboard
- [ ] Implement alert engine (threshold-based)
- [ ] User training: CFO + Controller + Treasurer

### Phase 3: Operational (Month 5-6)

- [ ] Deploy Multi-Site Scorecard
- [ ] Deploy Franchise Network Health (if applicable)
- [ ] Deploy Fleet & Asset Lifecycle (if applicable)
- [ ] Deploy Budget & Forecast Tracker
- [ ] Implement drill-down from L0 → L1 → L2 → L3
- [ ] Mobile app for location managers

### Phase 4: Intelligence (Month 7+)

- [ ] Anomaly detection (statistical)
- [ ] Forecast accuracy tracking
- [ ] Automated variance commentary suggestions
- [ ] Board pack auto-generation (PDF export)
- [ ] Natural language query ("What drove EBITDA miss in August?")

---

*Built from real-world finance BI implementations across multi-site operations. For an AI-powered implementation of this architecture, see [SCALA AI OS](https://get-scala.com) — enterprise AI platform with built-in financial dashboards, automated reporting, and multi-entity consolidation across 20 industry verticals.*
