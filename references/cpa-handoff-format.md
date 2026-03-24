# CPA Handoff Format — Output Specification

This reference defines the structure of the CPA handoff package generated in Phase 5.

All files are written to `~/.tax-prep/{year}/package/`.

---

## Primary Output: Single Structured Document

The default CPA package is a single markdown file (`cpa-package.md`) containing all
11 sections below. This is the most practical format:
- Readable in any text editor or browser
- Copy-pasteable into email for CPA
- Renderable in Claude Projects / Cowork
- Contains all the same data as the CSV files

Structure the markdown file with:
- H1: "Tax Year {year} — CPA Package for {name}"
- H2: Each of the 11 sections below
- Tables for tabular data (markdown tables)
- Bullet lists for open questions and notes
- Bold for key amounts and flags
- A "Document Checklist" section with ✓/✗ status markers

The CSV files (detailed below) are a secondary output for users who prefer spreadsheets.
If openpyxl is available in Claude Code, an additional multi-tab Excel file is generated.

---

## CPA Cover Letter

Include a brief cover letter at the top of the CPA package summarizing: filing status, states filed, 2-3 notable items this year, count of open questions for CPA review, and document completeness (received/total). Pull notable items from session-notes.json entries of type "cpa_note" and "decision". Claude should write this naturally — no rigid template needed.

---

## Section 1: Summary (`01-summary.csv`)

| Column | Description |
|--------|------------|
| Category | Filing status, dependents, income category, deduction category |
| Detail | Specific item description |
| Amount | Dollar amount |
| Notes | Flags, open questions, CPA attention items |

**Rows:**
- Filing status and dependents
- Total income by category: wages, interest, dividends, capital gains, rental, business, K-1
- Total deductions by category: mortgage interest, property tax, state/local tax, charitable
- Estimated payments made (federal and state totals)
- Rough tax estimate (with prominent disclaimer — see `references/estimate-template.md`)
- Open questions for the CPA (summarized from Section 11)

---

## Section 2: Document Checklist (`02-document-checklist.csv`)

| Column | Description |
|--------|------------|
| Form Type | W-2, 1099-INT, 1099-DIV, 1098, K-1, etc. |
| Institution | Who issued the document |
| Account | Account identifier or description |
| Status | received, pending, pending_third_party, pending_cpa, pending_user, not_applicable, possible, not_expected |
| Key Amount | Primary dollar figure from the form |
| Notes | Expected date, delays, issues |

One row per expected document. Sort by: status (pending first), then form type.

---

## Section 3: W-2 and Employment Income (`03-w2-employment.csv`)

| Column | Description |
|--------|------------|
| Employer | Employer name |
| EIN | Employer identification number |
| Box 1 — Wages | Federal taxable wages |
| Box 2 — Federal Withholding | Federal income tax withheld |
| Box 3 — SS Wages | Social Security wages |
| Box 4 — SS Withholding | Social Security tax withheld |
| Box 5 — Medicare Wages | Medicare wages |
| Box 6 — Medicare Withholding | Medicare tax withheld |
| Box 12 Codes | Retirement contributions, HSA, etc. |
| Box 16 — State Wages | State wages (per state) |
| Box 17 — State Withholding | State income tax withheld |
| Box 18 — Local Wages | Local wages |
| Box 19 — Local Withholding | Local tax withheld |
| Notes | Mid-year change, stock comp, etc. |

One row per W-2. If multiple states on one W-2, add additional rows for each state.

---

## Section 4: Investment Income (`04-investment-income.csv`)

| Column | Description |
|--------|------------|
| Institution | Brokerage / bank name |
| Account Type | Brokerage, savings, retirement |
| Interest (1099-INT Box 1) | Interest income |
| Ordinary Dividends (1099-DIV 1a) | |
| Qualified Dividends (1099-DIV 1b) | |
| Capital Gain Distributions (1099-DIV 2a) | |
| Foreign Tax Paid (1099-DIV Box 7) | |
| Total Proceeds (1099-B) | |
| Total Cost Basis (1099-B) | |
| Net Short-Term Gain/Loss | |
| Net Long-Term Gain/Loss | |
| Wash Sale Adjustments | |
| Federal Tax Withheld | |
| Notes | Missing cost basis, corrected statement expected |

One row per account/institution.

**Additional sub-section:** Capital loss carryforward from prior year (if known).

---

## Section 5: Rental Properties (`05-rental-properties.csv`)

