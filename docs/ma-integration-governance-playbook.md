# M&A Integration Governance Playbook — Finance Workstream

> A complete operational framework for integrating acquired subsidiaries into a group's financial structure. Covers Day-0 (signing) through Day-100+ (steady-state harmonisation).

---

## Table of Contents

1. [Integration Management Office (IMO) Setup](#1-integration-management-office-imo-setup)
2. [Day-0 Assessment: Financial Due Diligence Handover](#2-day-0-assessment-financial-due-diligence-handover)
3. [Chart of Accounts (CoA) Harmonisation](#3-chart-of-accounts-coa-harmonisation)
4. [Close Calendar Alignment](#4-close-calendar-alignment)
5. [ERP & Systems Integration Roadmap](#5-erp--systems-integration-roadmap)
6. [Intercompany Framework](#6-intercompany-framework)
7. [Tax & Statutory Compliance Alignment](#7-tax--statutory-compliance-alignment)
8. [Governance & Controls Framework](#8-governance--controls-framework)
9. [Communication & Change Management](#9-communication--change-management)
10. [Day-1 to Day-100 Timeline](#10-day-1-to-day-100-timeline)
11. [Risk Register](#11-risk-register)
12. [Success Metrics](#12-success-metrics)

---

## 1. Integration Management Office (IMO) Setup

### 1.1 Governance Structure

```
Group CFO (FR)
    └── IMO Lead (Finance Workstream PM)
            ├── CoA & Reporting Stream Lead
            ├── Systems & ERP Stream Lead
            ├── Tax & Compliance Stream Lead
            └── Per-subsidiary Finance Liaison (x N)
```

### 1.2 Roles & Responsibilities (RACI)

| Activity | Group CFO | IMO Lead | Stream Lead | Subsidiary Controller | External Auditor |
|----------|:---------:|:--------:|:-----------:|:---------------------:|:----------------:|
| Integration strategy approval | A | R | C | I | I |
| CoA mapping decisions | I | A | R | C | C |
| Close calendar definition | A | R | R | C | I |
| ERP migration go/no-go | A | R | R | C | I |
| Monthly close execution | I | I | C | R | I |
| Statutory filing | I | I | C | R | A |
| Intercompany policy | A | R | R | C | C |
| Controls testing | I | A | R | R | C |

**Legend:** R = Responsible, A = Accountable, C = Consulted, I = Informed

### 1.3 Cadence

| Meeting | Frequency | Attendees | Duration | Output |
|---------|-----------|-----------|----------|--------|
| IMO Steering Committee | Bi-weekly | Group CFO, IMO Lead, Stream Leads | 60 min | Decision log, risk escalation |
| Stream Working Sessions | Weekly | Stream Lead + subsidiary counterparts | 90 min | Action tracker update |
| Subsidiary Touchpoints | Weekly | IMO Lead + subsidiary controller | 30 min | Progress, blockers, change requests |
| Group Board Update | Monthly | CEO, CFO, IMO Lead | 30 min | Executive summary, RAG status |

---

## 2. Day-0 Assessment: Financial Due Diligence Handover

### 2.1 Information Request List (IRL) — Finance

Before any integration work begins, collect from each subsidiary:

**Accounting & Close:**
- [ ] Current Chart of Accounts (export from ERP)
- [ ] Monthly/quarterly close checklist (if exists)
- [ ] Close calendar with deadlines
- [ ] Last 3 years of audited financial statements
- [ ] Trial balance (last 12 months, monthly granularity)
- [ ] Journal entry approval process documentation
- [ ] Accrual and provision policies

**Systems & Tools:**
- [ ] ERP system (name, version, modules in use)
- [ ] Accounting software (if different from ERP)
- [ ] Treasury management system
- [ ] Expense management tool
- [ ] Invoicing/billing system
- [ ] Payroll system and provider
- [ ] BI/reporting tools in use
- [ ] Integration architecture (APIs, manual exports, middleware)

**Tax & Compliance:**
- [ ] VAT registration and filing frequency
- [ ] Corporate tax jurisdiction and rates
- [ ] Transfer pricing documentation (if intercompany exists)
- [ ] Statutory audit requirements and auditor identity
- [ ] Electronic invoicing compliance (SDI in Italy, Chorus Pro in France, etc.)
- [ ] Regulatory filings calendar

**People & Organisation:**
- [ ] Finance team org chart with roles
- [ ] Key person dependencies (who knows what)
- [ ] Outsourced functions (payroll, tax, audit)
- [ ] Contractual obligations with external providers

### 2.2 Maturity Assessment Matrix

Rate each subsidiary (1-5) on:

| Dimension | 1 (Ad hoc) | 3 (Defined) | 5 (Optimised) |
|-----------|-----------|-------------|---------------|
| Close discipline | No formal close; year-end only | Monthly close with checklist | Automated close with T+5 reporting |
| CoA structure | Flat, no hierarchy | 3-level structure | Multi-dimensional (entity, cost centre, project) |
| Controls | None documented | Key controls identified | SOX-style testing cycle |
| Systems | Spreadsheets | Single ERP, partial modules | Integrated ERP + BI + Treasury |
| Reporting | Annual statutory only | Monthly management P&L | Real-time dashboards + forecasting |
| Intercompany | No IC transactions | IC exists but manual reconciliation | Automated IC matching & elimination |

**Action principle:** Focus integration effort on entities scoring 1-2. Entities at 4-5 can self-serve with light coordination.

---

## 3. Chart of Accounts (CoA) Harmonisation

### 3.1 Approach Options

| Option | Description | Timeline | Risk | Best When |
|--------|-------------|----------|------|-----------|
| **Full migration** | All entities adopt group CoA | 6-12 months | High (disruption, retraining) | Long-term, single ERP planned |
| **Mapping layer** | Local CoA retained; mapping table translates to group structure | 2-4 months | Medium (mapping errors) | Multiple ERPs staying, need fast consolidation |
| **Hybrid** | Top-level accounts harmonised; sub-accounts stay local | 3-6 months | Low-Medium | Subsidiaries have mature local CoA |

### 3.2 Group CoA Structure (Recommended)

```
Level 1: Class         (1-digit)   → Asset, Liability, Equity, Revenue, COGS, OpEx, Finance, Tax
Level 2: Category      (2-digit)   → e.g., 60 = Personnel Costs
Level 3: Sub-category  (3-digit)   → e.g., 601 = Salaries
Level 4: Account       (4-digit)   → e.g., 6011 = Salaries - Permanent Staff
Level 5: Entity suffix (4+2 digit) → e.g., 6011.IT01 = Salaries Perm - Italy Subsidiary 1
```

### 3.3 Mapping Methodology

**Step 1:** Export source CoA from each subsidiary (complete account list with balances)

**Step 2:** Map each local account to group Level 4 account:

| Local Code | Local Description | Balance (EUR) | Group Code | Group Description | Mapping Notes |
|-----------|-------------------|---------------|-----------|-------------------|---------------|
| 5101 | Stipendi dipendenti | 1,240,000 | 6011 | Salaries - Permanent | Direct 1:1 |
| 5102 | TFR accantonamento | 89,000 | 6041 | Post-employment benefits | Italian TFR specific |
| 5103 | Collaboratori | 156,000 | 6012 | Salaries - Contractors | Check if CoCoCo or P.IVA |
| — | (no local equivalent) | — | 6050 | Share-based payments | New for group reporting |

**Step 3:** Identify gaps:
- **Unmapped accounts** — local accounts with no group equivalent (create new group account or merge)
- **Split accounts** — one local account maps to multiple group accounts (need sub-ledger or rule)
- **Missing accounts** — group accounts with no local equivalent (create locally or confirm zero balance)

**Step 4:** Validate with trial balance reconciliation:
- Sum of mapped balances per group account = consolidated trial balance
- Delta must be zero (any difference = mapping error)

### 3.4 CoA Governance Post-Integration

- **New account requests** go through IMO Lead (single approver for consistency)
- **Annual review** of unused accounts (archive after 24 months of zero activity)
- **Documentation** — every mapping decision recorded in a CoA Mapping Register with rationale

---

## 4. Close Calendar Alignment

### 4.1 Target Close Calendar (Group Standard)

| Day | Activity | Responsible | Dependency |
|-----|----------|-------------|------------|
| T+0 | Period end (last day of month) | — | — |
| T+1 | Bank reconciliation completed | Subsidiary controller | Bank feeds imported |
| T+1 | AP cut-off: last invoices booked | Subsidiary controller | Invoice receipt deadline T-2 |
| T+2 | Revenue recognition entries posted | Subsidiary controller | Billing system closed |
| T+2 | Payroll journal posted | Payroll provider | Payroll run completed |
| T+3 | Accruals and provisions reviewed | Subsidiary controller | Department heads confirm |
| T+3 | Intercompany transactions matched | IC coordinator | All entities booked IC |
| T+4 | Subsidiary trial balance locked | Subsidiary controller | All entries posted |
| T+4 | Variance analysis (actual vs budget) | Subsidiary controller | Budget loaded in system |
| T+5 | Management P&L submitted to group | Subsidiary controller | Trial balance locked |
| T+7 | Consolidated P&L produced | Group controller | All subsidiaries submitted |
| T+8 | CFO review and commentary | Group CFO | Consolidation complete |
| T+10 | Board reporting pack distributed | IMO Lead / FP&A | CFO sign-off |

### 4.2 Transition Period Adjustments

During integration (first 6 months), allow:
- **T+7** subsidiary submission (vs target T+5) — allows time for new process adoption
- **Dual reporting** — local P&L in local CoA + mapped P&L in group CoA (reconciled monthly)
- **IMO validation step** — IMO Lead reviews first 3 mapped submissions before trusting automation

### 4.3 Hard Deadlines vs Soft Deadlines

| Deadline Type | Definition | Consequence of Miss |
|--------------|-----------|---------------------|
| **Hard** | Bank recon, tax filings, statutory close | Regulatory/audit risk — escalate immediately |
| **Soft** | Management reporting, variance commentary | Consolidated report delayed — flag in steering |
| **Advisory** | Budget upload, forecast refresh | Next cycle catch-up — no escalation |

---

## 5. ERP & Systems Integration Roadmap

### 5.1 Decision Framework

```
Are all subsidiaries on the same ERP?
    ├── YES → Configure group CoA + reporting in existing system
    └── NO →
        ├── Is a single-ERP migration planned within 12 months?
        │       ├── YES → Build interim consolidation layer (Excel/BI tool)
        │       └── NO → Build permanent middleware integration
        └── Can we afford a parallel run?
                ├── YES → Big-bang cutover with 2-month parallel
                └── NO → Phased migration (entity by entity)
```

### 5.2 Integration Architecture Options

**Option A: Single ERP (Target State)**
```
[Subsidiary 1] ─┐
[Subsidiary 2] ─┼── [Group ERP] ── [Consolidation Module] ── [BI/Reporting]
[Subsidiary 3] ─┘
```

**Option B: Multi-ERP with Middleware**
```
[Sub 1 - SAP] ──────┐
[Sub 2 - Sage] ─────┼── [Integration Layer / ETL] ── [Group Data Warehouse] ── [BI]
[Sub 3 - Custom] ───┘
                            ↓
                    [Consolidation Engine]
                            ↓
                    [Group Financial Statements]
```

**Option C: Mapping + Manual Consolidation (Quick Win)**
```
[Sub 1 - Export TB] ──┐
[Sub 2 - Export TB] ──┼── [Excel/Google Sheets Consolidation Model] ── [Group P&L]
[Sub 3 - Export TB] ──┘
```

### 5.3 Data Migration Checklist

- [ ] Master data: CoA, cost centres, profit centres, vendors, customers
- [ ] Open balances: AP, AR, bank, intercompany
- [ ] Historical data: decide how many years to migrate (minimum: current year + prior year comparative)
- [ ] Fixed assets register (NBV, depreciation schedules)
- [ ] Tax registers (VAT, withholding tax, deferred tax)
- [ ] Employee master data (if payroll integrated)
- [ ] Recurring journal entries and templates

---

## 6. Intercompany Framework

### 6.1 Policy Principles

1. All intercompany transactions must be **at arm's length** (transfer pricing compliance)
2. IC invoicing follows the **same close calendar** as external — no late IC bookings after T+3
3. **Bilateral confirmation** required before close: both parties agree on the IC balance
4. **Elimination entries** are automated at consolidation level (never manual)
5. IC disputes unresolved at T+3 are **escalated to IMO Lead** — never left open

### 6.2 Intercompany Transaction Types

| Type | Example | Pricing Basis | Documentation |
|------|---------|---------------|---------------|
| Management fees | HQ charges subsidiary for shared services | Cost + margin (5-10%) | Service agreement |
| Royalties / IP | Brand usage, software licenses | % of revenue or flat fee | License agreement |
| Goods transfer | Inventory moved between entities | Cost + markup or market price | Transfer pricing study |
| Loans | Parent lends to subsidiary | Market interest rate | Loan agreement |
| Recharges | Shared costs allocated (rent, IT, insurance) | Cost allocation key (FTE, revenue, sqm) | Allocation methodology memo |

### 6.3 Monthly IC Reconciliation Process

```
Day T+2:  Each entity exports IC balances (AP and AR per counterparty)
Day T+2:  Automated matching: compare Sub A's IC-AR to Sub B's IC-AP
Day T+3:  Mismatches flagged → bilateral resolution (tolerance: EUR 100)
Day T+3:  Confirmed IC balances locked
Day T+7:  Elimination entries auto-generated in consolidation
```

### 6.4 Transfer Pricing Documentation (EU Minimum)

For each IC transaction type, maintain:
- Master file (group-level TP policy)
- Local file (per-country specifics)
- Benchmarking study (every 3 years, refresh annually)
- Country-by-country reporting (CbCR) if group revenue > EUR 750M

---

## 7. Tax & Statutory Compliance Alignment

### 7.1 Multi-Jurisdiction Compliance Matrix

| Obligation | Italy | France | Frequency | System | Deadline |
|-----------|-------|--------|-----------|--------|----------|
| VAT return | Liquidazione IVA | CA3 | Monthly/Quarterly | ERP + SDI/Chorus Pro | IT: 16th / FR: 19th-24th |
| Corporate tax | IRES + IRAP | IS | Annual + advances | External advisor | IT: 30 Nov / FR: 15 May |
| Withholding tax | Ritenute d'acconto | Retenue à la source | Monthly | Payroll system | IT: 16th / FR: 15th |
| Electronic invoicing | SDI (mandatory) | Chorus Pro (B2G only) | Per-transaction | ERP + e-invoicing module | IT: 12 days / FR: immediate B2G |
| Financial statements | Bilancio + Nota Integrativa | Comptes Annuels + Annexe | Annual | ERP + external | IT: 120 days / FR: 6 months |
| Statutory audit | Revisore Legale | Commissaire aux Comptes | Annual | External auditor | Before filing |
| Intrastat | Intrastat IT | DEB/DES | Monthly (>EUR 400K) | Customs module | 25th of following month |
| Consolidation package | Group reporting | Group reporting | Monthly | Group format | T+5 |

### 7.2 Tax Integration Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Permanent establishment (PE) risk | Subsidiary activities could create tax PE in parent's country | Map cross-border activities, get TP advice |
| VAT group registration | Different VAT treatment of IC supplies | Assess VAT group option per country |
| Thin capitalisation | IC loans rejected as equity → denied interest deduction | Maintain debt/equity ratio per country rules |
| CFC rules | Low-tax subsidiary income attributed to parent | Ensure subsidiaries have genuine economic substance |
| Stamp duty on restructuring | Mergers/transfers may trigger stamp duty | Map transaction steps with tax advisor pre-execution |

---

## 8. Governance & Controls Framework

### 8.1 Authority Matrix (Delegation of Authority — DoA)

| Transaction Type | Subsidiary Controller | Subsidiary GM | Group CFO | Board |
|-----------------|:--------------------:|:-------------:|:---------:|:-----:|
| Operating expenses < EUR 10K | Approve | — | — | — |
| Operating expenses EUR 10-50K | Recommend | Approve | — | — |
| Operating expenses > EUR 50K | Recommend | Recommend | Approve | — |
| Capital expenditure < EUR 25K | Recommend | Approve | Inform | — |
| Capital expenditure EUR 25-100K | Recommend | Recommend | Approve | — |
| Capital expenditure > EUR 100K | Recommend | Recommend | Recommend | Approve |
| Headcount addition | Recommend | Approve (within budget) | Approve (above budget) | — |
| New vendor onboarding | Approve (< EUR 50K/yr) | Approve (< EUR 200K/yr) | Approve (> EUR 200K/yr) | — |
| IC pricing changes | Recommend | — | Approve | Inform |
| Write-offs < EUR 5K | Approve | — | Inform | — |
| Write-offs > EUR 5K | Recommend | Recommend | Approve | Inform (> EUR 50K) |

### 8.2 Key Controls Checklist

**Financial Close Controls:**
- [ ] Bank reconciliation completed and reviewed (segregation of duties: preparer ≠ reviewer)
- [ ] Revenue cut-off testing (last 3 days of period: correct period attribution)
- [ ] AP three-way match (PO → receipt → invoice) for purchases > EUR 1K
- [ ] Payroll reconciliation (gross-to-net, headcount check vs HR system)
- [ ] Fixed asset register reconciled to GL (additions, disposals, depreciation)
- [ ] Intercompany balances confirmed bilaterally
- [ ] Accruals reasonableness check (vs prior period, vs budget)
- [ ] Journal entry approval (all manual JEs reviewed by second person)

**Access Controls:**
- [ ] ERP access rights reviewed quarterly
- [ ] No single user can create vendor + approve payment (segregation)
- [ ] Bank payment authorisation requires dual signature > EUR 10K
- [ ] Chart of accounts changes restricted to IMO Lead / Group Controller

### 8.3 Audit Trail Requirements

Every financial transaction must have:
1. **Source document** (invoice, contract, receipt, board minute)
2. **Approval evidence** (digital signature, email trail, system workflow)
3. **Booking reference** (journal entry number, posting date, user ID)
4. **Period attribution** (clear mapping to reporting period)
5. **Entity attribution** (clear mapping to legal entity)

---

## 9. Communication & Change Management

### 9.1 Stakeholder Map

| Stakeholder | Concern | Communication Need | Frequency |
|------------|---------|-------------------|-----------|
| Group CFO | Timeline, cost, risk | Executive dashboard | Bi-weekly |
| Subsidiary controllers | Process change, workload | Detailed work plan, training | Weekly |
| External auditors | Compliance, audit trail | Methodology changes, CoA mapping | As needed |
| IT team | System changes, data migration | Technical specs, testing windows | Per sprint |
| Subsidiary GMs | Business impact, resource ask | High-level progress, resource needs | Monthly |
| Employees (finance team) | Job security, skills | Town hall, FAQs, training plan | Quarterly |

### 9.2 Resistance Management

| Signal | Root Cause | Response |
|--------|-----------|----------|
| Missed deadlines without explanation | Overload or passive resistance | 1:1 with subsidiary controller, understand blockers |
| "We've always done it this way" | Fear of change, comfort with status quo | Show benefit (less manual work, fewer errors), pilot win |
| Data quality issues in mapping | Rushed or careless execution | Add validation step, provide clearer instructions |
| Escalation avoidance | Cultural (don't want to "bother" group) | Normalise escalation, celebrate early flagging |
| Parallel systems maintained "just in case" | Lack of trust in new process | Set clear sunset date, demonstrate reconciliation accuracy |

---

## 10. Day-1 to Day-100 Timeline

### Phase 1: Assessment & Planning (Day 1-30)

| Week | Activity | Deliverable |
|------|----------|-------------|
| 1-2 | IRL collection from all subsidiaries | Completed IRL per entity |
| 1-2 | IMO setup: roles, cadence, tools | IMO charter document |
| 2-3 | Maturity assessment per subsidiary | Maturity scorecard |
| 3-4 | CoA analysis: current state mapping | Gap analysis document |
| 3-4 | Systems landscape documentation | Architecture diagram |
| 4 | Integration plan presentation to steering | Approved plan + budget |

### Phase 2: Design & Quick Wins (Day 31-60)

| Week | Activity | Deliverable |
|------|----------|-------------|
| 5-6 | Group CoA design (or mapping layer) | CoA specification + mapping tables |
| 5-6 | Close calendar definition | Unified close calendar |
| 6-7 | Intercompany policy drafting | IC policy document |
| 7-8 | Authority matrix (DoA) | Approved DoA per entity |
| 7-8 | Quick win: unified management P&L template | Excel/BI template deployed |
| 8 | First consolidated report (manual/semi-auto) | Month-1 group P&L |

### Phase 3: Implementation & Testing (Day 61-100)

| Week | Activity | Deliverable |
|------|----------|-------------|
| 9-10 | CoA mapping implemented in systems | Automated mapping live |
| 9-10 | Intercompany reconciliation process deployed | First IC matching cycle |
| 10-11 | Close calendar enforced (first full cycle) | T+5 submission by all entities |
| 11-12 | Controls testing (first pass) | Controls assessment report |
| 12-13 | ERP integration/middleware deployed (if applicable) | Automated data flows live |
| 13-14 | Parallel run validation | Reconciliation report (old vs new) |
| 14 | Go-live sign-off | Steering committee approval |

### Phase 4: Steady State & Optimisation (Day 100+)

- Monthly close operating smoothly at T+5
- Quarterly reviews of process efficiency
- Continuous improvement backlog (automation, exception reduction)
- Training new team members on group processes
- Annual CoA review and cleanup

---

## 11. Risk Register

| # | Risk | Probability | Impact | Mitigation | Owner |
|---|------|:-----------:|:------:|-----------|-------|
| 1 | Key person leaves during integration | Medium | High | Document all tribal knowledge in first 2 weeks; cross-train | IMO Lead |
| 2 | ERP data migration errors | High | High | Parallel run for 2 months; reconciliation at account level | Systems Stream |
| 3 | Subsidiary resistance to new processes | Medium | Medium | Change management plan; early wins; involve local controllers in design | IMO Lead |
| 4 | Transfer pricing challenge from tax authority | Low | High | Benchmark study before IC pricing implementation | Tax Stream |
| 5 | Auditor disagrees with CoA mapping choices | Low | Medium | Involve auditor in design phase; document rationale | CoA Stream |
| 6 | Business disruption during close calendar change | Medium | Medium | Gradual transition (T+7 → T+5 over 3 months) | IMO Lead |
| 7 | Integration budget overrun | Medium | Medium | Fixed-scope phases with go/no-go gates | IMO Lead |
| 8 | Regulatory change during integration (e.g., new e-invoicing rules) | Low | Medium | Monitor regulatory pipeline; build flexibility into timeline | Tax Stream |

---

## 12. Success Metrics

### Lagging Indicators (measure after 100 days)

| Metric | Baseline | Target | How to Measure |
|--------|----------|--------|----------------|
| Consolidated close time | N/A (not possible) | T+10 (day 10 of following month) | Calendar days from period end to board pack |
| Subsidiary reporting accuracy | Unknown | < 5 adjusting entries per entity per month | Count post-close adjustments |
| IC reconciliation breaks | Unknown | < EUR 1K total open items at T+5 | IC matching report |
| Audit adjustments | (prior year count) | -50% vs prior year | Auditor's management letter |
| Finance team overtime | (baseline hours) | -20% vs baseline | Time tracking / self-report |

### Leading Indicators (monitor weekly during integration)

| Metric | Target | Action if Off-Track |
|--------|--------|---------------------|
| IRL completion rate | 100% by Day 14 | Escalate to subsidiary GM |
| CoA mapping % complete | 100% by Day 45 | Add resources or simplify |
| Steering committee attendance | 100% | Reschedule or escalate |
| Action items closed on time | > 80% | Review workload distribution |
| Subsidiary NPS (satisfaction) | > 6/10 | 1:1 interviews, adjust approach |

---

## Appendix A: Glossary

| Term | Definition |
|------|-----------|
| **CoA** | Chart of Accounts — the structured list of all general ledger accounts |
| **DoA** | Delegation of Authority — the approval matrix defining who can approve what |
| **IC** | Intercompany — transactions between entities within the same group |
| **IMO** | Integration Management Office — the team managing the integration |
| **IRL** | Information Request List — the standardised data collection template |
| **PMI** | Post-Merger Integration — the process of combining two organisations after M&A |
| **RACI** | Responsible, Accountable, Consulted, Informed — responsibility assignment matrix |
| **SDI** | Sistema di Interscambio — Italy's mandatory electronic invoicing system |
| **T+N** | N business days after period end (e.g., T+5 = 5th business day of new month) |
| **TB** | Trial Balance — the list of all GL accounts with their debit/credit balances |
| **TP** | Transfer Pricing — the pricing of intercompany transactions for tax purposes |

---

## Appendix B: Template Downloads

- [CoA Mapping Template (CSV)](../templates/coa-mapping-template.csv)
- [Close Calendar Template](../templates/close-calendar.md)
- [Intercompany Reconciliation Template](../templates/ic-reconciliation.md)
- [Integration Status Report Template](../templates/integration-status-report.md)

---

*Built from real-world experience integrating multiple subsidiaries post-acquisition. For automated financial consolidation and reporting, see [SCALA AI OS](https://get-scala.com).*
