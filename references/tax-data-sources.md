# Tax Data Sources — Current Year Numbers and Verification URLs

This file contains baseline tax numbers for the current tax year AND the URLs
to verify them via WebSearch.

**Maintenance:** Update this file annually when the IRS publishes inflation adjustments
(typically in Revenue Procedure released each November for the following tax year).

**Usage:**
- In Claude Code: read these numbers as baseline, then WebSearch to verify they're current
- In Cowork: use these numbers directly (no WebSearch available)

---

## Tax Year 2025 — Federal

### Standard Deduction

| Filing Status | Amount |
|--------------|--------|
| Single | $15,000 |
| Married Filing Jointly (MFJ) | $30,000 |
| Married Filing Separately (MFS) | $15,000 |
| Head of Household (HoH) | $22,500 |
| Additional (age 65+ or blind) — Single/HoH | +$1,950 |
| Additional (age 65+ or blind) — MFJ/MFS | +$1,550 |

**Verify:** Search "IRS 2025 standard deduction amounts" or check IRS Rev. Proc. 2024-40.

### Tax Brackets (Ordinary Income)

**Single:**
| Rate | Income Range |
|------|-------------|
| 10% | $0 – $11,925 |
| 12% | $11,926 – $48,475 |
| 22% | $48,476 – $103,350 |
| 24% | $103,351 – $197,300 |
| 32% | $197,301 – $250,525 |
| 35% | $250,526 – $626,350 |
| 37% | Over $626,350 |

**Married Filing Jointly:**
| Rate | Income Range |
|------|-------------|
| 10% | $0 – $23,850 |
| 12% | $23,851 – $96,950 |
| 22% | $96,951 – $206,700 |
| 24% | $206,701 – $394,600 |
| 32% | $394,601 – $501,050 |
| 35% | $501,051 – $751,600 |
| 37% | Over $751,600 |

**Verify:** Search "IRS 2025 tax brackets" or check IRS Rev. Proc. 2024-40.

### Capital Gains Rates

| Rate | Single | MFJ |
|------|--------|-----|
| 0% | $0 – $48,350 | $0 – $96,700 |
| 15% | $48,351 – $533,400 | $96,701 – $600,050 |
| 20% | Over $533,400 | Over $600,050 |

**Net Investment Income Tax (NIIT):** Additional 3.8% on investment income when MAGI exceeds $200,000 (single) or $250,000 (MFJ). These thresholds are NOT inflation-adjusted.

**Verify:** Search "IRS 2025 capital gains tax rates thresholds."

### Retirement Contribution Limits

| Account | 2025 Limit | Catch-Up (50+) |
|---------|-----------|----------------|
| 401(k) / 403(b) / 457 employee | $23,500 | +$7,500 |
| Traditional/Roth IRA | $7,000 | +$1,000 |
| SEP-IRA (employer) | $70,000 or 25% of comp | — |
| SIMPLE IRA | $16,500 | +$3,500 |
| Solo 401(k) employee | $23,500 | +$7,500 |

**Roth IRA income limits (2025):**
- Single: phase out $150,000 – $165,000
- MFJ: phase out $236,000 – $246,000

**Verify:** Search "IRS 2025 401k contribution limit" and "IRS 2025 IRA contribution limit."

### HSA Contribution Limits

| Coverage | 2025 Limit | Catch-Up (55+) |
|----------|-----------|----------------|
| Self-only | $4,300 | +$1,000 |
| Family | $8,550 | +$1,000 |

**Verify:** Search "IRS 2025 HSA contribution limits."

### SALT Deduction Cap

**$10,000** ($5,000 if Married Filing Separately).
Covers state and local income tax (or sales tax) + property tax combined.

**Note:** This cap was set by the Tax Cuts and Jobs Act (2017) and currently applies through 2025. Legislation may change this — verify at filing time.

### Estimated Tax Payment Due Dates (for Tax Year 2025)

| Quarter | Period | Due Date |
|---------|--------|----------|
| Q1 | Jan 1 – Mar 31 | April 15, 2025 |
| Q2 | Apr 1 – May 31 | June 16, 2025 |
| Q3 | Jun 1 – Aug 31 | September 15, 2025 |
| Q4 | Sep 1 – Dec 31 | January 15, 2026 |

**Safe harbor rules:**
- Pay ≥ 90% of current year tax, OR
- Pay ≥ 110% of prior year tax (100% if AGI ≤ $150,000 MFJ)
- Underpayment penalty rate: ~8% annualized (check IRS for current rate)

**Verify:** Search "IRS 2025 estimated tax payment due dates."

### Other Key Numbers

| Item | 2025 Amount |
|------|------------|
| Social Security wage base | $176,100 |
| Medicare additional tax threshold | $200,000 (single) / $250,000 (MFJ) |
| Gift tax exclusion | $19,000 per recipient |
| Child Tax Credit | $2,000 per qualifying child |
| Child & Dependent Care Credit max expenses | $3,000 (one) / $6,000 (two+) |
| Student loan interest deduction max | $2,500 |
| Student loan deduction phase-out | $80K–$95K (S) / $165K–$195K (MFJ) |
| AMT exemption | $88,100 (S) / $137,000 (MFJ) |

---

## Verification URLs

When using WebSearch in Claude Code, search these sources:

**Federal:**
- IRS Revenue Procedures: search "site:irs.gov revenue procedure {year} inflation"
- IRS Publication 17 (current year): search "IRS publication 17 {tax_year}"
- IRS Publication 501 (dependents, standard deduction): search "IRS publication 501"
- IRS Topic 409 (capital gains): search "IRS topic 409 capital gains rates"

**State — New Jersey:**
- NJ Division of Taxation: search "NJ income tax rates {tax_year}"
- NJ property tax deduction: search "NJ property tax deduction limit {tax_year}"
- NJ estimated payments: search "NJ estimated tax payment dates {tax_year}"
- URL: https://www.state.nj.us/treasury/taxation/

**State — New York:**
- NY Department of Taxation and Finance: search "NY income tax rates {tax_year}"
- NY estimated payments: search "NY estimated tax payment dates {tax_year}"
- NYC resident tax: search "NYC income tax rates {tax_year}"
- URL: https://www.tax.ny.gov/

---

## Caching

After verifying numbers via WebSearch, cache results to:
- `~/.tax-prep/{year}/federal-rates.json` — all federal numbers above
- `~/.tax-prep/{year}/state-rates/{state}.json` — per-state numbers

Follow the schemas in `references/schemas.md` for the JSON structure.
Cache is valid for the entire tax season (numbers don't change within a tax year).