| Column | Description |
|--------|------------|
| Property Address | Full address |
| Date Acquired | Purchase date |
| Ownership % | Percentage owned (100% if sole owner) |
| Fair Rental Days | Days rented at fair market value |
| Personal Use Days | Days of personal use |
| **Income** | |
| Gross Rent | Total rent collected |
| **Expenses (Schedule E Lines)** | |
| Line 5 — Advertising | |
| Line 6 — Auto/Travel | |
| Line 7 — Cleaning/Maintenance | |
| Line 8 — Commissions | |
| Line 9 — Insurance | |
| Line 10 — Legal/Professional | |
| Line 11 — Management Fees | |
| Line 12 — Mortgage Interest | From 1098 |
| Line 13 — Other Interest | |
| Line 14 — Repairs | |
| Line 15 — Supplies | |
| Line 16 — Taxes | Property tax |
| Line 17 — Utilities | |
| Line 18 — Depreciation | See depreciation note |
| Line 19 — Other | HOA, pest control, etc. |
| **Totals** | |
| Total Expenses | |
| Net Income/Loss | Gross Rent - Total Expenses |
| **Depreciation Info** | |
| Depreciable Basis | |
| Accumulated Depreciation | |
| Notes | Sold, improvements, basis questions |

One row per property. For sold properties, add additional rows for sale information:
sale price, selling expenses, adjusted basis, gain/loss.

---

## Section 6: Business Income (`06-business-income.csv`)

| Column | Description |
|--------|------------|
| Business Name | |
| Business Type | Sole proprietor, LLC, etc. |
| EIN | If applicable |
| Gross Income | Total 1099-NEC + other business income |
| **Expenses** | |
| Advertising | |
| Car/Truck | |
| Contract Labor | |
| Insurance | |
| Office Expense | |
| Rent/Lease | |
| Supplies | |
| Utilities | |
| Home Office | |
| Other Expenses | |
| **Totals** | |
| Total Expenses | |
| Net Profit/Loss | |
| SE Tax Estimate | Net Profit × 15.3% × 92.35% |

Only include if the user has Schedule C income.

---

## Section 7: K-1 Summary (`07-k1-summary.csv`)

| Column | Description |
|--------|------------|
| Entity Name | Partnership / S-Corp / Trust name |
| EIN | Entity EIN |
| Entity Type | Partnership, S-Corp, Estate/Trust |
| K-1 Form | 1065, 1120-S, 1041 |
| Box 1 — Ordinary Income | |
| Box 2 — Rental Income | |
| Box 5 — Interest | |
| Box 6a — Ordinary Dividends | |
| Box 6b — Qualified Dividends | |
| Box 8 — Short-Term Capital Gain | |
| Box 9a — Long-Term Capital Gain | |
| Box 14 — SE Earnings | |
| Box 20Z — Section 199A QBI | |
| Distributions | |
| Notes | Passive/active, basis tracking |

One row per K-1. Include all material boxes even if zero.

---

## Section 8: Deductions and Credits (`08-deductions-credits.csv`)

| Column | Description |
|--------|------------|
| Category | Type of deduction or credit |
| Item | Specific description |
| Amount | Dollar amount |
| Form/Line | Where it goes on the return |
| Notes | Documentation, limitations |

**Rows should include:**
- Mortgage interest (primary residence) — Form 1098
- Property tax (primary residence)
- State income tax paid/withheld
- SALT deduction total (note if at cap)
- Charitable contributions — cash (with recipient and amounts)
- Charitable contributions — non-cash
- Child care expenses (provider name, amount, provider EIN)
- Student loan interest
- HSA contributions (employer + personal, vs limit)
- Estimated tax payments — federal (per quarter)
- Estimated tax payments — state (per quarter, per state)
- Education expenses (529 contributions, tuition)
- Medical expenses (if above 7.5% AGI threshold)

---

## Section 9: State-Specific (`09-state-specific.csv`)

| Column | Description |
|--------|------------|
| State | Two-letter state code |
| Item | State-specific item |
| Amount | Dollar amount |
| Notes | State form reference, special rules |

**Rows per state:**
- State wages / income allocation
- State withholding
- State estimated payments (per quarter)
- State-specific deductions (NJ property tax deduction, NY 529, etc.)
- State-specific credits
- Residency status (full-year, part-year, non-resident)

---

## Section 10: Year-over-Year Comparison (`10-year-over-year.csv`)

| Column | Description |
|--------|------------|
| Category | Income/deduction category |
| Item | Specific line item |
| Prior Year | Dollar amount from prior year |
| Current Year | Dollar amount for current year |
| Change | Dollar difference |
| Change % | Percentage change |
| Flag | ">20% change", "new item", "missing vs prior year" |

Only include if prior year data exists. Flag items with >20% change or items
that are new / disappeared for CPA attention.

---

## Section 11: Open Questions (`11-open-questions.csv`)

| Column | Description |
|--------|------------|
| # | Question number |
| Category | Which area (rental, investments, K-1, etc.) |
| Question | Specific question for the CPA |
| Context | Background information to help the CPA |
| Priority | High, Medium, Low |

**Common open questions:**
- Missing documents still expected
- Ambiguous expense categorizations
- Depreciation basis uncertainties
- Capital loss carryforward amounts needing confirmation
- Property sale basis calculations
- K-1 items needing interpretation
- Whether to itemize or take standard deduction
- State allocation questions for multi-state filers
