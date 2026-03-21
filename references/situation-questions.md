# Situation Interview Question Bank (Phase 1)

The skill asks these questions one at a time, conversationally, adapting based on prior answers. Each entry includes the question text, why it matters for tax purposes, and what downstream phases or documents it unlocks.

---

## 1. Filing Status

### Q: Are you filing as single, married filing jointly, married filing separately, or head of household?

**Why it matters:** Filing status determines tax brackets, standard deduction amounts, and eligibility for many credits. Married filing jointly typically provides the lowest combined tax, but married filing separately is important when one spouse has significant liability exposure, student loan repayment concerns, or when spouses want to keep tax obligations separate.

**What it unlocks:** Every downstream calculation depends on this. Sets the standard deduction baseline, bracket thresholds, and credit phase-out ranges.

### Q: If married — did you get married this year, or were you married all year?

**Why it matters:** A mid-year marriage means the couple was single for part of the year. Filing status is determined by status on December 31, but the timing affects withholding accuracy and whether a prior-year joint return needs amending.

**What it unlocks:** Flags potential underwithholding if W-4s weren't updated promptly after marriage.

### Q: If head of household — do you have a qualifying dependent who lived with you for more than half the year?

**Why it matters:** Head of household provides a larger standard deduction and more favorable brackets than single, but has strict qualification rules. The IRS audits this status more frequently than others.

**What it unlocks:** Validates HoH eligibility before building the return on that basis.

#### Returning User

- "Last year you filed married filing jointly. Still the same this year?"
- "Any change in filing status — marriage, divorce, separation?"

---

## 2. Dependents

### Q: Do you have any dependents? Let's go through them — I'll need each person's name, date of birth, and relationship to you.

**Why it matters:** Dependents unlock the child tax credit ($2,000 per qualifying child under 17), child and dependent care credit, earned income credit, and education credits. Age cutoffs matter — a child who turned 17 during the tax year no longer qualifies for the full child tax credit.

**What it unlocks:** Child Tax Credit, Child and Dependent Care Credit (Form 2441), Earned Income Credit, education credits (Form 8863), dependency exemptions for state returns.

### Q: Did any of your dependents have income this year — like a part-time job or investment income?

**Why it matters:** A dependent with income above a threshold may need to file their own return. Unearned income over $2,500 for a child under 19 (or under 24 if a student) triggers the kiddie tax, which taxes that income at the parent's rate.

**What it unlocks:** Kiddie tax calculation (Form 8615), whether a separate return is needed for the dependent.

### Q: Did you pay for childcare or daycare so you could work?

**Why it matters:** The Child and Dependent Care Credit covers up to $3,000 in expenses for one dependent or $6,000 for two or more, for children under 13. The credit percentage phases down at higher incomes.

**What it unlocks:** Form 2441, dependent care FSA reconciliation.

### Q: Does anyone else (an ex-spouse, for example) also claim any of these dependents?

**Why it matters:** Only one taxpayer can claim a dependent. Duplicate claims trigger IRS rejection of the e-filed return. Divorced or separated parents need to determine who has the right to claim based on custody agreements or Form 8332.

**What it unlocks:** Form 8332 (Release of Claim to Exemption), determines which parent claims which credits.

#### Returning User

- "Last year you claimed two dependents — [names]. Same this year, or any changes? New baby, a child who aged out, or custody changes?"
- "Your oldest was 16 last year — they turned 17 this year, which means the child tax credit changes for them."

---

## 3. Employment

### Q: How many W-2 jobs did you have this year? Walk me through each one — employer name and roughly how long you worked there.

**Why it matters:** Each W-2 is a required document. Multiple W-2s from different employers in the same year can result in overwithholding of Social Security tax (the employer stops withholding at the wage base, but each employer calculates independently). Overwithholding is recoverable on the return.

**What it unlocks:** W-2 document collection, Social Security overwithholding credit, state return filing requirements if employers were in different states.

### Q: Did you change jobs during the year?

**Why it matters:** Mid-year job changes often cause underwithholding because each employer assumes it's the only one and sets withholding for a full year at that salary. The result can be an unexpected tax bill.

**What it unlocks:** Flags potential balance due, helps set expectations early.

### Q: Did you receive any bonuses, stock compensation, or equity payouts through your employer?

**Why it matters:** Supplemental wages like bonuses are often withheld at a flat 22% federal rate, which may be too low or too high depending on total income. Stock compensation (RSUs, ISOs, ESPP) has complex tax treatment that varies by type.

