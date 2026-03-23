# Tax Document Matrix

Reference mapping of account types to expected tax documents, availability dates, and practical notes.

---

## Document Matrix by Account Type

| Account Type | Institution Examples | Expected Tax Forms | Typical Availability | Notes |
|---|---|---|---|---|
| **Employer (W-2)** | Any employer | W-2 | Jan 31 | Check Box 12 for RSU, ESPP, HSA, 401k contributions. Multiple W-2s if changed jobs mid-year. |
| **Bank / Savings Account** | Chase, Ally, Marcus, Capital One 360 | 1099-INT | Jan 31 | Not issued if interest earned is under $10. Still reportable income even without the form. |
| **Brokerage** | Fidelity, Schwab, Vanguard, E*TRADE, Robinhood | 1099-B, 1099-DIV, 1099-INT (consolidated) | Feb 15 | Corrected/amended statements common through mid-March. Consolidated 1099 may bundle all three. Wait for "final" version before filing. |
| **Mortgage Lender** | Rocket Mortgage, loanDepot, local credit unions | 1098 | Jan 31 | Shows mortgage interest paid and property tax paid from escrow. One per mortgage. Includes PMI in Box 5 if applicable. |
| **Rental Income Platform** | Apartments.com, Zillow Rental Manager, Avail, TurboTenant | 1099-K | Jan 31 | 2025 tax year: 1099-K issued if gross payments exceed $2,500 (IRS phased threshold). Rental income is reportable regardless of whether a 1099-K is issued. |
| **HSA Administrator** | Optum, HealthEquity, Fidelity HSA, Lively | 1099-SA, 5498-SA | Jan 31 (1099-SA), May 31 (5498-SA) | 1099-SA reports distributions. 5498-SA reports contributions (arrives after filing season). W-2 Box 12 Code W shows employer + employee contributions. |
| **K-1 Sources (Partnerships / S-Corps)** | Any partnership, S-corp, LLC taxed as partnership | Schedule K-1 (Form 1065 or 1120-S) | Mar 15 deadline, often extended to Sep 15 | Most common late-arriving document. Entity must file its return before issuing K-1. If entity files extension, K-1 may not arrive until Sep-Oct. May require filing a personal extension. |
| **Retirement Accounts** | Fidelity, Vanguard, TIAA, Schwab | 1099-R | Jan 31 | Covers distributions from 401k, IRA, pension, annuity. Box 7 distribution code determines taxability. Roth conversions also generate a 1099-R. |
| **Freelance / Contract Clients** | Any client paying $600+ for services | 1099-NEC | Jan 31 | One per client. Income is reportable even if no 1099-NEC is received (under $600 threshold or client non-compliance). |
| **Health Insurance Marketplace** | Healthcare.gov, state exchanges (Covered California, NY State of Health, etc.) | 1095-A | Jan 31 | Required to reconcile premium tax credit (Form 8962). Must file even if you might owe back credits. Check for corrected versions. |
| **Employer Benefits (ALE)** | Large employers (50+ full-time employees) | 1095-C | Mar 2 | Documents employer-sponsored health coverage offer. Needed if marketplace coverage was also used. Not required to file with return but retain for records. |
| **Stock Compensation (RSU / ESPP)** | Employer + broker (E*TRADE, Schwab, Morgan Stanley at Work, Fidelity) | W-2 (supplemental info) + 1099-B from broker | W-2: Jan 31, 1099-B: Feb 15 | RSU income included in W-2 Boxes 1, 12, 14. Broker 1099-B often shows $0 cost basis for RSUs — must adjust using W-2 income to avoid double taxation. ESPP discount may appear on W-2. |
| **Education (Tuition)** | Universities, colleges, trade schools | 1098-T | Jan 31 | Box 1: payments received. Box 5: scholarships/grants. Needed for American Opportunity Credit or Lifetime Learning Credit. |
| **Education (Student Loans)** | Navient, FedLoan, SoFi, Nelnet, Great Lakes | 1098-E | Jan 31 | Reports student loan interest paid. Deductible up to $2,500 (income phase-outs apply). Not issued if interest paid is under $600, but still deductible. |
| **Cryptocurrency Exchange** | Coinbase, Kraken, Gemini, Binance.US | 1099-B or 1099-MISC | Varies (Jan 31 - Feb 15) | Reporting standards still evolving. Some exchanges issue 1099-MISC for staking/rewards instead of 1099-B. Cost basis may be incomplete — cross-reference with personal transaction records. DeFi/self-custody transactions may not be reported by any institution. |
| **State/Local Tax Refund** | State tax authority (FTB, DTF, etc.) | 1099-G | Jan 31 | Only taxable if you itemized deductions in the prior year. If you took the standard deduction, the refund is not taxable income. |
| **Social Security** | Social Security Administration | SSA-1099 | Jan 31 | Up to 85% of benefits may be taxable depending on combined income. Available online at my.ssa.gov if paper form is lost. |
| **Unemployment** | State workforce/employment agency | 1099-G | Jan 31 | Fully taxable as ordinary income. Check if state tax was withheld (Box 11). |
| **Cancellation of Debt** | Banks, credit card companies, mortgage servicers | 1099-C | Jan 31 | Cancelled debt is generally taxable income. Exceptions: bankruptcy, insolvency, qualified principal residence indebtedness (check current law). |
| **Real Estate Sale** | Title company, closing attorney, real estate broker | 1099-S | Shortly after closing | Reports gross proceeds from sale. Not issued if seller certifies principal residence exclusion at closing (Form W-9S). Retain closing statement (HUD-1 or Closing Disclosure) for basis calculation. |

