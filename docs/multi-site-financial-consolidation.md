# Multi-Site Financial Consolidation

> A comprehensive framework for consolidating financial data across multiple locations, subsidiaries, branches, and franchise models. Covers owned locations, franchisees, joint ventures, and hybrid structures.

---

## Table of Contents

1. [Consolidation Models by Ownership Structure](#1-consolidation-models-by-ownership-structure)
2. [Multi-Location P&L Architecture](#2-multi-location-pl-architecture)
3. [Franchise Financial Complexity](#3-franchise-financial-complexity)
4. [Intercompany & Intra-Group Elimination](#4-intercompany--intra-group-elimination)
5. [Multi-Currency Consolidation](#5-multi-currency-consolidation)
6. [Cost Allocation Across Sites](#6-cost-allocation-across-sites)
7. [Revenue Recognition by Location Type](#7-revenue-recognition-by-location-type)
8. [Working Capital Management (Multi-Site)](#8-working-capital-management-multi-site)
9. [Reporting Hierarchy & Drill-Down](#9-reporting-hierarchy--drill-down)
10. [Consolidation Close Process](#10-consolidation-close-process)
11. [Technology Architecture](#11-technology-architecture)
12. [Real-World Scenarios](#12-real-world-scenarios)

---

## 1. Consolidation Models by Ownership Structure

### 1.1 Ownership Spectrum

| Model | Ownership | Control | Consolidation Method | P&L Treatment |
|-------|:---------:|:-------:|---------------------|---------------|
| Fully owned subsidiary | 100% | Full | Full consolidation (line-by-line) | 100% revenue & costs |
| Majority-owned subsidiary | 51-99% | Full | Full consolidation + minority interest | 100% revenue & costs; NCI in equity |
| Joint venture (JV) | 50% | Joint | Equity method (IFRS) or proportional (local GAAP) | Share of profit only (equity) |
| Associate | 20-50% | Significant influence | Equity method | Share of profit only |
| Franchise (owned brand) | 0% (franchisee owns) | Contractual | NOT consolidated — royalty income only | Franchise fees as revenue |
| Management contract | 0% | Operational | NOT consolidated — fee income only | Management fees as revenue |
| Owned branch (no legal entity) | 100% (same entity) | Full | Branch accounting (internal) | Part of parent P&L |

### 1.2 Decision Matrix: When to Consolidate What

```
                        Legal Entity?
                       /            \
                     YES             NO (branch)
                    /                    \
              Ownership ≥50%?          → Include in parent P&L
             /              \              (cost centre allocation)
           YES               NO
            |                 |
    Full consolidation    Equity method
    (line-by-line)        (profit share only)
            |
    Minority interest?
    /              \
  YES               NO (100% owned)
   |                  |
  NCI line in      Clean consolidation
  equity + P&L     (no adjustments)
```

### 1.3 Hybrid Structures (Common in Retail, Hospitality, Healthcare)

Many real-world companies operate with a MIX:

```
Example: RestaurantCo Group
├── 12 fully owned restaurants (full consolidation)
├── 35 franchise restaurants (royalty income only)
├── 3 joint ventures with local partners (equity method)
├── 1 central kitchen (cost centre, shared service)
└── 2 ghost kitchens (managed by third party, management fee income)
```

**Key challenge:** The board wants a "total network view" (all 53 locations) while accounting standards require different treatment. Solution: dual reporting — statutory (GAAP-compliant) + management (operational, full network).

---

## 2. Multi-Location P&L Architecture

### 2.1 P&L Hierarchy

```
Level 0: Group Consolidated P&L
├── Level 1: By Legal Entity (statutory)
│   ├── Entity IT-01 (Italy Subsidiary 1)
│   ├── Entity IT-02 (Italy Subsidiary 2)
│   └── Entity FR-01 (France Parent)
│
├── Level 1: By Region (management)
│   ├── North Italy (10 locations)
│   ├── Central Italy (8 locations)
│   ├── South Italy (5 locations)
│   └── France (2 locations)
│
├── Level 1: By Format/Concept (management)
│   ├── Premium locations (high-margin)
│   ├── Standard locations (volume)
│   └── Express/compact locations (low-cost)
│
└── Level 0: Individual Location P&L (granular)
    ├── Location MIL-001 (Via Montenapoleone, Milan)
    ├── Location MIL-002 (Corso Buenos Aires, Milan)
    └── ... (N locations)
```

### 2.2 Standard Location P&L Template

```
═══════════════════════════════════════════════════════════════════════════════
LOCATION P&L — [Location Code] [Location Name]           Period: [Month Year]
═══════════════════════════════════════════════════════════════════════════════

                              Actual    Budget    Var      Var%    PY      LFL%
─────────────────────────────────────────────────────────────────────────────
REVENUE
  Core revenue (products/     XXX,XXX   XXX,XXX  +/-XXX   X%     XXX,XXX  X%
   services)
  Ancillary revenue            XX,XXX    XX,XXX  +/-XXX   X%      XX,XXX  X%
  (add-ons, upsells)
─────────────────────────────────────────────────────────────────────────────
TOTAL REVENUE                 XXX,XXX   XXX,XXX  +/-XXX   X%     XXX,XXX  X%
═══════════════════════════════════════════════════════════════════════════════

DIRECT COSTS (variable, attributable to this location)
  Cost of goods/materials     (XX,XXX)  (XX,XXX) +/-XXX   X%    (XX,XXX)
  Direct labour               (XX,XXX)  (XX,XXX) +/-XXX   X%    (XX,XXX)
  Location-specific marketing  (X,XXX)   (X,XXX) +/-XXX   X%     (X,XXX)
  Utilities (elec, gas, water) (X,XXX)   (X,XXX) +/-XXX   X%     (X,XXX)
  Maintenance & repairs        (X,XXX)   (X,XXX) +/-XXX   X%     (X,XXX)
─────────────────────────────────────────────────────────────────────────────
TOTAL DIRECT COSTS           (XXX,XXX) (XXX,XXX) +/-XXX   X%   (XXX,XXX)
─────────────────────────────────────────────────────────────────────────────
CONTRIBUTION MARGIN (CM1)     XXX,XXX   XXX,XXX  +/-XXX   X%    XXX,XXX
CM1 %                           XX.X%     XX.X%                    XX.X%
═══════════════════════════════════════════════════════════════════════════════

LOCATION OVERHEADS (fixed, attributable)
  Rent / lease costs          (XX,XXX)  (XX,XXX) +/-XXX   X%    (XX,XXX)
  Location management salary  (XX,XXX)  (XX,XXX) +/-XXX   X%    (XX,XXX)
  Insurance                    (X,XXX)   (X,XXX) +/-XXX   X%     (X,XXX)
  Depreciation (fitout, eqpt) (XX,XXX)  (XX,XXX) +/-XXX   X%    (XX,XXX)
  Local taxes & fees           (X,XXX)   (X,XXX) +/-XXX   X%     (X,XXX)
─────────────────────────────────────────────────────────────────────────────
TOTAL LOCATION OVERHEADS      (XX,XXX)  (XX,XXX) +/-XXX   X%    (XX,XXX)
─────────────────────────────────────────────────────────────────────────────
LOCATION EBITDA (CM2)          XX,XXX    XX,XXX  +/-XXX   X%     XX,XXX
CM2 %                           XX.X%     XX.X%                    XX.X%
═══════════════════════════════════════════════════════════════════════════════

ALLOCATED COSTS (from central / HQ)
  Central services allocation  (X,XXX)   (X,XXX) +/-XXX         (X,XXX)
  Brand/marketing allocation   (X,XXX)   (X,XXX) +/-XXX         (X,XXX)
  IT systems allocation        (X,XXX)   (X,XXX) +/-XXX         (X,XXX)
  Management fee (if franchise)(X,XXX)   (X,XXX) +/-XXX         (X,XXX)
─────────────────────────────────────────────────────────────────────────────
FULLY LOADED LOCATION PROFIT   XX,XXX    XX,XXX  +/-XXX   X%     XX,XXX
─────────────────────────────────────────────────────────────────────────────

NON-P&L METRICS
  Transactions / covers        X,XXX     X,XXX   +/-XXX   X%     X,XXX
  Average ticket              EUR XX    EUR XX   +/-XX           EUR XX
  FTE (headcount)               XX.X      XX.X   +/-X.X           XX.X
  Revenue per FTE            EUR X,XXX EUR X,XXX +/-XXX         EUR X,XXX
  Revenue per sqm            EUR XXX   EUR XXX   +/-XX          EUR XXX
  Capacity utilisation          XX%       XX%                      XX%
═══════════════════════════════════════════════════════════════════════════════
```

### 2.3 Like-for-Like (LFL) Analysis

**LFL revenue growth** compares only locations that were open in both the current AND prior period (excludes new openings and closures):

```
LFL Revenue Growth = (Revenue of comparable locations this year / Revenue of same locations last year) - 1

Criteria for inclusion in LFL:
- Open for full 12 months in current year AND prior year
- No major renovation closure (> 4 weeks)
- No format change
- Same ownership model (wasn't converted from franchise to owned)
```

| Category | Locations | Revenue CY | Revenue PY | LFL Growth |
|----------|:---------:|:----------:|:----------:|:----------:|
| LFL (comparable) | 45 | EUR 12.5M | EUR 11.8M | +5.9% |
| New openings (< 12 months) | 5 | EUR 1.2M | — | N/A |
| Closures / conversions | 3 | — | EUR 0.8M | N/A |
| **Total network** | **53** | **EUR 13.7M** | **EUR 12.6M** | **+8.7%** |

**LFL is the KPI PE cares about most** — it shows organic growth without the "noise" of network expansion.

---

## 3. Franchise Financial Complexity

### 3.1 Franchise Revenue Streams (Franchisor Perspective)

| Revenue Type | Basis | Typical Range | Timing | Accounting Treatment |
|-------------|-------|:-------------:|--------|---------------------|
| Initial franchise fee | One-time, at signing | EUR 20-100K | Recognised over contract term (IFRS 15) | Deferred + amortised |
| Ongoing royalty | % of franchisee gross revenue | 4-8% of revenue | Monthly, based on reported sales | Accrued monthly |
| Marketing fund contribution | % of franchisee revenue | 1-3% of revenue | Monthly | Restricted use (offset by marketing spend) |
| Supply chain margin | Markup on mandatory supplies | 5-15% markup | Per-transaction | Revenue or net (policy choice) |
| Technology / POS fee | Fixed monthly per location | EUR 200-500/month | Monthly | SaaS-like revenue |
| Training fees | Per-event or per-person | EUR 1-5K per session | At delivery | Point-in-time revenue |
| Transfer fee | When franchisee sells to new franchisee | % of sale price (1-3%) | At transfer | Point-in-time revenue |
| Renewal fee | At contract renewal | EUR 5-20K | At renewal | Point-in-time or deferred |

### 3.2 Franchisee P&L (Franchisor Must Monitor)

Even though franchisees are not consolidated, the franchisor MUST monitor their financial health:

```
Franchisee Unit Economics (Franchisor Monitoring View)
═════════════════════════════════════════════════════════
Revenue (reported by franchisee POS)           EUR 450,000 / year
─────────────────────────────────────────────────────────────────
(-) COGS                                      (EUR 135,000)  30%
(-) Labour                                    (EUR 135,000)  30%
(-) Rent                                       (EUR 54,000)  12%
(-) Royalty to franchisor                      (EUR 27,000)   6%
(-) Marketing fund                             (EUR 9,000)    2%
(-) Technology fee                             (EUR 3,600)    0.8%
(-) Other operating costs                      (EUR 36,000)   8%
═════════════════════════════════════════════════════════════════
Franchisee EBITDA                               EUR 50,400   11.2%
(-) Loan repayment (initial investment)        (EUR 30,000)
═════════════════════════════════════════════════════════════════
Franchisee cash flow (before tax)               EUR 20,400    4.5%
═════════════════════════════════════════════════════════════════

Franchisor target: Franchisee EBITDA > 10% (healthy)
Red flag: Franchisee EBITDA < 5% → risk of closure / non-payment
```

### 3.3 Franchise Financial Risks for the Franchisor

| Risk | Description | Financial Impact | Mitigation |
|------|-------------|-----------------|------------|
| Revenue under-reporting | Franchisee reports less than actual sales | Lower royalty income | POS system integration, mystery audits |
| Franchisee insolvency | Franchisee can't pay royalties or debts | Bad debt write-off + location loss | Credit checks, minimum capital requirements |
| Brand damage | Poor franchisee operations hurt brand | Reduced network revenue | Operating standards, inspection programme |
| Territory cannibalisation | Too many locations in same area | Reduced LFL growth | Territory mapping, minimum distance rules |
| Supply chain disputes | Franchisee sources outside approved network | Lost supply margin + quality risk | Contractual mandatory sourcing |
| Lease complications | Franchisor is head-lessee; franchisee defaults | Lease liability remains with franchisor | Direct lease structure or sublease protection |

### 3.4 Franchise vs Owned: Financial Comparison Matrix

| Dimension | Owned Location | Franchise Location |
|-----------|:-------------:|:-----------------:|
| Revenue capture | 100% revenue | 6-12% of revenue (royalty + fees) |
| Capex investment | EUR 200-500K per location | EUR 0 (franchisee invests) |
| Operating risk | High (we bear all costs) | Low (franchisee bears costs) |
| Margin | 15-25% EBITDA (if managed well) | 85-95% margin (royalty is almost pure profit) |
| Growth speed | Slow (capital-constrained) | Fast (franchisee capital) |
| Control | Full operational control | Contractual control only |
| Exit valuation | Revenue multiple × owned revenue | Revenue multiple × royalty stream |
| Working capital | Significant (inventory, receivables) | Minimal (monthly royalty collection) |

**Strategic implication for consolidation:** A network of 10 owned + 40 franchise generates LESS revenue (top-line) but potentially HIGHER margins and LOWER capital intensity than 50 owned locations. PE valuation models must distinguish between owned and franchise revenue streams (different multiples apply).

---

## 4. Intercompany & Intra-Group Elimination

### 4.1 Common Intercompany Transactions in Multi-Site

| Transaction | From | To | Elimination Entry |
|------------|------|-----|-------------------|
| Central services charge | HQ entity | Subsidiary | Dr IC Revenue (HQ) / Cr IC Cost (Sub) → eliminated |
| Inventory transfer | Central warehouse | Branch entities | Eliminate IC margin on unsold inventory |
| Management fee | Parent | Subsidiaries | Dr IC Revenue (Parent) / Cr IC Cost (Sub) → eliminated |
| Brand royalty | IP holding entity | Operating entities | Dr IC Revenue (IP) / Cr IC Cost (Operating) → eliminated |
| IC loan interest | Lending entity | Borrowing entity | Dr IC Finance Income / Cr IC Finance Cost → eliminated |
| IC dividend | Subsidiary | Parent | Eliminate against investment value |
| IC asset transfer | Selling entity | Buying entity | Eliminate gain/loss; adjust asset to original cost |

### 4.2 Elimination Logic (Automated Rules)

```sql
-- Example: Auto-generate elimination journal entries
-- Rule 1: IC Revenue vs IC Cost elimination
INSERT INTO journal_entries (entity, account, amount, description)
SELECT
    'ELIM' as entity,
    CASE
        WHEN direction = 'revenue' THEN ic_revenue_account
        WHEN direction = 'cost' THEN ic_cost_account
    END as account,
    CASE
        WHEN direction = 'revenue' THEN -amount  -- Debit (reduce revenue)
        WHEN direction = 'cost' THEN amount      -- Credit (reduce cost)
    END as amount,
    'IC elimination: ' || counterparty_entity as description
FROM intercompany_transactions
WHERE period = current_period
  AND status = 'confirmed'  -- Both parties agree
```

### 4.3 Unrealised Profit Elimination (Inventory)

When Entity A sells inventory to Entity B at a markup, and Entity B has not sold it externally by period end:

```
Entity A sells to Entity B:
- Cost to A:       EUR 100
- IC selling price: EUR 120 (20% markup)
- Entity B's book value: EUR 120

If Entity B still holds EUR 60K of this inventory at month-end:

Unrealised profit = EUR 60K × (20/120) = EUR 10K

Elimination entry:
  Dr Retained Earnings / IC Profit (ELIM)    EUR 10K
  Cr Inventory (ELIM)                        EUR 10K

→ Consolidated inventory shown at original group cost (EUR 50K), not inflated IC price
```

---

## 5. Multi-Currency Consolidation

### 5.1 Translation Methods

| Method | When Used | Balance Sheet | P&L | FX Difference |
|--------|-----------|:------------:|:---:|:-------------:|
| **Closing rate** | Foreign subsidiary (functional ≠ presentation currency) | Closing rate at BS date | Average rate for period | Translation reserve (OCI) |
| **Temporal** | Subsidiary operates in parent's currency (extension of parent) | Historical rate (non-monetary) / Closing rate (monetary) | Historical rate | P&L impact |

### 5.2 FX Exposure Types in Multi-Site Operations

| Exposure | Description | Example | Hedge? |
|----------|-------------|---------|--------|
| **Transaction** | Committed future cash flow in foreign currency | Italian sub buys supplies in USD | Yes — forward contract |
| **Translation** | Converting foreign sub FS to group presentation currency | French parent consolidates Italian sub in EUR | Usually no (non-cash) |
| **Economic** | Competitive position affected by long-term FX moves | EUR strengthens → Italian exports less competitive | Strategic pricing decisions |

### 5.3 Multi-Currency Close Process

```
Step 1: Each subsidiary closes in its FUNCTIONAL currency (local)
Step 2: IC transactions matched in original currency (both parties)
Step 3: IC balances re-measured at closing rate
Step 4: FX difference on IC loans: P&L (monetary item)
Step 5: Full subsidiary P&L translated at average rate for period
Step 6: Full subsidiary BS translated at closing rate
Step 7: FX translation difference → Other Comprehensive Income (OCI)
Step 8: Elimination entries in GROUP presentation currency
Step 9: Consolidated Trial Balance produced
```

---

## 6. Cost Allocation Across Sites

### 6.1 Allocation Methodology

| Cost Type | Allocation Key | Rationale |
|-----------|---------------|-----------|
| Central finance team | Revenue share | Finance effort correlates with transaction volume |
| IT systems / ERP | Headcount or user count | System cost driven by users |
| Marketing (brand) | Revenue share | Locations benefiting proportionally |
| Marketing (local) | Direct attribution | Assigned to specific location |
| Senior management | Equal share (flat) | Governance cost shared equally |
| Warehousing / logistics | Units shipped or weight | Cost driven by physical throughput |
| Insurance (property) | Sqm (floor area) | Premium based on insured area |
| Insurance (liability) | Revenue or headcount | Risk proportional to activity |
| HR & recruitment | Headcount | Direct correlation |
| Rent (shared office) | Sqm occupied or desks | Physical space usage |
| Depreciation (shared assets) | Usage hours or throughput | Activity-based |

### 6.2 Allocation Policy: Principles

1. **Causality** — The allocation key should reflect what CAUSES the cost
2. **Materiality** — Don't allocate EUR 500/month across 50 locations (EUR 10 each is noise)
3. **Controllability** — Location managers should only be measured on costs they can influence
4. **Consistency** — Same method every month (no switching to flatter a location)
5. **Transparency** — Every location controller must understand and agree with the methodology

### 6.3 Two-Tier Margin Reporting

| Level | Name | What's Included | Purpose |
|-------|------|-----------------|---------|
| CM1 | Contribution Margin | Revenue - Direct Costs (variable) | Shows location's direct economic contribution |
| CM2 | Location EBITDA | CM1 - Location Overheads (fixed, attributable) | Shows location's standalone viability |
| CM3 | Fully Loaded Profit | CM2 - Allocated Central Costs | Shows true group-level profitability per location |

**Management decision rule:**
- If CM1 < 0 → Close immediately (not covering variable costs)
- If CM1 > 0 but CM2 < 0 → Location is loss-making; investigate if fixable within 6 months, else close
- If CM2 > 0 but CM3 < 0 → Location is viable standalone but doesn't cover its share of central; acceptable if marginal contribution positive

---

## 7. Revenue Recognition by Location Type

### 7.1 Revenue Recognition Scenarios

| Business Model | Revenue Event | Timing | IFRS 15 Performance Obligation |
|---------------|---------------|--------|-------------------------------|
| Retail (point of sale) | Customer pays at POS | At transaction | Satisfied at point in time |
| Subscription / membership | Monthly recurring | Over time (monthly) | Satisfied over time |
| Long-term rental | Monthly rental fee | Over lease term | Satisfied over time |
| Franchise royalty | % of franchisee sales | Monthly (when franchisee reports) | Satisfied over time |
| Installation + maintenance | Install fee + monthly | Split: install at completion; maintenance over time | Two distinct obligations |
| Prepaid services | Customer prepays | When service is delivered | Deferred until delivery |
| Gift cards / vouchers | Sold to customer | When redeemed (or breakage estimate) | Deferred until redemption |

### 7.2 Long-Term Rental Revenue Complexity

For vehicle rental, equipment leasing, or property management:

```
Monthly rental revenue recognition:
─────────────────────────────────────────────────────────────
Contract value:           EUR 500 / month × 48 months = EUR 24,000
Delivery date:            15 March 2026
First invoice:            01 April 2026
Revenue recognition:      01 April 2026 onward (straight-line)

Additional complexity:
├── Early termination fee: recognised only when triggered (contingent)
├── Excess mileage/usage: recognised at end of contract (variable consideration)
├── Insurance bundled:     separate performance obligation (allocated)
├── Maintenance included:  separate performance obligation (allocated over time)
└── Residual value gain:   recognised at return/disposal (end of contract)

Month-end accrual (if billing ≠ revenue period):
- Contract starts 15 March → 16 days of March revenue accrued
- Revenue = EUR 500 × (16/31) = EUR 258.06 accrued in March
- Remaining EUR 241.94 allocated to April
```

### 7.3 Fleet/Asset Financial Lifecycle (Long-Term Rental)

```
ASSET ACQUISITION
│ Purchase price: EUR 25,000
│ Registration & delivery: EUR 1,200
│ Total capitalised cost: EUR 26,200
│
├── DEPRECIATION (straight-line over useful life)
│   Useful life: 48 months
│   Residual value estimate: EUR 8,000
│   Monthly depreciation: (26,200 - 8,000) / 48 = EUR 379.17 / month
│
├── REVENUE (rental contract)
│   Monthly rental: EUR 500
│   Annual revenue per asset: EUR 6,000
│   Revenue over 48 months: EUR 24,000
│
├── DIRECT COSTS (per asset)
│   Insurance: EUR 80/month
│   Maintenance provision: EUR 50/month
│   Road tax: EUR 20/month
│   Total direct cost: EUR 150/month
│
├── MONTHLY P&L PER ASSET
│   Revenue:         EUR 500
│   (-) Direct costs: (EUR 150)
│   (-) Depreciation: (EUR 379)
│   ═══════════════════════════
│   Monthly margin:  EUR (29)  ← appears loss-making monthly!
│
└── END OF CONTRACT
    Sale price achieved: EUR 10,000
    Book value at month 48: EUR 8,000 (residual)
    Gain on disposal: EUR 2,000 ← THIS is where rental makes money

    TOTAL LIFECYCLE MARGIN:
    Revenue (48 months):     EUR 24,000
    Direct costs (48 months): (EUR 7,200)
    Depreciation:            (EUR 18,200)
    Gain on disposal:        + EUR 2,000
    ═══════════════════════════════════════
    Lifecycle margin:         EUR 600 per asset (2.3% of revenue)

    → If residual was underestimated by EUR 3,000: +EUR 3,000 upside
    → If residual was overestimated by EUR 3,000: -EUR 3,000 writedown
```

**Key insight:** Long-term rental profitability is HIGHLY sensitive to residual value assumptions. A 10% error in residual estimate across a fleet of 500 vehicles = EUR 1.25M P&L swing. This is why fleet management companies must:
- Update residual value estimates quarterly
- Track disposal prices vs estimates
- Build residual value risk into pricing
- Maintain strict vehicle condition standards (protect resale)

---

## 8. Working Capital Management (Multi-Site)

### 8.1 Working Capital by Location Type

| Component | Owned Retail | Franchise | Long-Term Rental | Services |
|-----------|:-----------:|:---------:|:----------------:|:--------:|
| Inventory | HIGH (stock on shelves) | None (franchisee owns) | MEDIUM (spare parts) | LOW/None |
| Trade receivables | LOW (B2C = immediate) | MEDIUM (royalty collection) | HIGH (B2B monthly billing) | HIGH (B2B invoicing) |
| Trade payables | HIGH (supplier terms) | LOW (minimal direct purchases) | HIGH (fleet procurement) | MEDIUM |
| Prepayments | MEDIUM (rent deposits, insurance) | LOW | HIGH (insurance prepaid) | LOW |
| Deferred revenue | LOW | LOW | HIGH (prepaid rentals) | MEDIUM (retainers) |

### 8.2 Cash Pooling Structure

```
GROUP CASH POOL (Zero-balancing)
═══════════════════════════════════════════════════════════
Master Account (Parent / Treasury entity)
├── Sub-account: Entity IT-01 (auto-sweep daily)
├── Sub-account: Entity IT-02 (auto-sweep daily)
├── Sub-account: Entity IT-03 (auto-sweep daily)
├── Sub-account: Entity FR-01 (auto-sweep daily)
└── Operating accounts (ring-fenced):
    ├── Payroll account (funded weekly)
    ├── Tax account (funded before due dates)
    └── Capex account (funded per approval)

Benefits:
- Reduced borrowing cost (net position lower)
- Central visibility on group cash
- Subsidiaries don't hold idle cash
- Simplified bank relationship management

Intercompany implication:
- Each daily sweep creates IC balance (subsidiary "owes" parent or vice versa)
- IC interest calculated monthly at arm's-length rate
- Transfer pricing documentation required
```

### 8.3 Cash Collection by Model

| Collection Model | DSO Target | Process | Risk |
|-----------------|:----------:|---------|------|
| POS / card payments | 0-2 days | Automatic settlement from payment processor | Chargebacks |
| Direct debit (rental/subscription) | 0-3 days | Mandated DD on contract start | Failed DDs, mandate cancellation |
| Invoice (B2B) | 30-60 days | Invoice → reminder → escalation → collection | Bad debt, disputes |
| Franchise royalty | 15-30 days | Self-report + automatic debit from franchisee account | Under-reporting, non-payment |
| Prepaid / deposit | Negative DSO | Cash collected before service delivered | Refund liability |

---

## 9. Reporting Hierarchy & Drill-Down

### 9.1 Reporting Dimensions

Every transaction should be tagged with:

| Dimension | Purpose | Example Values |
|-----------|---------|----------------|
| Legal Entity | Statutory consolidation | IT-01, IT-02, FR-01 |
| Location / Site | Operational reporting | MIL-001, ROM-003, PAR-001 |
| Region / Area | Geographic analysis | North, Central, South, International |
| Format / Concept | Business model analysis | Premium, Standard, Express, Franchise |
| Ownership type | Consolidation method | Owned, Franchise, JV |
| Cost Centre | Responsibility accounting | Sales, Ops, Admin, Shared |
| Product / Service Line | Revenue analysis | Product A, Service B, Rental C |
| Customer Segment | Commercial analysis | B2C, B2B, Enterprise, SMB |
| Project / Initiative | Capex tracking | New opening MIL-005, Renovation ROM-002 |

### 9.2 Drill-Down Path

```
Group EBITDA: EUR 2.4M (12.0% margin)
│
├── By Region:
│   ├── North Italy: EUR 1.2M (14.0%)  ← Best performing
│   ├── Central Italy: EUR 0.7M (11.5%)
│   ├── South Italy: EUR 0.3M (8.0%)   ← Underperforming
│   └── France: EUR 0.2M (13.0%)
│       │
│       └── Drill into South Italy:
│           ├── NAP-001: EUR 120K (10.0%)
│           ├── NAP-002: EUR 80K (7.5%)
│           ├── BAR-001: EUR 60K (6.0%)  ← Investigate
│           ├── PAL-001: EUR 50K (9.0%)
│           └── CAT-001: EUR (10K) (-2.0%)  ← LOSS: closure candidate
│               │
│               └── Drill into CAT-001:
│                   ├── Revenue: EUR 500K (-15% vs PY)  ← Market decline
│                   ├── COGS: (EUR 175K) (35% ratio, vs 30% norm)  ← Cost issue
│                   ├── Labour: (EUR 180K) (36%, vs 28% norm)  ← Overstaffed
│                   ├── Rent: (EUR 72K) (14.4%, vs 10% norm)  ← Above market
│                   └── Action: Renegotiate rent + reduce 2 FTE → breakeven by Q3
```

### 9.3 Management vs Statutory Reporting Views

| Dimension | Statutory View | Management View |
|-----------|:-------------:|:---------------:|
| Entity boundary | Legal entity (mandatory) | Can cross legal entities |
| Franchise locations | Excluded (not consolidated) | Included (operational KPIs) |
| Transfer pricing | At arm's length (tax) | At cost (true margin) |
| Cost allocation | As booked (actual entity) | Re-allocated by usage |
| Minority interest | Separate line in equity | Ignored (operational focus) |
| JV | Equity method (one line) | Proportional or full (operational) |
| Currency | Presentation currency (EUR) | Can show in local currency |

---

## 10. Consolidation Close Process

### 10.1 Monthly Consolidation Calendar

| Day | Activity | Responsible | System |
|-----|----------|-------------|--------|
| T+1 | Location daily revenue reconciliation (POS vs bank) | Location manager | POS + Bank |
| T+2 | Location-level P&L prelim close | Location controller | ERP |
| T+3 | Regional consolidation (sum of locations) | Regional controller | ERP / BI |
| T+3 | Intercompany matching (all entities) | IC coordinator | IC matching tool |
| T+4 | Entity-level trial balance locked | Entity controller | ERP |
| T+4 | Management adjustments (reclasses, accruals) | Group controller | Consolidation tool |
| T+5 | Elimination entries auto-generated | System | Consolidation tool |
| T+5 | FX translation applied | System | Consolidation tool |
| T+6 | Consolidated trial balance produced | Group controller | Consolidation tool |
| T+6 | Variance analysis vs budget + PY | FP&A analyst | BI / Excel |
| T+7 | Management commentary drafted | Subsidiary controllers | Template |
| T+8 | CFO review (challenge session) | CFO | Meeting |
| T+9 | Final adjustments (if any) | Group controller | Consolidation tool |
| T+10 | Monthly financial pack distributed | FP&A | PDF / Email |

### 10.2 Consolidation Checklist

- [ ] All entities closed and locked (no further postings)
- [ ] IC balances match (zero net IC position after elimination)
- [ ] FX rates applied (ECB rate at period end for BS, average for P&L)
- [ ] Minority interest calculated correctly
- [ ] Elimination entries balance (total eliminations net to zero)
- [ ] Group equity reconciled (opening + P&L + OCI + dividends = closing)
- [ ] Cash reconciles (per-entity cash = sum of bank accounts)
- [ ] No orphan transactions (all transactions have entity + location tag)

---

## 11. Technology Architecture

### 11.1 Multi-Site Finance Tech Stack

```
┌──────────────────────────────────────────────────────────────┐
│                    PRESENTATION LAYER                         │
│  ┌─────────────┐  ┌──────────────┐  ┌───────────────────┐  │
│  │ Board Pack  │  │ BI Dashboard │  │ Location Scorecard│  │
│  │ (PDF/PPT)   │  │ (real-time)  │  │ (mobile app)      │  │
│  └─────────────┘  └──────────────┘  └───────────────────┘  │
├──────────────────────────────────────────────────────────────┤
│                    ANALYTICS LAYER                            │
│  ┌────────────────────────────────────────────────────────┐ │
│  │  BI Platform (Power BI / Tableau / Metabase / Custom)  │ │
│  │  - Pre-built views: Location P&L, Regional, Group      │ │
│  │  - Drill-down from group → region → location           │ │
│  │  - Alert engine: KPI threshold breaches                │ │
│  └────────────────────────────────────────────────────────┘ │
├──────────────────────────────────────────────────────────────┤
│                 CONSOLIDATION LAYER                           │
│  ┌────────────────────────────────────────────────────────┐ │
│  │  Consolidation Engine                                   │ │
│  │  - CoA mapping (local → group)                         │ │
│  │  - IC matching & elimination                           │ │
│  │  - FX translation                                      │ │
│  │  - Minority interest calculation                       │ │
│  │  - Audit trail on every adjustment                     │ │
│  └────────────────────────────────────────────────────────┘ │
├──────────────────────────────────────────────────────────────┤
│                   DATA LAYER                                  │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐   │
│  │ ERP      │  │ POS      │  │ Payroll  │  │ Bank     │   │
│  │ (GL, AP, │  │ (daily   │  │ (monthly │  │ (daily   │   │
│  │  AR, FA) │  │  revenue)│  │  journal)│  │  feeds)  │   │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘   │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐                  │
│  │ CRM      │  │ Fleet    │  │ Franchise│                  │
│  │ (pipeline│  │ Mgmt     │  │ Portal   │                  │
│  │  , churn)│  │ (assets) │  │ (royalty)│                  │
│  └──────────┘  └──────────┘  └──────────┘                  │
└──────────────────────────────────────────────────────────────┘
```

### 11.2 Data Flow (Daily → Monthly)

| Frequency | Data | Source | Destination | Purpose |
|-----------|------|--------|-------------|---------|
| Real-time | POS transactions | POS terminals | Data warehouse | Revenue monitoring |
| Daily | Bank movements | Bank API | Treasury module | Cash position |
| Daily | Card settlements | Payment processor | Bank reconciliation | Verify receipts |
| Weekly | Payroll accrual | HRIS | GL | Labour cost estimate |
| Monthly | Full close entries | ERP | Consolidation | Official P&L |
| Monthly | Franchise royalty reports | Franchise portal | Revenue booking | Franchise income |
| Quarterly | Residual value review | Fleet management | Depreciation adjustment | Asset accuracy |

---

## 12. Real-World Scenarios

### Scenario A: Italian Group Acquires 5 Local Companies

**Context:** French parent acquires 5 Italian SMEs (EUR 2-10M each). Each has its own commercialista, different accounting software, different CoA. No intercompany activity existed before.

**Challenges:**
- 5 different charts of accounts (some barely structured)
- 3 different accounting systems (2× TeamSystem, 1× Zucchetti, 2× Excel-only)
- Close discipline ranges from T+5 (best) to T+45 (worst — basically annual-only)
- No one understands "group reporting requirements"
- Italian statutory requirements (bilancio, nota integrativa, SDI) must continue

**Approach:**
1. **Phase 1 (Month 1-3):** Mapping layer only. Keep local systems. Extract monthly TB via Excel export → central consolidation model.
2. **Phase 2 (Month 3-6):** Enforce close calendar (start at T+15, tighten to T+7). Implement IC framework.
3. **Phase 3 (Month 6-12):** Evaluate single-ERP migration OR permanent middleware. Depends on group long-term IT strategy.

### Scenario B: Restaurant Chain with Mixed Owned/Franchise

**Context:** 50 locations (15 owned, 35 franchised). Owned locations on single ERP. Franchisees have their own systems but report via franchise portal.

**Challenges:**
- Statutory P&L only includes owned locations + franchise fee income
- Management wants full network view (all 50 locations)
- Franchise royalty income depends on franchisee-reported revenue (trust issue)
- Different cost structures between owned and franchise (rent, labour policies)
- New openings pipeline includes both owned and franchise → different capex profiles

**Approach:**
1. **Statutory view:** Consolidate 15 owned. Franchise income = royalty line in P&L.
2. **Management view:** Build "network P&L" including estimated franchise unit economics. Use POS data (franchisor-controlled) as revenue source of truth.
3. **KPI dashboard:** LFL growth for both owned AND franchise (separately and combined). Flag franchise locations below EBITDA threshold for intervention.

### Scenario C: Long-Term Rental Company (70 Branches)

**Context:** Vehicle rental company with 70 branches, 5000 vehicles, EUR 33M revenue. Each branch is a profit centre but all within same legal entity. Acquired by international group.

**Challenges:**
- Branch managers think in "vehicles rented" not "EBITDA per branch"
- Fleet depreciation is 40% of costs — residual value assumptions drive P&L
- Seasonality extreme (summer = 95% utilisation, winter = 60%)
- Multi-location: vehicle can be picked up in Milan, returned in Rome → revenue allocation
- Acquirer wants monthly management reporting to group standards (from annual reporting baseline)

**Approach:**
1. **Branch P&L:** Revenue (rentals + ancillary) - Direct costs (insurance, maintenance, cleaning) - Allocated fleet depreciation (by vehicles assigned to branch) - Branch overheads (rent, local staff)
2. **Fleet profitability:** Lifecycle margin per vehicle. Track depreciation vs disposal price. Quarterly residual value review committee.
3. **Revenue allocation rule:** Revenue attributed to pickup branch (simplicity; industry standard).
4. **Utilisation reporting:** Daily fleet utilisation by branch. Threshold alerts (<70% for >2 weeks → investigate or redeploy vehicles).

---

*Built from real-world experience consolidating 70+ locations post-acquisition. For automated multi-site consolidation, see [SCALA AI OS](https://get-scala.com).*