**What it unlocks:** Cross-references with the Investments section for stock compensation details, verifies W-2 box 12 codes.

### Q: Did you work remotely from a different state than your employer's location?

**Why it matters:** Many states require income tax filing based on where the work is physically performed, not where the employer is located. This can create multi-state filing obligations and potential double taxation (mitigated by credits in most cases).

**What it unlocks:** Multi-state filing requirements, state tax credit calculations.

#### Returning User

- "Last year you had a W-2 from [employer]. Same job this year, or any changes?"
- "Still working remotely, or did your work location change?"

---

## 4. Self-Employment

### Q: Did you do any freelance, contract, or self-employment work this year? This includes side gigs, consulting, or selling goods/services — even if you didn't receive a 1099.

**Why it matters:** Self-employment income is reported on Schedule C and is subject to both income tax and self-employment tax (15.3% for Social Security and Medicare). All net income over $400 triggers SE tax, regardless of whether a 1099 was issued.

**What it unlocks:** Schedule C, Schedule SE, quarterly estimated tax payment reconciliation, QBI deduction (Section 199A).

### Q: What's the nature of the business? And roughly what was the total revenue for the year?

**Why it matters:** The business type determines the applicable business code (NAICS), which the IRS uses for audit selection comparisons. Revenue level affects QBI deduction phase-outs for specified service trades.

**What it unlocks:** Schedule C business code, QBI deduction eligibility.

### Q: Did you have significant business expenses — things like equipment, software, home office, vehicle use, or subcontractors you paid?

**Why it matters:** Business expenses reduce net self-employment income, lowering both income tax and SE tax. The home office deduction alone can be substantial. Payments to subcontractors over $600 require issuing 1099s.

**What it unlocks:** Schedule C expense categories, home office deduction (Form 8829), vehicle expense method selection (standard mileage vs actual), 1099 filing obligations.

### Q: Did you make any estimated quarterly tax payments this year — federal or state?

**Why it matters:** Self-employed individuals are required to pay estimated taxes quarterly. If they didn't and owe more than $1,000, the IRS assesses an underpayment penalty. Tracking payments also prevents double-counting.

**What it unlocks:** Form 1040-ES reconciliation, underpayment penalty calculation (Form 2210), cross-references with the Estimated Payments section.

### Q: Is this business an LLC, sole proprietorship, or something else?

**Why it matters:** Entity type determines filing requirements. A single-member LLC is a disregarded entity (Schedule C). A multi-member LLC files as a partnership (Form 1065). An LLC that elected S-corp treatment files Form 1120-S. Getting this wrong changes the entire return structure.

**What it unlocks:** Correct form selection, K-1 generation if partnership/S-corp.

#### Returning User

- "Last year you reported self-employment income from [business]. Still doing that work this year?"
- "You made quarterly estimated payments last year. Did you continue those this year, and were the amounts similar?"
- "Any new side gigs or freelance work beyond what you did last year?"

---

## 5. Rental Properties

### Q: Do you own any rental properties? Let's go through each one — address and roughly when you acquired it.

**Why it matters:** Each rental property is reported separately on Schedule E. The acquisition date establishes the depreciation start date and method (27.5 years for residential). Depreciation is a significant non-cash deduction that reduces taxable rental income.

**What it unlocks:** Schedule E, depreciation schedules (Form 4562), passive activity loss rules.

### Q: Did you sell any rental property this year?

**Why it matters:** Selling a rental property triggers capital gains and depreciation recapture (taxed at up to 25%). Even if the property sold at a loss, prior depreciation must be recaptured. This is often the largest single tax event in a taxpayer's year.

**What it unlocks:** Form 4797, Schedule D, depreciation recapture calculation, installment sale reporting (Form 6252) if applicable.

### Q: Did you or your family use any of the rental properties personally this year? Even for a few days?

**Why it matters:** If personal use exceeds 14 days or 10% of rental days (whichever is greater), the property is treated as a personal residence, limiting deductible expenses. Below that threshold, it's treated as a pure rental with full expense deductibility.

**What it unlocks:** Personal use vs rental use allocation, vacation home rules (Section 280A).

### Q: What were the major expenses this year — mortgage interest, property taxes, repairs, improvements, property management fees?

**Why it matters:** Repairs are immediately deductible; improvements must be capitalized and depreciated. The distinction is one of the most common audit triggers for rental property owners. Property management fees, insurance, and HOA dues are all deductible.