---

## Cross-Reference Rules

Use these rules to infer expected documents from a taxpayer's profile. Each rule follows the pattern: **if the profile includes X, then expect Y**.

### Income Sources

- **If profile has an employer** → expect one W-2 per employer. If job changed mid-year, expect multiple W-2s.
- **If profile has freelance/contract income** → expect one 1099-NEC per client paying $600+. Also expect to prepare Schedule C.
- **If profile has K-1 sources** → expect one K-1 per partnership, S-corp, or LLC. Flag as potential late arrival (Mar-Sep). Consider whether a personal extension (Form 4868) is needed.
- **If profile receives Social Security** → expect SSA-1099.
- **If profile received unemployment** → expect 1099-G from the state.

### Investment & Banking

- **If profile has bank or savings accounts** → expect 1099-INT per institution (if interest exceeds $10). High-yield savings accounts almost always generate one.
- **If profile has brokerage accounts** → expect consolidated 1099 (1099-B + 1099-DIV + 1099-INT) per brokerage. Wait until mid-March for final/corrected versions before filing.
- **If profile has cryptocurrency holdings with sales or rewards** → expect 1099-B or 1099-MISC per exchange, but verify completeness against personal records.
- **If profile has stock compensation (RSU/ESPP)** → expect both a W-2 (with compensation income) and a 1099-B from the administering broker. Cross-reference to ensure cost basis is correctly adjusted.

### Real Estate

- **If profile has a primary residence with a mortgage** → expect one 1098 from the mortgage servicer.
- **If profile has rental properties** → expect one 1098 per mortgaged rental property + property tax records from the county. If rent is collected through a platform, may also receive 1099-K.
- **If profile sold real estate during the year** → expect 1099-S from the title company (unless exclusion was certified at closing). Retain the closing disclosure for gain/loss calculation.
- **If profile has multiple rental properties** → expect Schedule E with one section per property. Collect rent rolls, expense receipts, and depreciation schedules per property.

### Health & Benefits

- **If profile has an HSA** → expect 1099-SA (distributions) and 5498-SA (contributions, arrives late). Cross-reference W-2 Box 12 Code W for employer contributions.
- **If profile purchased health insurance through the marketplace** → expect 1095-A. Required for filing — do not file without it.
- **If profile works for a large employer (ALE)** → may receive 1095-C. Retain for records.

### Education

- **If profile (or dependent) attended college/university** → expect 1098-T. Needed for education credits.
- **If profile is repaying student loans** → expect 1098-E if interest paid exceeds $600. Interest may still be deductible below that threshold.

### Debt & Government

- **If profile had debt cancelled or forgiven** → expect 1099-C. Evaluate insolvency or bankruptcy exclusion.
- **If profile received a state/local tax refund** → expect 1099-G. Only relevant if the taxpayer itemized in the prior year.

---

## Timing Summary

| Window | Documents Expected |
|---|---|
| **By Jan 31** | W-2, 1099-INT, 1099-NEC, 1099-R, 1099-G, SSA-1099, 1095-A, 1098, 1098-T, 1098-E, 1099-SA, 1099-K, 1099-C |
| **By Feb 15** | 1099-B / consolidated 1099 (brokerage), crypto exchange forms |
| **By Mar 2** | 1095-C |
| **By Mar 15** | K-1 (if entity files on time) |
| **By May 31** | 5498-SA (HSA contributions — informational, not needed to file) |
| **Sep 15 (extended)** | K-1 from entities that filed extensions |
| **After closing** | 1099-S (real estate sale) |

---

## Filing Readiness Checklist

A return is **ready to file** when:

1. All expected W-2s and 1099s have been received (cross-reference against prior year).
2. Brokerage statements are marked "final" or "corrected" (not "preliminary").
3. All K-1s have been received — or a decision to extend has been made.
4. 1095-A is in hand (if marketplace insurance was used).
5. RSU/ESPP cost basis has been cross-referenced between W-2 and 1099-B.
