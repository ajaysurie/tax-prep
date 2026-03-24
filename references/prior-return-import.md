# Prior Return Import Guide

Maps Form 1040 lines and common schedules to the tax-prep skill's JSON state files.
Use this when a user uploads a prior year's tax return to bootstrap their profile.

---

## How to Use This Guide

1. User uploads their prior year 1040 PDF (and any attached schedules)
2. Read the PDF using the Read tool
3. Extract values using the line mappings below
4. Pre-populate `profile.json` and partially populate `accounts.json`
5. Present extracted data to user for confirmation before saving
6. Ask follow-up questions for anything the 1040 doesn't tell you (institution names, account details)

**Important:** A 1040 shows totals, not sources. It says "$4,200 in dividends" but not
"Fidelity brokerage." After extracting, ask the user to identify which accounts generated
each income line.

---

## CPA-Prepared Return PDF Structure

CPA returns are typically 50-200 page PDFs. Not everything is a tax form. Common structure (varies by CPA firm):

| Section | What It Is | Extract? |
|---------|-----------|----------|
| Cover letter / transmittal | CPA's letter to client | NO — skip |
| Filing instructions | Where/how to file, payment vouchers | NO — but note if extension was filed |
| Engagement letter | CPA service agreement | NO — skip |
| Form 1040 (pages 1-2) | The actual tax return | YES — primary extraction target |
| Schedules (1, 2, 3, A, B, C, D, E, SE) | Supporting schedules | YES — extract per mappings below |
| Form 8959, 8960 | Additional Medicare / Net Investment Income | YES — note if present |
| Form 8962 | Premium Tax Credit | YES — if marketplace insurance |
| State returns | State-specific forms | YES — extract income, withholding, estimated payments |
| K-1 worksheets | CPA's K-1 analysis | MAYBE — useful for basis tracking |
| Depreciation schedules | Per-asset depreciation detail | YES — valuable for rental properties |
| CPA workpapers / summaries | Internal CPA calculations | NO — but may have useful YoY comparison |
| Prior year comparison | Side-by-side YoY numbers | USEFUL — for sanity checking extraction |
| Payment vouchers | Estimated payment stubs | NOTE — shows next year's estimated amounts |

**Finding forms in the PDF:**
- Search for "Form 1040" — usually appears after 2-5 pages of cover material
- Each IRS form has its form number in the header/footer
- State returns usually follow federal, separated by a state cover page
- Depreciation schedules are often near the end, labeled "Depreciation and Amortization"

---

## Form 1040 — Page 1 (Filing Status and Income)

### Filing Status (top of page 1, checkboxes)
| Checkbox | Value for profile.json |
|----------|----------------------|
| Single | `"filing_status": "single"` |
| Married filing jointly | `"filing_status": "mfj"` |
| Married filing separately | `"filing_status": "mfs"` |
| Head of household | `"filing_status": "hoh"` |
| Qualifying surviving spouse | `"filing_status": "qss"` |

### Dependents (page 1, dependents section)
Extract each dependent: name, SSN (last 4 only), relationship, and whether they qualify
for child tax credit or credit for other dependents.

Map to `profile.json`:
```json
"dependents": [
  {
    "name": "...",
    "relationship": "...",
    "date_of_birth": "ask user",
    "qualifies_for_ctc": true
  }
]
```

### Income Lines (page 1)
| Line | Description | What it tells you |
|------|-------------|-------------------|
| 1a | Wages, salaries, tips | Has W-2 income. Ask: how many employers? |
| 2a | Tax-exempt interest | Has municipal bond holdings |
| 2b | Taxable interest | Has bank/brokerage accounts generating interest |
| 3a | Qualified dividends | Has investment accounts with dividend-paying holdings |
| 3b | Ordinary dividends | Same — 3a is a subset of 3b |
| 4a | IRA distributions | Has retirement accounts, took distributions |
| 4b | Taxable IRA amount | Portion that's taxable |
| 5a | Pensions and annuities | Has pension/annuity income |
| 5b | Taxable pension amount | Portion that's taxable |
| 6a | Social Security benefits | Receives Social Security |
| 6b | Taxable Social Security | Portion that's taxable |
| 7 | Capital gain or loss | Has investment sales. Check Schedule D |
| 8 | Other income (Schedule 1) | Has additional income — check Schedule 1 for details |