**What it unlocks:** Schedule E expense categorization, improvement vs repair classification, new depreciation schedules for improvements.

### Q: Do you actively manage the properties yourself, or do you use a property manager?

**Why it matters:** Active participation allows up to $25,000 in rental losses to offset ordinary income (phasing out between $100K-$150K AGI). Without active participation, losses are passive and can only offset passive income.

**What it unlocks:** Passive activity loss limitation (Form 8582), active participation determination.

#### Returning User

- "Last year you had [N] rental properties at [addresses]. Same this year, or did you buy, sell, or stop renting any?"
- "Any major repairs or improvements to the rental properties this year?"
- "Any changes in how you manage them — switch to a property manager, or start managing yourself?"

---

## 6. Investments

### Q: Do you have any brokerage accounts — Schwab, Fidelity, Vanguard, Robinhood, anything like that?

**Why it matters:** Each brokerage account may generate a 1099-B (sales), 1099-DIV (dividends), and 1099-INT (interest). Even if the taxpayer didn't actively trade, mutual fund distributions and reinvested dividends are taxable events.

**What it unlocks:** 1099-B, 1099-DIV, 1099-INT document collection, Schedule D, Form 8949.

### Q: Did you sell any stocks, bonds, mutual funds, or crypto this year?

**Why it matters:** Each sale must be reported on Form 8949 with cost basis. Short-term gains (held under one year) are taxed as ordinary income; long-term gains get preferential rates (0%, 15%, or 20%). Net capital losses can offset up to $3,000 of ordinary income per year, with the remainder carrying forward.

**What it unlocks:** Schedule D, Form 8949, capital loss carryforward from prior years.

### Q: Do you have any retirement accounts — 401(k), traditional IRA, Roth IRA?

**Why it matters:** Traditional IRA contributions may be deductible depending on income and whether the taxpayer is covered by an employer plan. Roth contributions aren't deductible but aren't taxed on withdrawal. 401(k) contributions reduce W-2 box 1 income. Excess contributions trigger a 6% penalty.

**What it unlocks:** IRA deduction (Form 8606), Roth conversion reporting, excess contribution penalties, Required Minimum Distribution tracking for taxpayers 73+.

### Q: Did you contribute to a traditional IRA or do a Roth conversion this year?

**Why it matters:** Traditional IRA deductibility depends on AGI and employer plan coverage. Roth conversions are taxable events in the year of conversion — the full converted amount is added to income. Backdoor Roth conversions (non-deductible traditional IRA contribution followed by conversion) require careful Form 8606 reporting to avoid double taxation.

**What it unlocks:** Form 8606, Roth conversion income, pro-rata rule calculation if the taxpayer has pre-tax IRA balances.

### Q: Did you receive any stock options, RSUs, or participate in an employee stock purchase plan (ESPP)?

**Why it matters:** RSU income is included in W-2 wages at vesting. ISO exercises may trigger Alternative Minimum Tax (AMT). NSO exercises are ordinary income at exercise. ESPP discounts are ordinary income when shares are sold. Each type has a different tax treatment and different reporting requirements.

**What it unlocks:** AMT calculation (Form 6251) for ISOs, W-2 cross-referencing for RSUs, cost basis adjustments for ESPP sales, Form 3921 (ISO) and Form 3922 (ESPP).

### Q: Did you invest in any cryptocurrency, or sell/trade/use crypto this year?

**Why it matters:** The IRS treats cryptocurrency as property. Every sale, trade, or use to purchase goods is a taxable event. Many crypto platforms issue 1099s with incomplete cost basis — manual tracking is often necessary.

**What it unlocks:** Form 8949 for crypto transactions, Schedule D, "Yes" checkbox on the digital assets question on Form 1040.

#### Returning User

- "Last year you had accounts at [brokerages]. Any new accounts, or did you close any?"
- "You had RSUs vesting from [employer] last year. Still receiving those?"
- "Any new crypto activity, or same situation as last year?"
- "Did you do a Roth conversion this year like you did last year?"

---

## 7. K-1 Sources

### Q: Are you a partner or shareholder in any business — partnerships, S-corporations, or LLCs taxed as partnerships?

**Why it matters:** K-1s report the taxpayer's share of income, deductions, and credits from pass-through entities. K-1 income is taxable to the individual regardless of whether cash was distributed. The character of income (ordinary, capital gain, rental) flows through to the individual return.

**What it unlocks:** Schedule E Part II, passive vs non-passive classification, QBI deduction, basis limitation tracking.

