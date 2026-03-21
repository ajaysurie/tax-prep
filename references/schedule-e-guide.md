# Schedule E Guide — Rental Property Tax Categorization

This reference maps common rental property expenses to their correct Schedule E
(Form 1040) line items, covers depreciation calculations, and handles property sales.

## Schedule E Part I: Income or Loss From Rental Real Estate

### Line-by-Line Mapping

| Line | IRS Description | Common Expenses That Map Here | Notes |
|------|----------------|-------------------------------|-------|
| 3 | Rents received | Gross rent collected from tenants | Include all rent, even if paid through a platform like Apartments.com |
| 5 | Advertising | Listing fees, online advertising, signage | Zillow, Apartments.com listing fees |
| 6 | Auto and travel | Mileage/travel to property for management | IRS standard mileage rate or actual expenses. Must be for property management, not commuting |
| 7 | Cleaning and maintenance | Cleaning between tenants, lawn care, snow removal, regular upkeep | Landscaping, gutter cleaning, HVAC filter replacement |
| 8 | Commissions | Real estate agent commissions for finding tenants | Broker fees, finder's fees |
| 9 | Insurance | Property insurance, landlord liability, flood insurance | NOT mortgage insurance (that's Line 12 "Other interest") |
| 10 | Legal and other professional fees | Attorney fees, accountant fees, eviction costs | Only the portion attributable to the rental property |
| 11 | Management fees | Property management company fees | Typically 8-12% of gross rent |
| 12 | Mortgage interest paid | Mortgage interest from 1098 | Match Box 1 of the 1098 for this property's loan |
| 13 | Other interest | Home equity loan interest used for the property, credit card interest for property expenses | Mortgage insurance premiums may also go here |
| 14 | Repairs | Fixing broken items, patching, painting, plumbing repairs | Must be repairs (restoring to original condition), NOT improvements (see below) |
| 15 | Supplies | Cleaning supplies, light bulbs, hardware, small tools | Items consumed in maintenance |
| 16 | Taxes | Property taxes, any local real estate taxes | Match against your property tax bill |
| 17 | Utilities | Electric, gas, water, sewer, trash if paid by landlord | Only if you pay — not if tenant pays directly |
| 18 | Depreciation expense | Annual depreciation deduction | Calculated below. This is NOT an out-of-pocket expense |
| 19 | Other | HOA/condo fees, pest control, home warranty | Anything that doesn't fit Lines 5-18 |

### Common Categorization Mistakes

**"Maintenance" is ambiguous.** Many people track a single "maintenance" bucket. Break it down:
- Routine upkeep (cleaning gutters, lawn care) → Line 7 (Cleaning and maintenance)
- Fixing something broken (plumbing leak, broken window) → Line 14 (Repairs)
- Upgrading something (new roof, new appliance) → NOT an expense — it's a capital improvement (added to basis)

**"Expenses" is too vague.** If your records have a generic "expenses" category, ask what's in it. Common contents: supplies (Line 15), small repairs (Line 14), or HOA fees (Line 19).

**Repairs vs. Improvements:**
- **Repair** (deductible this year): Fixes, patches, restores to working condition. Examples: fixing a leak, replacing a broken window, repainting.
- **Improvement** (capitalized, added to basis): Makes the property better, adapts it to new use, or extends its life. Examples: new roof, new kitchen, adding a bathroom, new HVAC system.
- Rule of thumb: If it would be a repair on a car (new brakes = repair, engine swap = improvement), the same logic applies to property.

---

## Depreciation

Depreciation is one of the most valuable deductions for rental property owners — and the most commonly missed because it's not an out-of-pocket expense. You must claim it whether you want to or not (the IRS recaptures it on sale regardless).

### Straight-Line Depreciation for Residential Rental Property

- **Useful life:** 27.5 years
- **Method:** Straight-line (equal amount each year)
- **Convention:** Mid-month (treat the property as placed in service in the middle of the month you acquired it)

### Calculating Depreciable Basis

```
Depreciable Basis = Purchase Price + Closing Costs + Improvements - Land Value
```

**Land value** is not depreciable — only the building. Determine land vs building value from:
1. Property tax assessment (shows land and improvement values separately)
2. Appraisal at time of purchase
3. County assessment records
4. Common ratio: 20-30% land, 70-80% building (varies significantly by location)

**Closing costs that increase basis:** Title insurance, recording fees, transfer taxes, legal fees for purchase. Do NOT include items prepaid at closing (property tax, insurance prepayment).

**Improvements after purchase:** New roof ($15,000), new HVAC ($8,000), kitchen renovation ($25,000) — each added to basis and depreciated over their own 27.5-year schedule starting from the date placed in service.

### Annual Depreciation Calculation

```
Annual Depreciation = Depreciable Basis / 27.5
```

**First year (mid-month convention):**
If you bought in June, you get 6.5 months of depreciation (mid-June through December).
```
First Year = (Annual Amount / 12) × (12 - month_acquired + 0.5)
```

**Example:**
- Purchase price: $400,000
- Land value (from tax assessment): $80,000 (20%)
- Building value: $320,000
- Annual depreciation: $320,000 / 27.5 = $11,636
- If acquired in June: first year = $11,636 / 12 × 6.5 = $6,303

### Tracking Depreciation

Ask the user:
1. "What was the purchase price of the property?"
2. "What is the land value? (Check your property tax assessment — it usually splits land and building.)"
3. "When did you acquire it?"
4. "Have you made any capital improvements since purchase? (New roof, HVAC, renovation, etc.)"
5. "Have you been claiming depreciation? What is your current adjusted basis?"

If the user has been working with a CPA, the CPA should have a depreciation schedule. If not, calculate it from acquisition date.

---

## Sold Properties

When a rental property is sold, several things happen:

### Capital Gain Calculation

```
Capital Gain = Sale Price - Selling Expenses - Adjusted Basis
Adjusted Basis = Original Basis + Improvements - Accumulated Depreciation
```

**Selling expenses:** Agent commissions, closing costs, transfer taxes, legal fees.

### Depreciation Recapture (Section 1250)

All accumulated depreciation is "recaptured" and taxed at a maximum rate of 25%
(not the favorable long-term capital gains rate). This applies even if you didn't
actually claim depreciation — the IRS assumes you did.

```
Depreciation Recapture Tax = Accumulated Depreciation × 25%
Remaining Gain Tax = (Total Gain - Accumulated Depreciation) × long-term capital gains rate
```

### Required Documents for Sold Property

- Closing Disclosure (CD) or HUD-1 Settlement Statement
- Original purchase closing documents (for basis)
- Records of all capital improvements
- Depreciation schedule from CPA or prior returns
- 1099-S (Proceeds from Real Estate Transactions) — issued by the closing agent

### Tax Forms

- **Form 4797:** Sale of business property (the rental)
- **Schedule D:** Capital gain/loss flows here
- **Form 8949:** Details of the sale transaction

Ask: "For the property you sold, I need: (1) the sale price and closing costs from the
Closing Disclosure, (2) your original purchase price and closing costs, (3) a list of
capital improvements with costs and dates, and (4) your accumulated depreciation
(your CPA should have this from prior returns)."

---

## Condo/Co-op Special Rules

- **Common charges / HOA fees:** Deductible on Line 19 (Other) for rental units
- **Special assessments:** If for repairs (new boiler for the building), deductible. If for improvements (new lobby renovation), added to basis.
- **Underlying mortgage:** Co-ops have a building-level mortgage. Your share of the interest is deductible on Line 12, and your share of the property tax on Line 16. The co-op should provide a statement annually.

---

## Multiple Properties

Schedule E supports up to 3 properties per page. If you have more than 3, use
additional Schedule E pages. Each property gets its own column.

Track all expenses per-property. Do not combine expenses across properties — the IRS
wants to see income and loss for each property separately.