### Key Totals (page 1-2)
| Line | Description | Maps to |
|------|-------------|---------|
| 9 | Total income | Informational — sum of above |
| 10 | Adjustments (Schedule 1) | Check Schedule 1 for IRA deduction, student loan interest, HSA, etc. |
| 11 | Adjusted Gross Income (AGI) | Key number for phase-outs and safe harbor |
| 12 | Standard or itemized deduction | Tells you deduction method |
| 13 | Qualified business income deduction | Has QBI from pass-through entities |
| 15 | Taxable income | Informational |

---

## Form 1040 — Page 2 (Tax and Payments)

| Line | Description | What it tells you |
|------|-------------|-------------------|
| 16 | Tax | Total tax computed |
| 19 | Child tax credit (Schedule 8812) | Has qualifying children |
| 24 | Total tax | After credits |
| 25a | W-2 withholding | Federal tax withheld from wages |
| 25b | 1099 withholding | Federal tax withheld from other income |
| 26 | Estimated tax payments | Made estimated payments — get quarterly breakdown |
| 33 | Total payments | Sum of withholding + estimated + credits |
| 34 | Overpayment | Got a refund |
| 37 | Amount owed | Owed additional tax |

---

## Schedule 1 — Additional Income and Adjustments

### Part I — Additional Income
| Line | Description | What it tells you |
|------|-------------|-------------------|
| 3 | Business income or loss | Has Schedule C — self-employment |
| 5 | Rental real estate, royalties | Has Schedule E — rental properties |
| 7 | Unemployment compensation | Received unemployment |
| 8a | Net operating loss deduction | Had prior year losses |
| 8p | Scholarship/fellowship income | Education-related |
| 8z | Other income | Jury duty, gambling, etc. |

### Part II — Adjustments to Income
| Line | Description | What it tells you |
|------|-------------|-------------------|
| 11 | Educator expenses | Is a teacher |
| 13 | HSA deduction | Has HSA — ask for contribution amounts |
| 15 | SEP/SIMPLE/qualified plans | Has self-employed retirement |
| 16 | Self-employment tax deduction | Has Schedule SE |
| 17 | Self-employed health insurance | Self-employed with health insurance |
| 20 | Student loan interest | Has student loans — up to $2,500 |
| 21 | IRA deduction | Made deductible IRA contributions |

---

## Schedule A — Itemized Deductions

If the return used itemized deductions (1040 line 12 shows amount different from
standard deduction), check Schedule A:

| Line | Description | What it tells you |
|------|-------------|-------------------|
| 5a | State/local income tax | State tax paid (part of SALT) |
| 5b | State/local sales tax | Elected sales tax instead of income tax |
| 5c | Real estate taxes | Property tax paid (part of SALT) |
| 5d | Personal property tax | Vehicle/property tax (part of SALT) |
| 5e | Total SALT | Combined — subject to cap |
| 8a | Home mortgage interest (1098) | Has mortgage — ask which property |
| 10 | Investment interest | Has margin interest or investment debt |
| 12 | Charitable cash contributions | Made charitable donations |
| 13 | Charitable non-cash | Donated goods/property |
| 14 | Casualty/theft losses | Had disaster losses |

---

## Schedule B — Interest and Dividends

This is the most useful schedule for account discovery — it lists each payer by name.

| Section | What it tells you |
|---------|-------------------|
| Part I — Interest | Each institution that paid interest and the amount |
| Part II — Dividends | Each institution that paid dividends and the amount |
| Part III — Foreign accounts | Whether they have foreign accounts (FBAR) |

**Map each payer to `accounts.json`:** Each line in Schedule B is an account that should
appear in the accounts list with expected documents for the current year.

---

## Schedule C — Business Income

| Line | Description | Maps to |
|------|-------------|---------|
| A | Principal business | Business type |
| B | Business code | Industry code |
| C | Business name | Business name |
| 1 | Gross receipts | Business revenue |
| 4 | Cost of goods sold | If applicable |
| 7 | Gross income | Revenue minus COGS |
| 8-27 | Expenses by category | Business expenses |
| 30 | Business use of home | Has home office |
| 31 | Net profit or loss | Bottom line |