### Q: Do you have any angel investments, syndication deals, or private fund investments?

**Why it matters:** Angel investments and real estate syndications generate K-1s, often with losses in early years. These losses are subject to passive activity rules, at-risk rules, and basis limitations. Many investors don't realize they need to track basis across years.

**What it unlocks:** K-1 document tracking, passive loss carryforward, at-risk basis worksheets, potential Section 1202 (QSBS) exclusion for startup investments.

### Q: A heads-up — K-1s are usually the last tax documents to arrive, often in March or even April. Do you know if all of yours are in yet?

**Why it matters:** K-1 delays are the number one reason returns get extended. Setting expectations early prevents the taxpayer from wondering why their return isn't filed yet when they've "sent everything."

**What it unlocks:** Extension filing decision (Form 4868), timeline expectations.

#### Returning User

- "Last year you had K-1s from [entities]. Expecting the same ones this year?"
- "Any new investments that would generate a K-1 — partnerships, syndications, funds?"
- "Have all your K-1s arrived yet, or are you still waiting on any?"

---

## 8. Bank Accounts

### Q: Do you have any savings accounts, money market accounts, or CDs that earned interest this year?

**Why it matters:** Interest income over $10 triggers a 1099-INT from the bank. Even under $10, the income is technically taxable — it just may not be reported to the IRS. With high interest rate environments, savings account interest can be surprisingly large.

**What it unlocks:** 1099-INT document collection, Schedule B if total interest exceeds $1,500.

### Q: Do you have any accounts at foreign banks or financial institutions? At any point during the year, did the combined value exceed $10,000?

**Why it matters:** FBAR (FinCEN 114) filing is required if the aggregate value of all foreign accounts exceeds $10,000 at any point during the year. Penalties for non-filing are severe — up to $10,000 per year for non-willful violations. FATCA (Form 8938) has separate, higher thresholds.

**What it unlocks:** FBAR filing, Form 8938, Schedule B Part III foreign account questions.

#### Returning User

- "Last year you had interest income from [banks]. Same accounts this year?"
- "Any new savings accounts, CDs, or high-yield accounts opened this year?"
- "Still no foreign accounts, correct?"

---

## 9. Healthcare / HSA

### Q: Do you have a Health Savings Account (HSA)?

**Why it matters:** HSAs are triple-tax-advantaged: contributions are deductible, growth is tax-free, and qualified withdrawals are tax-free. Employer contributions reduce the deductible amount. The 2024 limits are $4,150 (individual) / $8,300 (family), with a $1,000 catch-up for 55+.

**What it unlocks:** Form 8889, HSA deduction, excess contribution penalty if over-contributed, Form 5498-SA cross-reference.

### Q: Did you make any personal contributions to your HSA beyond what your employer contributed?

**Why it matters:** Personal contributions are an above-the-line deduction, reducing AGI. This is one of the few remaining deductions available to all taxpayers regardless of whether they itemize. The deduction directly lowers AGI, which affects other phase-outs.

**What it unlocks:** Form 8889 Line 2, above-the-line deduction on Schedule 1.

### Q: Did you get your health insurance through the marketplace (HealthCare.gov or your state exchange)?

**Why it matters:** Marketplace insurance with advance premium tax credits requires reconciliation on Form 8962. If actual income differs from the estimate used when enrolling, the taxpayer may owe back credits or receive additional credits. Form 1095-A is required — the return cannot be filed without it.

**What it unlocks:** Form 8962, premium tax credit reconciliation, 1095-A document collection.

#### Returning User

- "You contributed to an HSA last year. Same this year? And was it the same contribution amount?"
- "Still on marketplace insurance, or did your coverage change?"

---

## 10. Life Changes

### Q: Any big life changes this year? Marriage, divorce, new baby, home purchase or sale, job loss, moved to a new state — anything like that?

**Why it matters:** This is a catch-all for events with significant tax implications that the taxpayer may not realize are relevant. Each event changes the return in specific ways — a home purchase adds mortgage interest and property taxes, a home sale may trigger the $250K/$500K exclusion, a baby adds a dependent and credits, a state move creates multi-state obligations.

**What it unlocks:** Varies by event — see sub-questions below.

### Q: (If home purchase) When did you close? Did you pay any points on the mortgage?

**Why it matters:** Mortgage interest and points paid are deductible on Schedule A. Points paid at closing are generally fully deductible in the year of purchase for a primary residence. The settlement statement (HUD-1/Closing Disclosure) has the exact amounts.

