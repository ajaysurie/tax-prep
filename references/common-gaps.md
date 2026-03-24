# Common Gaps — Frequently Missed Deductions and Credits

This reference organizes commonly missed tax items by taxpayer profile type.
During Phase 4 (Reconciliation), load this file and check each relevant section
based on the user's profile.

---

## Everyone (All Filers)

### Estimated Tax Payments
**What:** Quarterly payments to the IRS (and state) for income not subject to withholding.
**Who it applies to:** Anyone with investment income, rental income, self-employment income, or K-1 income. Also people whose withholding doesn't cover their tax liability.
**Why it's missed:** No form is mailed — the user has to remember they made payments.
**How to ask:** "Did you make estimated tax payments this year? Federal? State? How much each quarter?"

**Federal quarterly due dates (typical):**
- Q1: April 15
- Q2: June 15
- Q3: September 15
- Q4: January 15 (of the following year)

**Safe harbor rules (to avoid underpayment penalties):**
- Pay at least **90%** of the current year's tax liability, OR
- Pay at least **110%** of last year's tax liability (100% if AGI ≤ $150,000 MFJ)
- The 110% rule is the safer choice when income is unpredictable

**Tax impact:** Doesn't change your tax bill — but failure to pay estimated taxes triggers
penalties (currently ~8% annualized). Catching this in the CPA package helps avoid surprises.

### Charitable Contributions
**What:** Cash donations, non-cash donations (clothing, household items, vehicles), donor-advised fund contributions.
**Who:** Anyone who itemizes or anyone who made large donations.
**Why it's missed:** Small cash donations add up but aren't on any form. Non-cash donations are often forgotten.
**How to ask:** "Did you make any charitable donations this year? Cash, clothing/household item donations, or contributions to a donor-advised fund?"

**Documentation requirements:**
- Under $250: Bank record or written receipt
- $250+: Written acknowledgment from the charity
- Non-cash over $500: Form 8283 required
- Non-cash over $5,000: Qualified appraisal required

**Tax impact:** Deductible if itemizing. Cash donations up to 60% of AGI. Non-cash up to 30% of AGI.

### State and Local Tax (SALT) Deduction
**What:** State income tax paid + property tax paid (or state sales tax as alternative).
**Who:** Anyone who itemizes.
**Why it matters:** Capped at $10,000 combined ($5,000 MFS). If your state income tax + property tax exceeds $10,000, you're already at the cap. Knowing the breakdown helps the CPA optimize.
**How to ask:** (Usually captured elsewhere, but verify): "What was your total property tax on your primary residence?"

---

## Rental Property Owners

### Depreciation
**What:** Annual deduction for the wear and tear of the building (not land). 27.5 years for residential rental.
**Who:** Every rental property owner.
**Why it's missed:** It's not an out-of-pocket expense, so owners forget it. But the IRS recaptures it on sale whether you claimed it or not — so you should ALWAYS claim it.
**How to ask:** "Have you been depreciating each rental property? Do you know your current adjusted basis?"
**Tax impact:** Typically $5,000–$15,000+ per property per year. One of the most valuable rental deductions.
**Reference:** See `schedule-e-guide.md` for depreciation calculation details.

### Insurance Premiums
**What:** Landlord/property insurance, liability insurance, flood insurance.
**Who:** All rental property owners.
**Why it's missed:** Often paid annually, not monthly — easy to forget.
**How to ask:** "How much did you pay for insurance on each rental property?"
**Tax impact:** Fully deductible on Schedule E Line 9.

### Property Management Fees
**What:** Fees paid to a property management company.
**Who:** Owners who use property managers (typically 8-12% of rent).
**Why it's missed:** Sometimes bundled with rent collection and not tracked separately.
**How to ask:** "Do you use a property manager? What did you pay them this year?"

### Travel to Properties
**What:** Mileage or travel costs to manage rental properties.
**Who:** Owners who personally manage properties (visit for repairs, inspections, tenant showings).
**Why it's missed:** Casual trips aren't logged.
**How to ask:** "How often did you drive to your rental properties for management? Approximate total miles?"
**Tax impact:** IRS standard mileage rate × miles driven for rental management.

---

## Self-Employed / Business Income

