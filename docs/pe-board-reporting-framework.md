# PE Board Reporting Framework

> A complete framework for financial reporting to Private Equity shareholders and boards of directors. Covers monthly financial packs, quarterly board decks, KPI governance, and investor communication standards.

---

## Table of Contents

1. [Reporting Cadence & Calendar](#1-reporting-cadence--calendar)
2. [Monthly Financial Pack (MFP)](#2-monthly-financial-pack-mfp)
3. [Quarterly Board Deck](#3-quarterly-board-deck)
4. [KPI Governance Framework](#4-kpi-governance-framework)
5. [Cash & Liquidity Reporting](#5-cash--liquidity-reporting)
6. [Variance Analysis Standards](#6-variance-analysis-standards)
7. [Forecasting & Reforecasting](#7-forecasting--reforecasting)
8. [Investor Relations Best Practices](#8-investor-relations-best-practices)
9. [Governance Documentation](#9-governance-documentation)

---

## 1. Reporting Cadence & Calendar

### 1.1 Standard PE Reporting Rhythm

| Report | Frequency | Audience | Deadline | Format |
|--------|-----------|----------|----------|--------|
| Flash report (revenue + cash) | Weekly | CFO, CEO | Monday AM | Email / 1-page |
| Monthly Financial Pack | Monthly | Board, PE partner | T+10 | PDF, 15-20 pages |
| Management commentary | Monthly | Board | T+10 (with MFP) | Written narrative |
| Quarterly Board Deck | Quarterly | Full board + PE | T+15 | Presentation, 30-40 slides |
| Budget / Annual Plan | Annually | Board + PE IC | October-November | Excel model + presentation |
| Reforecast | Quarterly (or trigger-based) | CFO, CEO, Board | T+20 post quarter | Updated model |
| Ad-hoc deep dives | As needed | PE partner | 48h turnaround | Memo or model |

### 1.2 Calendar Example (Monthly)

```
Period End (e.g., 31 January)
├── T+1-3:  Subsidiary close activities
├── T+5:    Subsidiary management P&L submitted
├── T+6-7:  Consolidation, eliminations, adjustments
├── T+8:    CFO review of consolidated numbers
├── T+9:    Commentary drafted, CFO approves
├── T+10:   Monthly Financial Pack distributed to board
├── T+12:   PE partner follow-up call (if questions)
└── T+15:   [Quarterly only] Board meeting
```

---

## 2. Monthly Financial Pack (MFP)

### 2.1 Standard Structure (15-20 pages)

| Section | Pages | Content |
|---------|:-----:|---------|
| Executive Summary | 1 | Traffic-light dashboard: revenue, EBITDA, cash, headcount. 3-line narrative. |
| P&L — Actual vs Budget vs Prior Year | 2-3 | Full P&L with variances (absolute + %). Highlights on material items. |
| Revenue Deep Dive | 2 | By segment/product/geography. New vs recurring. Pipeline/backlog if relevant. |
| Cost Analysis | 2 | Fixed vs variable. Major cost lines with trend. FTE vs non-FTE. |
| EBITDA Bridge | 1 | Waterfall: Budget → Volume → Price/Mix → Cost → FX → Actual EBITDA |
| Cash Flow | 2 | Operating CF, investing CF, financing CF. Cash conversion. DSO/DPO/DIO trends. |
| Balance Sheet Highlights | 1 | Working capital, net debt, capex, key ratios (leverage, coverage). |
| KPI Scorecard | 1 | 10-15 operational and financial KPIs with RAG status. |
| Risks & Opportunities | 1 | Top 5 risks (quantified), top 3 upside opportunities. |
| Outlook & Guidance | 1 | Updated view for quarter/year. Any guidance revision flagged. |
| Appendix | 2-3 | Detailed P&L, BS, CF statements. Headcount table. Capex tracker. |

### 2.2 P&L Template (PE Standard)

```
                          Actual    Budget    Var (EUR)  Var (%)   PY      vs PY (%)
─────────────────────────────────────────────────────────────────────────────────────
Revenue
  Product / Service A     X,XXX     X,XXX     +/-XXX    +/-X%    X,XXX    +/-X%
  Product / Service B     X,XXX     X,XXX     +/-XXX    +/-X%    X,XXX    +/-X%
  Other Revenue           X,XXX     X,XXX     +/-XXX    +/-X%    X,XXX    +/-X%
─────────────────────────────────────────────────────────────────────────────────────
Total Revenue             X,XXX     X,XXX     +/-XXX    +/-X%    X,XXX    +/-X%
─────────────────────────────────────────────────────────────────────────────────────
COGS / Direct Costs       (X,XXX)   (X,XXX)   +/-XXX    +/-X%   (X,XXX)   +/-X%
─────────────────────────────────────────────────────────────────────────────────────
Gross Profit              X,XXX     X,XXX     +/-XXX    +/-X%    X,XXX    +/-X%
Gross Margin %            XX.X%     XX.X%                         XX.X%
─────────────────────────────────────────────────────────────────────────────────────
Operating Expenses
  Personnel costs         (X,XXX)   (X,XXX)   +/-XXX    +/-X%   (X,XXX)   +/-X%
  Marketing & sales       (X,XXX)   (X,XXX)   +/-XXX    +/-X%   (X,XXX)   +/-X%
  Technology / IT         (X,XXX)   (X,XXX)   +/-XXX    +/-X%   (X,XXX)   +/-X%
  Facilities & rent       (X,XXX)   (X,XXX)   +/-XXX    +/-X%   (X,XXX)   +/-X%
  Professional services   (X,XXX)   (X,XXX)   +/-XXX    +/-X%   (X,XXX)   +/-X%
  Other G&A               (X,XXX)   (X,XXX)   +/-XXX    +/-X%   (X,XXX)   +/-X%
─────────────────────────────────────────────────────────────────────────────────────
Total OpEx                (X,XXX)   (X,XXX)   +/-XXX    +/-X%   (X,XXX)   +/-X%
─────────────────────────────────────────────────────────────────────────────────────
EBITDA                    X,XXX     X,XXX     +/-XXX    +/-X%    X,XXX    +/-X%
EBITDA Margin %           XX.X%     XX.X%                         XX.X%
─────────────────────────────────────────────────────────────────────────────────────
D&A                       (X,XXX)   (X,XXX)                      (X,XXX)
─────────────────────────────────────────────────────────────────────────────────────
EBIT                      X,XXX     X,XXX     +/-XXX    +/-X%    X,XXX    +/-X%
─────────────────────────────────────────────────────────────────────────────────────
Net financial income/exp  (X,XXX)   (X,XXX)                      (X,XXX)
─────────────────────────────────────────────────────────────────────────────────────
EBT (Profit Before Tax)   X,XXX     X,XXX     +/-XXX    +/-X%    X,XXX    +/-X%
─────────────────────────────────────────────────────────────────────────────────────
Tax                       (X,XXX)   (X,XXX)                      (X,XXX)
─────────────────────────────────────────────────────────────────────────────────────
Net Profit                X,XXX     X,XXX     +/-XXX    +/-X%    X,XXX    +/-X%
Net Margin %              XX.X%     XX.X%                         XX.X%
═══════════════════════════════════════════════════════════════════════════════════════
```

### 2.3 EBITDA Bridge (Waterfall Methodology)

The EBITDA bridge explains **why** actual differs from budget:

```
Budget EBITDA:                          EUR 1,200K
─────────────────────────────────────────────────────
(+) Volume effect (more units sold)      + EUR 150K
(+/-) Price/Mix effect                   - EUR  30K
(+/-) COGS variance (input costs)        - EUR  45K
(+/-) Personnel variance                 - EUR  20K
(+/-) Other OpEx variance                + EUR  35K
(+/-) FX impact                          - EUR  10K
(+/-) One-off / extraordinary items      + EUR   0K
─────────────────────────────────────────────────────
= Actual EBITDA:                        EUR 1,280K
                                        (+6.7% vs budget)
```

**Rules for bridge construction:**
- Start with budget (the "promise")
- Decompose into no more than 6-8 drivers
- Each driver must be quantifiable and actionable
- "Other" bucket should never exceed 20% of total variance
- One-offs must be genuinely non-recurring (PE will challenge repeating "one-offs")

### 2.4 Executive Summary — What PE Partners Actually Read

The executive summary is the **only page** guaranteed to be read. Structure it as:

```
┌──────────────────────────────────────────────────────────────────┐
│  EXECUTIVE SUMMARY — [Month Year]                                │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐           │
│  │REVENUE  │  │EBITDA   │  │CASH     │  │HEADCOUNT│           │
│  │EUR X.XM │  │EUR X.XM │  │EUR X.XM │  │XXX FTE  │           │
│  │[▲/▼] vs │  │[▲/▼] vs │  │[▲/▼] vs │  │[▲/▼] vs │           │
│  │budget   │  │budget   │  │prior mo │  │budget   │           │
│  │[GREEN]  │  │[AMBER]  │  │[GREEN]  │  │[GREEN]  │           │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘           │
│                                                                  │
│  KEY MESSAGES (max 3 bullets):                                  │
│  1. [Most important thing — good or bad]                        │
│  2. [Second most important thing]                               │
│  3. [Action being taken / decision needed]                      │
│                                                                  │
│  OUTLOOK: [One sentence on rest-of-year trajectory]             │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

**Rules:**
- Never bury bad news. Lead with it. PE partners will find it anyway.
- Quantify everything. "Sales were soft" → "Revenue missed budget by EUR 85K (-7%) driven by delayed contract X"
- Always pair a problem with an action: "Revenue missed... Management is [action] with expected recovery by [month]"

---

## 3. Quarterly Board Deck

### 3.1 Board Deck Structure (30-40 slides)

| # | Section | Slides | Owner |
|---|---------|:------:|-------|
| 1 | Agenda + Admin | 1 | Board secretary |
| 2 | Executive Summary & KPIs | 2-3 | CEO / CFO |
| 3 | Financial Performance (P&L, Bridge, CF) | 5-7 | CFO |
| 4 | Revenue & Commercial Update | 4-5 | CRO / CEO |
| 5 | Operational Performance | 3-4 | COO |
| 6 | People & Organisation | 2-3 | CHRO / CEO |
| 7 | Strategic Initiatives & Projects | 3-4 | CEO |
| 8 | Risk Register | 1-2 | CFO |
| 9 | Forecast Update (if reforecast quarter) | 2-3 | CFO |
| 10 | Decisions Required | 1 | CEO |
| 11 | Appendix (detailed data) | 5-8 | CFO |

### 3.2 Board Deck — Financial Slides Content

**Slide: Quarter P&L Summary**
- Q actual vs Q budget vs Q prior year
- YTD actual vs YTD budget vs YTD prior year
- Highlight top 3 variances (positive and negative)

**Slide: EBITDA Bridge (Quarterly)**
- Waterfall from budget EBITDA to actual EBITDA
- Decomposed by: Volume, Price/Mix, COGS, Personnel, Other OpEx, FX, One-offs

**Slide: Cash Flow & Liquidity**
- Cash waterfall: Opening balance → Operating CF → Investing CF → Financing CF → Closing balance
- Net debt evolution (if leveraged)
- Covenant compliance (if debt covenants exist)
- 13-week cash flow forecast (rolling)

**Slide: Working Capital Deep Dive**
- DSO (Days Sales Outstanding) trend — 12-month rolling
- DPO (Days Payable Outstanding) trend — 12-month rolling
- DIO (Days Inventory Outstanding) trend — if applicable
- Cash Conversion Cycle (CCC) = DSO + DIO - DPO
- Aged receivables breakdown (current, 30d, 60d, 90d, 120d+)
- Bad debt provision adequacy

**Slide: Capex Tracker**
- Approved budget vs spent vs committed
- By category (maintenance capex vs growth capex)
- ROI tracking on completed projects (planned vs actual payback)

### 3.3 PE Partner Expectations — What They Really Want

| What they ask | What they mean | How to answer |
|---------------|---------------|---------------|
| "Walk me through the bridge" | Explain WHY you missed/beat | Volume, price, cost — in that order. Quantify each. |
| "What's the cash position?" | Will you run out of money? | Cash + available facilities + 13-week forecast. Show runway. |
| "Where are we vs plan?" | Are we on track for the exit thesis? | YTD vs budget. Full-year forecast. Gap-to-plan actions. |
| "What about headcount?" | Are we hiring too fast? | FTE actual vs plan. Revenue-per-FTE trend. Planned hires. |
| "Any surprises coming?" | Don't blindside me at IC | Flag anything that could change the outlook by >5%. Early. |
| "What do you need from us?" | How can we help (and are you in control?) | Specific asks: introductions, market intel, approval for X. |

---

## 4. KPI Governance Framework

### 4.1 KPI Hierarchy

```
Level 1: Board KPIs (5-8 max)
├── Revenue growth (%)
├── EBITDA (EUR) + Margin (%)
├── Free Cash Flow (EUR)
├── Net debt / EBITDA (ratio)
├── Customer retention / NRR (%)
└── Headcount + Revenue per FTE

Level 2: Management KPIs (15-20)
├── Revenue by segment/geo
├── Gross margin by product
├── CAC (Customer Acquisition Cost)
├── LTV (Lifetime Value)
├── LTV/CAC ratio
├── Pipeline coverage (pipeline / quota)
├── Win rate (%)
├── Churn rate (%)
├── ARPU / ACV
├── Payroll as % of revenue
├── OpEx ratio
├── Capex as % of revenue
├── DSO / DPO / CCC
├── Employee NPS
└── Productivity metrics (units/FTE, revenue/FTE)

Level 3: Operational KPIs (per-team)
├── [Sales] Meetings booked, proposals sent, conversion by stage
├── [Ops] SLA adherence, utilisation, error rate
├── [Finance] Close time, reporting accuracy, forecast precision
├── [Product] Feature velocity, bug backlog, uptime
└── [HR] Time-to-hire, offer acceptance, attrition rate
```

### 4.2 KPI Definition Template

For each KPI, document:

| Field | Description |
|-------|------------|
| **Name** | Clear, unambiguous name |
| **Definition** | Exact formula (numerator / denominator) |
| **Data source** | System of record (ERP, CRM, HRIS, etc.) |
| **Frequency** | Daily / Weekly / Monthly / Quarterly |
| **Owner** | Person accountable for the number AND the outcome |
| **Target** | Budget value + stretch value |
| **Threshold** | Red / Amber / Green boundaries |
| **Trend direction** | Higher is better (↑) or lower is better (↓) |
| **Segmentation** | By geo, product, team, entity — as applicable |
| **Known limitations** | Data lag, estimation, exclusions |

### 4.3 Example: Revenue KPI Card

```
┌────────────────────────────────────────────────────────┐
│  KPI: Monthly Recurring Revenue (MRR)                  │
├────────────────────────────────────────────────────────┤
│  Definition:  Sum of all active subscription values    │
│               at month-end, normalised to monthly      │
│  Formula:     Σ (contract_value / contract_months)     │
│               for all contracts where status='active'  │
│  Source:      Billing system (Stripe / ERP)            │
│  Frequency:   Monthly (reported T+1)                   │
│  Owner:       Head of Revenue                          │
│  Target:      EUR 450K/month (budget FY26)             │
│  Thresholds:  GREEN ≥95% of target                    │
│               AMBER 85-95% of target                   │
│               RED <85% of target                       │
│  Segments:    By product tier, by geography            │
│  Limitations: Excludes one-time fees, usage overage    │
│               2-day lag from billing system sync       │
└────────────────────────────────────────────────────────┘
```

### 4.4 RAG (Red-Amber-Green) Logic

| Status | Definition | Board Communication | Action Required |
|--------|-----------|--------------------:|-----------------|
| **GREEN** | On track (≥95% of target) | Brief note, no elaboration needed | Continue executing |
| **AMBER** | At risk (85-95% of target) | Explain root cause + corrective action | Management intervention |
| **RED** | Off track (<85% of target) | Full explanation + recovery plan + timeline | Board-level discussion |

**Rule:** An item should never jump from GREEN to RED without passing through AMBER first. If it does, that signals a reporting/visibility failure — which is its own governance issue.

---

## 5. Cash & Liquidity Reporting

### 5.1 13-Week Cash Flow Forecast

```
                   Wk1    Wk2    Wk3    Wk4    Wk5    ...   Wk13
────────────────────────────────────────────────────────────────────
Opening cash       X,XXX  X,XXX  X,XXX  X,XXX  X,XXX        X,XXX

INFLOWS
  Customer receipts X,XXX  X,XXX  X,XXX  X,XXX  X,XXX        X,XXX
  Other income       XXX    XXX    XXX    XXX    XXX           XXX
────────────────────────────────────────────────────────────────────
Total inflows      X,XXX  X,XXX  X,XXX  X,XXX  X,XXX        X,XXX

OUTFLOWS
  Payroll          (X,XXX)  —      —    (X,XXX)  —          (X,XXX)
  Rent / leases    (XXX)    —      —      —      —            —
  Suppliers (AP)   (X,XXX)(X,XXX)(X,XXX)(X,XXX)(X,XXX)      (X,XXX)
  Tax payments      —       —    (X,XXX)  —      —            —
  Loan repayments   —       —      —      —    (X,XXX)        —
  Capex            (XXX)    —      —      —      —           (XXX)
  Other            (XXX)  (XXX)  (XXX)  (XXX)  (XXX)         (XXX)
────────────────────────────────────────────────────────────────────
Total outflows    (X,XXX)(X,XXX)(X,XXX)(X,XXX)(X,XXX)      (X,XXX)

Net cash flow     +/-XXX +/-XXX +/-XXX +/-XXX +/-XXX       +/-XXX
────────────────────────────────────────────────────────────────────
Closing cash       X,XXX  X,XXX  X,XXX  X,XXX  X,XXX        X,XXX
Available facility X,XXX  X,XXX  X,XXX  X,XXX  X,XXX        X,XXX
────────────────────────────────────────────────────────────────────
TOTAL LIQUIDITY    X,XXX  X,XXX  X,XXX  X,XXX  X,XXX        X,XXX
Min. cash buffer  (X,XXX)(X,XXX)(X,XXX)(X,XXX)(X,XXX)      (X,XXX)
────────────────────────────────────────────────────────────────────
HEADROOM           X,XXX  X,XXX  X,XXX  X,XXX  X,XXX        X,XXX
```

### 5.2 Cash Conversion KPIs

| KPI | Formula | Target | Frequency |
|-----|---------|--------|-----------|
| DSO | (Trade Receivables / Revenue) × Days in Period | < 45 days | Monthly |
| DPO | (Trade Payables / COGS) × Days in Period | 45-60 days | Monthly |
| DIO | (Inventory / COGS) × Days in Period | < 30 days | Monthly |
| CCC | DSO + DIO - DPO | < 30 days | Monthly |
| Cash Conversion Rate | Operating CF / EBITDA | > 80% | Quarterly |
| Runway (months) | Cash / Monthly Burn Rate | > 12 months | Monthly |

### 5.3 Covenant Monitoring (if leveraged)

| Covenant | Definition | Limit | Current | Headroom | Status |
|----------|-----------|:-----:|:-------:|:--------:|:------:|
| Net Debt / EBITDA | Total debt - cash / LTM EBITDA | < 3.5x | 2.8x | 0.7x | GREEN |
| Interest Coverage | EBITDA / Interest expense | > 3.0x | 4.2x | 1.2x | GREEN |
| Capex limit | Annual capex | < EUR 2M | EUR 1.1M | EUR 0.9M | GREEN |
| Minimum liquidity | Cash + undrawn facility | > EUR 1M | EUR 2.3M | EUR 1.3M | GREEN |
| Dividend restriction | No distributions if leverage > 2.5x | — | 2.8x | BLOCKED | AMBER |

---

## 6. Variance Analysis Standards

### 6.1 Materiality Thresholds

| Level | Threshold | Action Required |
|-------|-----------|-----------------|
| Immaterial | < EUR 10K AND < 5% of line | No commentary needed |
| Notable | EUR 10-50K OR 5-15% of line | Brief explanation (1 sentence) |
| Material | EUR 50-200K OR 15-30% of line | Full explanation + root cause + action |
| Significant | > EUR 200K OR > 30% of line | Separate deep dive slide/memo for board |

### 6.2 Variance Commentary Framework

For each material variance, answer these 4 questions:

1. **What happened?** (factual, quantified)
2. **Why?** (root cause, not symptoms)
3. **Is it recurring or one-off?** (affects forecast)
4. **What action is being taken?** (management response)

**Example (good):**
> Personnel costs exceeded budget by EUR 65K (+8%) driven by: (1) 2 unplanned hires in engineering to cover critical project deadline (EUR 40K, recurring from March); (2) overtime in operations due to seasonal peak (EUR 25K, one-off Q1 only). Action: engineering hires approved by CEO — reforecast reflects. Overtime normalising in April.

**Example (bad):**
> Personnel costs were higher than budget.

### 6.3 Variance Decomposition Logic

```
Total Variance = Volume Variance + Price Variance + Mix Variance + Efficiency Variance

Volume Variance    = (Actual qty - Budget qty) × Budget price
Price Variance     = (Actual price - Budget price) × Actual qty
Mix Variance       = Δ product mix × (product margins - average margin)
Efficiency Variance = (Actual hours - Standard hours) × Standard rate
```

---

## 7. Forecasting & Reforecasting

### 7.1 Forecast Types

| Type | When | Accuracy target | Method |
|------|------|:---------------:|--------|
| Annual budget (Plan) | October-November | ±10% by Q4 | Bottom-up + top-down reconciliation |
| Quarterly reforecast (RF) | End of each quarter | ±5% for next quarter | Actual trend + known changes |
| Rolling forecast (12-month) | Monthly | Directional | Driver-based model |
| Scenario analysis | Ad-hoc (trigger events) | N/A | Best / Base / Worst case |

### 7.2 Driver-Based Forecasting Model

Instead of forecasting each P&L line independently, link to operational drivers:

```
Revenue = Customers × ARPU × Retention Rate
    ↓
COGS = Revenue × (1 - Gross Margin %)
    ↓
Personnel = Headcount × Average Cost per FTE × (1 + Payroll Tax Rate)
    ↓
Marketing = Revenue × Marketing-as-%-of-Revenue target
    ↓
EBITDA = Revenue - COGS - Personnel - Marketing - Other OpEx
    ↓
Cash = EBITDA × Cash Conversion % - Capex - Debt Service - Tax
```

### 7.3 Forecast Accuracy Tracking

Track forecast accuracy over time to improve:

| Month | Revenue Forecast | Revenue Actual | Error (%) | Commentary |
|-------|:----------------:|:--------------:|:---------:|------------|
| Jan | 500K | 485K | -3.0% | Delayed contract |
| Feb | 510K | 520K | +2.0% | Upsell not forecasted |
| Mar | 530K | 510K | -3.8% | Churn higher than expected |
| **Q1** | **1,540K** | **1,515K** | **-1.6%** | **Within tolerance** |

Target: forecast error < 5% at monthly level, < 3% at quarterly level.

---

## 8. Investor Relations Best Practices

### 8.1 Communication Principles

1. **No surprises** — Flag potential misses EARLY (as soon as you see it, not at month-end)
2. **Quantify everything** — "Soft" is not a number. Give the EUR impact.
3. **Own the narrative** — Present your interpretation before they form theirs
4. **Show the action** — Every problem comes with a management response
5. **Be consistent** — Same format, same metrics, same definitions every month
6. **Protect credibility** — Under-promise, over-deliver. Never promise what you can't control.

### 8.2 Difficult Conversations Framework

| Situation | Approach |
|-----------|---------|
| Revenue miss | Lead with "we missed by X because [root cause]. We're doing [action]. Impact on full year is [quantified]. Recovery expected by [month]." |
| Cash crunch | Present 13-week forecast. Show exactly when and why. Present solutions (cost cuts, facility draw, accelerated collections). |
| Team attrition | Quantify replacement cost + time. Show pipeline. Present retention actions taken. |
| Market downturn | Benchmark vs competitors. Show relative performance. Present scenario analysis (base/worst). |
| Budget revision | Explain what changed vs assumptions. New baseline is [X]. Updated path to plan is [timeline]. |

### 8.3 Board Meeting Preparation Checklist

- [ ] Financial pack distributed 3 business days before meeting
- [ ] Pre-meeting call with PE partner (anticipate questions, no surprises)
- [ ] Decision items clearly flagged with recommendation
- [ ] Backup slides prepared for likely deep-dive questions
- [ ] Minutes template ready (actions, decisions, deadlines)
- [ ] Prior meeting actions tracked (status update for each)

---

## 9. Governance Documentation

### 9.1 Finance Policy Manual (Table of Contents)

1. **Chart of Accounts policy** — CoA structure, account creation/closure process
2. **Revenue recognition policy** — When and how revenue is booked (IFRS 15 / local GAAP)
3. **Expense policy** — Approval thresholds, expense categories, documentation requirements
4. **Procurement policy** — Vendor selection, PO process, three-way match
5. **Delegation of Authority (DoA)** — Who can approve what (by value and type)
6. **Treasury policy** — Bank account management, cash pooling, FX hedging
7. **Intercompany policy** — Transfer pricing, IC invoicing, reconciliation
8. **Fixed asset policy** — Capitalisation threshold, depreciation methods, impairment
9. **Provisioning policy** — Bad debt, warranty, restructuring, legal claims
10. **Close policy** — Calendar, checklist, sign-off process
11. **Reporting policy** — Templates, deadlines, distribution lists
12. **Audit policy** — External audit scope, internal audit (if applicable)
13. **Data retention policy** — What to keep, for how long, where

### 9.2 Finance Team Operating Manual

| Process | Documented? | Tested? | Single-point-of-failure? | Action |
|---------|:-----------:|:-------:|:------------------------:|--------|
| Monthly close | Yes | Yes | No (2 people trained) | — |
| Payroll | Yes | No | Yes (only Maria) | Cross-train by Q2 |
| VAT filing | Yes | Yes | No | — |
| Board reporting | Partial | No | Yes (only CFO) | Document by Q1 |
| Bank reconciliation | Yes | Yes | No | — |
| Intercompany | No | No | Yes (only Luca) | Document + cross-train Q1 |
| Budget/forecast | No | No | Yes (only CFO) | Model documentation Q2 |

---

## Appendix: Reporting Format Standards

### Number Formatting

| Element | Format | Example |
|---------|--------|---------|
| Currency | EUR with K/M suffix | EUR 1.2M, EUR 450K |
| Percentages | One decimal place | 12.3%, -5.7% |
| Negative numbers | Brackets, not minus | (EUR 150K), not -EUR 150K |
| Variances | Arrow + colour | ▲ +EUR 50K (GREEN), ▼ -EUR 80K (RED) |
| Decimals | Thousands separator = comma (EU: dot) | 1,234,567 |
| Dates | DD-MMM-YYYY | 25-Aug-2026 |

### Chart Standards

| Chart type | Use for | Never use for |
|-----------|---------|---------------|
| Line chart | Trends over time (12-month rolling) | Comparing categories |
| Bar chart | Comparing categories or periods | More than 8 categories |
| Waterfall | Bridges (budget to actual, month to month) | Trends |
| Pie chart | **Never** (PE partners hate pie charts) | Anything |
| Donut | Revenue mix (max 5 segments) | Time series |
| Bullet chart | KPI vs target | Complex comparisons |

---

*Built from real-world PE board reporting experience. For automated financial reporting and KPI dashboards, see [SCALA AI OS](https://get-scala.com).*