**What it unlocks:** Schedule A mortgage interest deduction, Form 1098, points deduction.

### Q: (If home sale) Was it your primary residence? How long did you live there?

**Why it matters:** The Section 121 exclusion allows $250,000 ($500,000 MFJ) of gain to be excluded if the home was the primary residence for 2 of the last 5 years. Partial exclusions may apply for shorter periods due to job change, health, or unforeseen circumstances.

**What it unlocks:** Section 121 exclusion calculation, Form 8949 if gain exceeds exclusion, depreciation recapture if home office was claimed.

### Q: (If moved states) What date did you move, and did you work in both states during the year?

**Why it matters:** Part-year resident returns are required in both states. Income allocation rules vary by state — some use days-based allocation, others require specific sourcing. The timing of the move determines how W-2 income, investment income, and deductions are split.

**What it unlocks:** Part-year resident state returns, income allocation, moving expense deduction (limited to active military after 2017).

### Q: (If divorce) Was the divorce finalized this year? Is there alimony involved?

**Why it matters:** Filing status is determined by marital status on December 31. Alimony from pre-2019 divorce agreements is deductible by the payer and taxable to the recipient. Post-2018 agreements have no tax effect. Property transfers in divorce are generally tax-free but affect future cost basis.

**What it unlocks:** Filing status determination, alimony deduction/income, property basis carryover.

### Q: (If job loss) Did you receive unemployment benefits or a severance package?

**Why it matters:** Unemployment compensation is fully taxable. Severance may have reduced withholding. Job search expenses are no longer deductible after 2017, but this is worth noting to manage expectations.

**What it unlocks:** 1099-G for unemployment, severance tax treatment, potential estimated payment shortfall.

#### Returning User

- "No major life changes last year. Anything different this year — home purchase, move, new family members?"
- "You bought a home last year. Any changes — refinance, sale, or new purchase?"
- "You moved states last year. Settled in [state] for the full year now?"

---

## 11. Estimated Tax Payments

### Q: Did you make any estimated tax payments this year — federal or state? If so, how much and when?

**Why it matters:** This is the most commonly forgotten item in tax preparation. Estimated payments that aren't accounted for result in an artificially high balance due, causing the taxpayer to think they owe far more than they do. Conversely, missed quarterly payments may trigger underpayment penalties.

**What it unlocks:** Form 1040 estimated payment credits, state return payment credits, underpayment penalty calculation (Form 2210).

### Q: Do you know the exact amounts for each quarter — Q1 (April 15), Q2 (June 15), Q3 (September 15), Q4 (January 15)?

**Why it matters:** The penalty is calculated per quarter, not annually. A taxpayer who paid nothing for Q1-Q3 but made a large Q4 payment will still have penalties for the first three quarters. Getting the per-quarter amounts right directly affects penalty calculations.

**What it unlocks:** Per-quarter penalty calculation on Form 2210, annualized income installment method if income was uneven.

### Q: Did you apply your prior-year overpayment to this year's estimated taxes?

**Why it matters:** Taxpayers often forget that they chose to apply last year's refund as a Q1 estimated payment. If this isn't captured, the Q1 payment appears missing, triggering a false penalty calculation.

**What it unlocks:** Q1 estimated payment credit, reconciliation with prior-year return.

#### Returning User

- "Last year you made quarterly estimated payments of approximately $[X] per quarter. Did you continue the same amounts this year?"
- "You applied $[X] of your refund to this year's estimates last time. Did you do that again?"
- "Any state estimated payments this year?"

---

## 12. Charitable Contributions

### Q: Did you make any charitable donations this year — cash, checks, credit card, or through a donor-advised fund?

**Why it matters:** Charitable contributions are an itemized deduction on Schedule A. Cash contributions to public charities are deductible up to 60% of AGI. Donor-advised fund contributions are deductible in the year of contribution, even if grants are made in later years.

**What it unlocks:** Schedule A charitable deduction, determines whether itemizing exceeds the standard deduction.

### Q: Did you donate any non-cash items — clothing, furniture, household goods, vehicles?

**Why it matters:** Non-cash donations must be valued at fair market value (what a willing buyer would pay). Items over $500 require Form 8283. Items over $5,000 require a qualified appraisal. Overvalued non-cash donations are a common audit trigger.

**What it unlocks:** Form 8283, fair market value determination, appraisal requirement.