### Home Office Deduction
**What:** Deduction for the portion of your home used exclusively and regularly for business.
**Who:** Self-employed individuals (Schedule C filers) with a dedicated workspace.
**Why it's missed:** People assume they don't qualify or it triggers audits (it doesn't if legitimate).
**How to ask:** "Do you have a dedicated space in your home used exclusively for your business? How many square feet?"

**S-Corp shareholders:** Cannot deduct home office on personal return. Must use accountable plan reimbursement through the S-Corp. See `references/s-corp-home-office.md`.

**Two methods:**
- Simplified: $5 per square foot, up to 300 sq ft = max $1,500
- Regular: Actual expenses (mortgage interest, property tax, utilities, insurance, repairs) × percentage of home used for business

### Vehicle Expenses
**What:** Business use of a personal vehicle.
**Who:** Self-employed individuals, rental property owners.
**How to ask:** "Did you use your personal vehicle for business? Approximate business miles?"
**Two methods:** Standard mileage rate OR actual expenses (gas, insurance, repairs, depreciation) × business use percentage.

### Health Insurance Premiums (Self-Employed)
**What:** Health, dental, and vision insurance premiums paid by the self-employed.
**Who:** Self-employed individuals not eligible for an employer plan.
**Why it's missed:** It's an adjustment to income (Form 1040 Line 17), not a Schedule C expense.
**How to ask:** "Did you pay for your own health insurance? Were you eligible for coverage through a spouse's employer?"
**Tax impact:** 100% deductible as an above-the-line deduction.

### Retirement Contributions (SEP-IRA, Solo 401k)
**What:** Tax-deductible retirement contributions for self-employed individuals.
**Who:** Anyone with Schedule C income.
**Why it's missed:** Contributions can be made up to the filing deadline (including extensions).
**How to ask:** "Did you contribute to a SEP-IRA or Solo 401(k)? You have until the filing deadline to contribute for this tax year."
**Tax impact:** Up to 25% of net self-employment income (SEP-IRA) or $23,500 + 25% employer match (Solo 401k for 2025).

---

## Investors

### Capital Loss Carryforward
**What:** Unused capital losses from prior years that can offset current gains.
**Who:** Anyone who had net capital losses exceeding $3,000 in a prior year.
**Why it's missed:** It's from a prior year return — the user may not remember.
**How to ask:** "Did you have capital losses that exceeded $3,000 in any prior year? Your CPA or prior return would show a carryforward amount."
**Tax impact:** Offsets capital gains dollar-for-dollar, plus up to $3,000 against ordinary income per year.

### Wash Sale Adjustments
**What:** Disallowed losses when you sell a security at a loss and buy a substantially identical security within 30 days before or after.
**Who:** Active traders, anyone who sells and rebuys the same stock/fund.
**Why it matters:** The loss isn't gone — it's added to the cost basis of the replacement shares. But it must be tracked.
**How to check:** Review 1099-B for wash sale adjustments column. Flag any entries.

### Foreign Tax Credit
**What:** Credit for foreign taxes paid on international investments.
**Who:** Anyone with international mutual funds or ETFs, foreign stock.
**Why it's missed:** Shows up as Box 7 on 1099-DIV — easily overlooked.
**How to ask:** "Do any of your investment accounts hold international funds? Check your 1099-DIV for Box 7 (Foreign tax paid)."
**Tax impact:** Dollar-for-dollar credit against US tax. Often $50-$500 for typical portfolios.

---

## Families with Children

### Child and Dependent Care Credit (Form 2441)
**What:** Credit for child care expenses that enable you to work.
**Who:** Parents with children under 13 who pay for daycare, preschool, before/after school care, summer camp.
**Why it's missed:** People track it informally or it gets buried in other records.
**How to ask:** "Did you pay for child care (daycare, preschool, camp) for children under 13? Provider name(s), amounts, and provider EIN if you have it."
**Tax impact:** Credit of 20-35% of expenses, up to $3,000 per child ($6,000 for 2+). Non-refundable.

### Child Tax Credit
**What:** Credit for each qualifying child under 17.
**Who:** Parents with qualifying children.
**Why it matters:** Usually captured automatically through dependents, but verify the ages — children who turned 17 during the tax year no longer qualify.
**Tax impact:** $2,000 per qualifying child (2025). Partially refundable up to $1,700.

---

## Education

### Student Loan Interest Deduction
**What:** Deduction for interest paid on qualified student loans.
**Who:** Anyone paying student loans (income limits apply: phases out at $90K single / $185K MFJ for 2025).
**Why it's missed:** It's an above-the-line deduction — you get it even if you don't itemize.
**How to ask:** "Did you or your spouse pay student loan interest this year? Your servicer should have sent a 1098-E."
**Tax impact:** Up to $2,500 deduction.

### 529 Contributions
**What:** Contributions to a 529 education savings plan.
**Who:** Parents, grandparents, or anyone saving for education.
**Why it matters:** Not deductible federally, but many states (including NJ and NY) offer state tax deductions.
**How to ask:** "Did you contribute to a 529 plan this year?"
**Tax impact:** State-dependent. NJ: no deduction. NY: up to $5,000 deduction ($10,000 MFJ).

---

## Healthcare

### HSA Contributions
**What:** Contributions to a Health Savings Account.
**Who:** Anyone enrolled in a high-deductible health plan (HDHP).
**Why it's missed:** Employer contributions may be captured on W-2, but personal contributions (especially if made directly to the HSA provider) are sometimes forgotten.
**How to ask:** "Did you contribute to an HSA beyond what your employer contributes? The 2025 family limit is $8,550."
**Tax impact:** Triple-tax-advantaged: contributions are pre-tax, growth is tax-free, qualified withdrawals are tax-free. One of the best tax vehicles available.

### Medical Expenses (if extreme)
**What:** Out-of-pocket medical expenses exceeding 7.5% of AGI.
**Who:** Anyone with very high medical expenses (surgery, dental work, ongoing treatment).
**Why it's missed:** The threshold is high, so it only applies in unusual years.
**How to ask:** Only ask if the user mentions significant medical events: "You mentioned {medical event}. Did your out-of-pocket medical expenses exceed 7.5% of your income this year? If so, the excess is deductible."

---

## Multi-State Filers

### State Estimated Payments
**What:** Estimated tax payments made to each state.
**Who:** Anyone who files in multiple states or has income not subject to state withholding.
**Why it's missed:** Easy to confuse which payments went to which state, or to forget entirely.
**How to ask:** "Did you make estimated tax payments to {state}? How much each quarter?"

### State-Specific Deductions
**What:** Deductions that exist at the state level but not federally (or vice versa).
**Why it matters:** Each state has its own rules. See `state-guides/{state}.md` for details.
**Examples:**
- NJ: Property tax deduction (up to $15,000), no SALT cap at state level
- NY: 529 contributions deductible up to $5,000/$10,000
- CA: Additional credits for renters, dependent care differences