**For profile.json:** `"self_employment": true`, capture business name and type.
**For accounts.json:** Expect 1099-NEC from clients, possibly 1099-K.

---

## Schedule D — Capital Gains and Losses

| Line | Description | What it tells you |
|------|-------------|-------------------|
| 1a | Short-term from 8949 | Has stock/asset sales, held < 1 year |
| 1b | Short-term from brokerage (no 8949) | Brokerage reported directly |
| 7 | Net short-term | Short-term total |
| 8a | Long-term from 8949 | Sales held > 1 year |
| 8b | Long-term from brokerage | Brokerage reported directly |
| 14 | Net capital loss carryover | Carried forward losses from prior years |
| 15 | Net long-term | Long-term total |
| 21 | Net capital gain or loss | Combined — flows to 1040 line 7 |

**For profile.json:** `"has_investments": true`, note if capital loss carryover exists.
**For accounts.json:** Need to identify which brokerages. Ask the user.

---

## Schedule E — Rental Property

Each property gets its own column (A, B, C). Extract per property:

| Line | Description | Maps to |
|------|-------------|---------|
| 1a-c | Property address | Property identification |
| 2 | Property type | Rental type code |
| 3 | Rents received | Gross rental income |
| 5 | Advertising | Expense |
| 6 | Auto and travel | Expense |
| 7 | Cleaning and maintenance | Expense |
| 8 | Commissions | Expense |
| 9 | Insurance | Expense |
| 10 | Legal and professional | Expense |
| 11 | Management fees | Expense |
| 12 | Mortgage interest | Expense — should match 1098 |
| 13 | Other interest | Expense |
| 14 | Repairs | Expense |
| 15 | Supplies | Expense |
| 16 | Taxes | Property tax |
| 17 | Utilities | Expense |
| 18 | Depreciation | Annual depreciation amount |
| 19 | Other | Expense |
| 20 | Total expenses | Sum |
| 21 | Net income/loss | Per property |

### Part II — K-1 Income
Lines 28-34 show income from partnerships and S-corps. Each entity is listed with
its EIN and income/loss amount.

**For profile.json:** `"rental_properties": [...]` with addresses and property types.
**For accounts.json:** Each property needs mortgage lender, insurance provider, property
management company if applicable.

---

## Schedule SE — Self-Employment Tax

| Line | Description | What it tells you |
|------|-------------|-------------------|
| 3 | Net earnings | Self-employment income subject to SE tax |
| 12 | SE tax | Total self-employment tax |

Confirms self-employment. The deductible half flows to Schedule 1 line 15.

---

## State Returns

State returns vary by state, but generally extract:
- State wages and income
- State tax withheld
- State estimated payments made (quarterly amounts)
- State-specific credits claimed
- Property tax amounts (especially NJ, where it's a separate deduction)

Map state filing to `profile.json`: `"states": ["NJ", "NY"]`

---

## What the 1040 Does NOT Tell You

After extracting, you still need to ask the user:

1. **Institution names for investment accounts** — Schedule D shows gains/losses but not
   which brokerage (unless Schedule B or 8949 lists them)
2. **Account numbers** — never on the 1040
3. **Current year changes** — new accounts, closed accounts, new dependents, moved states
4. **Employer details** — the 1040 shows total wages, not per-employer breakdown
   (unless multiple W-2s attached)
5. **Estimated payment quarterly breakdown** — line 26 shows the total, not per-quarter
6. **HSA contribution details** — employer vs personal, which provider
7. **Charitable contribution details** — organizations, non-cash item descriptions
8. **Rental property acquisition details** — purchase date, original cost, land value
   (needed for depreciation but not on Schedule E)

---

## Import Workflow

1. **Read the PDF** — extract all pages
2. **Identify the form** — look for "Form 1040" header and tax year
3. **Extract page 1-2** (1040 main) using the line mappings above
4. **Check for schedules** — look for Schedule 1, A, B, C, D, E, SE headers
5. **Extract each schedule** found
6. **Build profile.json** from extracted data
7. **Build partial accounts.json** — institutions from Schedule B, properties from Schedule E, business from Schedule C
8. **Present everything to user for confirmation**
9. **Ask follow-up questions** for the gaps listed above
10. **Save state** and report: "I imported your {year} return. Here's what I found: {summary}. To complete your profile for this year, I need to know: {gaps}."