### Q: For any single cash donation over $250, do you have a written acknowledgment from the charity?

**Why it matters:** The IRS requires contemporaneous written acknowledgment from the charity for any single contribution of $250 or more. Without it, the deduction is disallowed — even if the taxpayer has a cancelled check. This is a strict documentation rule.

**What it unlocks:** Substantiation verification, audit-proofing the charitable deduction.

### Q: Did you make any qualified charitable distributions (QCDs) from an IRA? This applies if you're 70 1/2 or older.

**Why it matters:** QCDs up to $105,000 (2024) satisfy the Required Minimum Distribution and are excluded from income entirely. This is better than a deduction because it reduces AGI, which affects Medicare premiums, Social Security taxation, and other AGI-sensitive calculations.

**What it unlocks:** QCD exclusion from income, RMD satisfaction, Form 1099-R reporting.

#### Returning User

- "Last year you claimed about $[X] in charitable deductions. Similar this year?"
- "You contributed to a donor-advised fund last year. Any new contributions this year?"
- "Any large non-cash donations — cars, artwork, significant household items?"

---

## 13. Education

### Q: Did you or a dependent attend college or take courses this year?

**Why it matters:** The American Opportunity Credit (up to $2,500 per student, first 4 years of college) and Lifetime Learning Credit (up to $2,000 per return) can significantly reduce tax liability. The AOC is partially refundable. Form 1098-T from the institution is required.

**What it unlocks:** Form 8863, 1098-T document collection, AOC vs LLC determination.

### Q: Did you pay student loan interest this year?

**Why it matters:** Student loan interest up to $2,500 is an above-the-line deduction, available even without itemizing. Phases out at higher incomes ($75K-$90K single, $155K-$185K MFJ for 2024). Form 1098-E from the loan servicer is the source document.

**What it unlocks:** Student loan interest deduction on Schedule 1, 1098-E document collection.

### Q: Did you contribute to a 529 education savings plan?

**Why it matters:** 529 contributions are not federally deductible, but many states offer a state income tax deduction or credit. The tax benefit varies significantly by state — some are very generous (e.g., unlimited deduction in some states), others offer nothing.

**What it unlocks:** State-specific 529 deduction, 1099-Q if distributions were taken.

### Q: Did you or a dependent receive any scholarships or grants?

**Why it matters:** Scholarships used for tuition and required fees are tax-free. Scholarships used for room and board are taxable income. The taxable portion must be reported on the student's return (or the parent's if claimed as a dependent). This also affects education credit calculations.

**What it unlocks:** Scholarship income reporting, education credit reduction for tax-free scholarships.

#### Returning User

- "Last year you claimed education credits for [dependent]. Still in school this year?"
- "You deducted student loan interest last year. Same lender and similar amount?"
- "Any new 529 contributions or distributions this year?"

---

## 14. State-Specific

### Q: Which state or states do you need to file in this year?

**Why it matters:** State filing obligations aren't always obvious. Income earned in a state, rental property in a state, or K-1 income sourced to a state can all create filing requirements — even if the taxpayer never lived there. Some states (like California) are aggressive about claiming former residents as still owing tax.

**What it unlocks:** State return preparation, multi-state credit calculations, residency status determination.

### Q: Were you a full-year resident of one state, or did you live in multiple states during the year?

**Why it matters:** Part-year residents must file part-year returns in each state, with income allocated based on residency dates and income sourcing rules. Full-year residents in states with no income tax (FL, TX, WA, NV, etc.) may still owe other states for income earned there.

**What it unlocks:** Part-year vs full-year resident return type, income allocation method.

### Q: Did you pay property taxes this year? On which properties?

**Why it matters:** State and local property taxes are deductible on Schedule A, but the SALT deduction is capped at $10,000 ($5,000 MFS). If the taxpayer also has state income tax, the combined SALT cap may already be reached — but property taxes should still be captured in case it matters.

**What it unlocks:** Schedule A SALT deduction, SALT cap calculation, state-specific property tax credits.

### Q: Did you pay any local or city income taxes?

**Why it matters:** Some cities and localities impose their own income taxes (New York City, many Ohio cities, Philadelphia, etc.). These are part of the SALT deduction and may require separate local returns.

**What it unlocks:** Local tax return filing, SALT deduction inclusion.

#### Returning User

- "Last year you filed in [states]. Same states this year, or any changes?"
- "Still a full-year resident of [state]?"
- "Property tax amounts similar to last year, or any significant changes — new assessment, new property?"
