# JSON Schema Reference

Single source of truth for every JSON state file the skill writes to `~/.tax-prep/{year}/`.
All files include `"schema_version": "1.0"` at the top level.

---

## Table of Contents

1. [profile.json](#1-profilejson)
2. [accounts.json](#2-accountsjson)
3. [reconciliation.json](#3-reconciliationjson)
4. [federal-rates.json](#4-federal-ratesjson)
5. [state-rates/{state}.json](#5-state-ratesstatejson)
6. [documents/{id}.json](#6-documentsidjson)

---

## 1. profile.json

**Path:** `~/.tax-prep/{year}/profile.json`
**Created by:** Phase 1 (Situation Interview)
**Updated by:** Any phase if the user corrects or adds profile information mid-flow.

This is the foundation file. Every other phase reads from it to determine what accounts, documents, and deductions to expect.

### Example

```json
{
  "schema_version": "1.0",
  "tax_year": 2025,
  "created_at": "2026-01-18T14:30:00Z",
  "updated_at": "2026-02-10T09:15:00Z",
  "filing_status": "married_filing_jointly",
  "dependents": [
    {
      "name": "Emma Johnson",
      "date_of_birth": "2019-06-15",
      "relationship": "daughter",
      "ssn_last4": "4321",
      "qualifies_for_ctc": true
    },
    {
      "name": "Liam Johnson",
      "date_of_birth": "2022-03-08",
      "relationship": "son",
      "ssn_last4": "8765",
      "qualifies_for_ctc": true
    }
  ],
  "income_sources": {
    "w2": [
      {
        "employer": "Acme Corp",
        "ein": "12-3456789",
        "start_date": "2020-03-01",
        "end_date": null,
        "notes": "Primary employment, full year"
      }
    ],
    "self_employment": [
      {
        "business_name": "Johnson Consulting LLC",
        "ein": "98-7654321",
        "business_type": "single_member_llc",
        "activity": "Management consulting",
        "home_office": true,
        "vehicle_use": false,
        "notes": "Started Q2 2025"
      }
    ],
    "rental_properties": [
      {
        "address": "123 Main Street, Unit 2, Newark, NJ 07102",
        "date_acquired": "2018-05-15",
        "cost_basis": 285000,
        "ownership_percentage": 100,
        "property_type": "single_family",
        "status": "active",
        "mortgage_lender": "National Home Lending",
        "management_company": null,
        "notes": null
      },
      {
        "address": "456 Oak Avenue, Unit 1, Newark, NJ 07105",
        "date_acquired": "2021-09-01",
        "cost_basis": 340000,
        "ownership_percentage": 100,
        "property_type": "condo",
        "status": "active",
        "mortgage_lender": "Pacific Mortgage Co",
        "management_company": "Garden State Property Mgmt",
        "notes": "Common charges include water"
      }
    ],
    "investments": [
      {
        "institution": "Charles Schwab",
        "account_type": "brokerage",
        "notes": "Individual taxable account"
      },
      {
        "institution": "Fidelity",
        "account_type": "brokerage",
        "notes": "Joint account"
      },
      {
        "institution": "Fidelity",
        "account_type": "401k",
        "notes": "Employer plan via Acme Corp, traditional contributions"
      }
    ],
    "k1_sources": [
      {
        "entity_name": "Sunrise Ventures Fund II LP",
        "ein": "55-1234567",
        "entity_type": "partnership",
        "notes": "Angel syndicate investment, expect K-1 by March 15"
      }
    ],
    "bank_accounts": [
      {
        "institution": "Amex",
        "account_type": "high_yield_savings",
        "interest_expected": true,
        "notes": "High yield savings, expect 1099-INT"
      },
      {
        "institution": "Chase",
        "account_type": "checking",
        "interest_expected": false,
        "notes": "Minimal interest, likely under $10"
      }
    ]
  },
  "deduction_categories": [
    {
      "category": "mortgage_interest",
      "applies": true,
      "notes": "Two properties with mortgages"
    },
    {
      "category": "property_tax",
      "applies": true,
      "notes": "Primary residence + 2 rentals"
    },
    {
      "category": "state_local_tax",
      "applies": true,
      "notes": "NJ income tax, subject to SALT cap"
    },
    {
      "category": "charitable",
      "applies": true,
      "notes": "Cash donations to local charities"
    },
    {
      "category": "hsa",
      "applies": true,
      "notes": "Family HSA through employer"
    },
    {
      "category": "child_care",
      "applies": true,
      "notes": "Two children in daycare"
    },
    {
      "category": "education",
      "applies": false,
      "notes": null
    },
    {
      "category": "student_loan_interest",
      "applies": false,
      "notes": null
    },
    {
      "category": "home_office",
      "applies": true,
      "notes": "For Johnson Consulting LLC"
    },
    {
      "category": "estimated_payments",
      "applies": true,
      "notes": "Federal and NJ state quarterly payments"
    }
  ],
  "life_changes": [
    {
      "event": "new_business",
      "description": "Started Johnson Consulting LLC in April 2025",
      "tax_impact": "Schedule C, self-employment tax, estimated payments"
    }
  ],
  "states": [
    {
      "state": "NJ",
      "residency": "full_year",
      "notes": "Primary residence"
    }
  ],
  "primary_residence": {
    "address": "123 Main Street, Montclair, NJ 07042",
    "property_tax_annual": 14200,
    "notes": null
  },
  "estimated_payments": {
    "federal": [
      { "quarter": "Q1", "due_date": "2025-04-15", "amount": 3000, "date_paid": "2025-04-14" },
      { "quarter": "Q2", "due_date": "2025-06-16", "amount": 3000, "date_paid": "2025-06-15" },
      { "quarter": "Q3", "due_date": "2025-09-15", "amount": 3000, "date_paid": "2025-09-14" },
      { "quarter": "Q4", "due_date": "2026-01-15", "amount": 3000, "date_paid": "2026-01-10" }
    ],
    "state": [
      {
        "state": "NJ",
        "payments": [
          { "quarter": "Q1", "due_date": "2025-04-15", "amount": 1500, "date_paid": "2025-04-14" },
          { "quarter": "Q2", "due_date": "2025-06-16", "amount": 1500, "date_paid": "2025-06-15" },
          { "quarter": "Q3", "due_date": "2025-09-15", "amount": 1500, "date_paid": "2025-09-14" },
          { "quarter": "Q4", "due_date": "2026-01-15", "amount": 1500, "date_paid": "2026-01-10" }
        ]
      }
    ]
  },
  "prior_year_ref": "2024"
}
```

### Field Definitions

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `schema_version` | string | **yes** | Always `"1.0"` |
| `tax_year` | integer | **yes** | The tax year being prepared (e.g., `2025`) |
| `created_at` | string (ISO 8601) | **yes** | Timestamp when the profile was first created |
| `updated_at` | string (ISO 8601) | **yes** | Timestamp of the most recent update |
| `filing_status` | string (enum) | **yes** | One of: `"single"`, `"married_filing_jointly"`, `"married_filing_separately"`, `"head_of_household"`, `"qualifying_surviving_spouse"` |
| `dependents` | array | **yes** | Array of dependent objects. Empty array `[]` if none. |
| `dependents[].name` | string | **yes** | Full name of the dependent |
| `dependents[].date_of_birth` | string (YYYY-MM-DD) | **yes** | Date of birth |
| `dependents[].relationship` | string (enum) | **yes** | One of: `"son"`, `"daughter"`, `"stepchild"`, `"foster_child"`, `"sibling"`, `"parent"`, `"other"` |
| `dependents[].ssn_last4` | string | optional | Last 4 digits of SSN, for CPA reference |
| `dependents[].qualifies_for_ctc` | boolean | **yes** | Whether the dependent qualifies for the Child Tax Credit (under age 17 at end of tax year) |
| `income_sources` | object | **yes** | Contains all income source categories |
| `income_sources.w2` | array | **yes** | W-2 employers. Empty array if none. |
| `income_sources.w2[].employer` | string | **yes** | Employer name |
| `income_sources.w2[].ein` | string | optional | Employer Identification Number |
| `income_sources.w2[].start_date` | string (YYYY-MM-DD) | optional | Employment start date |
| `income_sources.w2[].end_date` | string or null | optional | Employment end date. `null` if still employed. |
| `income_sources.w2[].notes` | string or null | optional | Any relevant context |
| `income_sources.self_employment` | array | **yes** | Self-employment / Schedule C businesses. Empty array if none. |
| `income_sources.self_employment[].business_name` | string | **yes** | Legal business name |
| `income_sources.self_employment[].ein` | string | optional | Business EIN |
| `income_sources.self_employment[].business_type` | string (enum) | **yes** | One of: `"sole_proprietor"`, `"single_member_llc"`, `"partnership"`, `"s_corp"` |
| `income_sources.self_employment[].activity` | string | **yes** | Description of business activity |
| `income_sources.self_employment[].home_office` | boolean | **yes** | Whether a home office deduction applies |
| `income_sources.self_employment[].vehicle_use` | boolean | **yes** | Whether business vehicle use applies |
| `income_sources.self_employment[].notes` | string or null | optional | Additional context |
| `income_sources.rental_properties` | array | **yes** | Rental properties. Empty array if none. |
| `income_sources.rental_properties[].address` | string | **yes** | Full property address |
| `income_sources.rental_properties[].date_acquired` | string (YYYY-MM-DD) | **yes** | Acquisition date |
| `income_sources.rental_properties[].cost_basis` | number | **yes** | Original purchase price (for depreciation) |
| `income_sources.rental_properties[].ownership_percentage` | number | **yes** | 1-100 |
| `income_sources.rental_properties[].property_type` | string (enum) | **yes** | One of: `"single_family"`, `"condo"`, `"multi_family"`, `"townhouse"`, `"commercial"` |
| `income_sources.rental_properties[].status` | string (enum) | **yes** | One of: `"active"`, `"sold"`, `"vacant"` |
| `income_sources.rental_properties[].mortgage_lender` | string or null | **yes** | Lender name, or `null` if owned outright |
| `income_sources.rental_properties[].management_company` | string or null | optional | Property management company, or `null` |
| `income_sources.rental_properties[].notes` | string or null | optional | Additional context |
| `income_sources.investments` | array | **yes** | Investment/brokerage/retirement accounts. Empty array if none. |
| `income_sources.investments[].institution` | string | **yes** | Brokerage or custodian name |
| `income_sources.investments[].account_type` | string (enum) | **yes** | One of: `"brokerage"`, `"401k"`, `"403b"`, `"traditional_ira"`, `"roth_ira"`, `"sep_ira"`, `"hsa"`, `"529"`, `"espp"` |
| `income_sources.investments[].notes` | string or null | optional | Additional context |
| `income_sources.k1_sources` | array | **yes** | K-1 entities. Empty array if none. |
| `income_sources.k1_sources[].entity_name` | string | **yes** | Partnership or S-corp name |
| `income_sources.k1_sources[].ein` | string | optional | Entity EIN |
| `income_sources.k1_sources[].entity_type` | string (enum) | **yes** | One of: `"partnership"`, `"s_corp"`, `"trust"` |
| `income_sources.k1_sources[].notes` | string or null | optional | Additional context |
| `income_sources.bank_accounts` | array | **yes** | Bank accounts. Empty array if none. |
| `income_sources.bank_accounts[].institution` | string | **yes** | Bank name |
| `income_sources.bank_accounts[].account_type` | string (enum) | **yes** | One of: `"checking"`, `"savings"`, `"high_yield_savings"`, `"cd"`, `"money_market"` |
| `income_sources.bank_accounts[].interest_expected` | boolean | **yes** | Whether a 1099-INT is expected (interest likely > $10) |
| `income_sources.bank_accounts[].notes` | string or null | optional | Additional context |
| `deduction_categories` | array | **yes** | Deduction categories that apply to this filer |
| `deduction_categories[].category` | string (enum) | **yes** | One of: `"mortgage_interest"`, `"property_tax"`, `"state_local_tax"`, `"charitable"`, `"medical"`, `"hsa"`, `"child_care"`, `"education"`, `"student_loan_interest"`, `"home_office"`, `"estimated_payments"`, `"vehicle_expenses"`, `"other"` |
| `deduction_categories[].applies` | boolean | **yes** | Whether this category is relevant for the tax year |
| `deduction_categories[].notes` | string or null | optional | Context or detail |
| `life_changes` | array | **yes** | Significant life events affecting taxes. Empty array if none. |
| `life_changes[].event` | string (enum) | **yes** | One of: `"marriage"`, `"divorce"`, `"new_dependent"`, `"home_purchase"`, `"home_sale"`, `"property_sale"`, `"new_business"`, `"job_change"`, `"state_move"`, `"retirement"`, `"inheritance"`, `"other"` |
| `life_changes[].description` | string | **yes** | Free-text description of the event |
| `life_changes[].tax_impact` | string | **yes** | Brief note on how this affects the return |
| `states` | array | **yes** | States the user files in |
| `states[].state` | string | **yes** | Two-letter state code (e.g., `"NJ"`) |
| `states[].residency` | string (enum) | **yes** | One of: `"full_year"`, `"part_year"`, `"nonresident"` |
| `states[].notes` | string or null | optional | Context (e.g., "Moved to NJ from NY in June") |
| `primary_residence` | object or null | **yes** | Primary home details. `null` if renting. |
| `primary_residence.address` | string | **yes** | Full address |
| `primary_residence.property_tax_annual` | number or null | **yes** | Annual property tax. `null` if unknown at interview time. |
| `primary_residence.notes` | string or null | optional | Additional context |
| `estimated_payments` | object | **yes** | Estimated tax payments made during the year |
| `estimated_payments.federal` | array | **yes** | Federal quarterly payments. Empty array if none. |
| `estimated_payments.federal[].quarter` | string | **yes** | `"Q1"`, `"Q2"`, `"Q3"`, or `"Q4"` |
| `estimated_payments.federal[].due_date` | string (YYYY-MM-DD) | **yes** | IRS due date for that quarter |
| `estimated_payments.federal[].amount` | number | **yes** | Amount paid |
| `estimated_payments.federal[].date_paid` | string (YYYY-MM-DD) | **yes** | Actual date the payment was made |
| `estimated_payments.state` | array | **yes** | Per-state quarterly payments. Empty array if none. |
| `estimated_payments.state[].state` | string | **yes** | Two-letter state code |
| `estimated_payments.state[].payments` | array | **yes** | Array of quarterly payment objects (same shape as federal) |
| `prior_year_ref` | string or null | **yes** | Tax year of the prior year profile used as baseline. `null` if first-time user. |

### Notes

- The profile is the first file created and the most frequently updated. Any phase can add information to it (e.g., the user mentions a forgotten K-1 during reconciliation).
- When updating, always bump `updated_at`.
- The `prior_year_ref` field links to the prior year's state directory. If `~/.tax-prep/{prior_year_ref}/profile.json` exists, Phase 1 uses it to pre-populate and ask "what changed?"
- Dollar amounts are stored as numbers (not strings). Use full precision -- do not round.
- All dates use ISO 8601 format.

---

## 2. accounts.json

**Path:** `~/.tax-prep/{year}/accounts.json`
**Created by:** Phase 2 (Account Discovery)
**Updated by:** Phase 3 (Document Collection) updates `status` and `parsed_data` on each expected document as documents arrive.

This is the master checklist. It maps every financial account to the tax documents it should produce, and tracks whether each document has been received and parsed.

### Example

```json
{
  "schema_version": "1.0",
  "tax_year": 2025,
  "created_at": "2026-01-20T10:00:00Z",
  "updated_at": "2026-03-05T16:45:00Z",
  "accounts": [
    {
      "id": "acme-corp-w2",
      "institution": "Acme Corp",
      "account_type": "employer",
      "account_label": "Primary W-2 employment",
      "source": "profile",
      "expected_documents": [
        {
          "doc_id": "acme-corp-w2-2025",
          "form_type": "W-2",
          "description": "Wage and tax statement",
          "expected_by": "2026-01-31",
          "status": "received",
          "received_date": "2026-01-25",
          "document_ref": "acme-corp-w2-2025",
          "parsed_data": {
            "box1_wages": 185000.00,
            "box2_federal_withheld": 38500.00,
            "box3_ss_wages": 168600.00,
            "box4_ss_withheld": 10453.20,
            "box5_medicare_wages": 185000.00,
            "box6_medicare_withheld": 2682.50,
            "box12_codes": {
              "D": 23500.00,
              "W": 7300.00
            },
            "box16_state_wages": 185000.00,
            "box17_state_withheld": 11200.00,
            "state": "NJ"
          }
        }
      ]
    },
    {
      "id": "schwab-brokerage",
      "institution": "Charles Schwab",
      "account_type": "brokerage",
      "account_label": "Individual taxable brokerage",
      "source": "profile",
      "expected_documents": [
        {
          "doc_id": "schwab-1099b-2025",
          "form_type": "1099-B",
          "description": "Proceeds from broker transactions",
          "expected_by": "2026-02-15",
          "status": "received",
          "received_date": "2026-02-12",
          "document_ref": "schwab-1099b-2025",
          "parsed_data": {
            "total_proceeds": 45230.50,
            "total_cost_basis": 38100.00,
            "short_term_gain_loss": 1200.50,
            "long_term_gain_loss": 5930.00,
            "wash_sale_disallowed": 320.00,
            "federal_withheld": 0
          }
        },
        {
          "doc_id": "schwab-1099div-2025",
          "form_type": "1099-DIV",
          "description": "Dividend income",
          "expected_by": "2026-02-15",
          "status": "received",
          "received_date": "2026-02-12",
          "document_ref": "schwab-1099div-2025",
          "parsed_data": {
            "box1a_ordinary_dividends": 3420.18,
            "box1b_qualified_dividends": 2890.00,
            "box2a_capital_gain_distributions": 410.25,
            "box3_nondividend_distributions": 0,
            "box4_federal_withheld": 0,
            "box7_foreign_tax_paid": 85.30,
            "box11_exempt_interest_dividends": 0
          }
        }
      ]
    },
    {
      "id": "amex-hysa",
      "institution": "Amex",
      "account_type": "bank",
      "account_label": "High yield savings account",
      "source": "profile",
      "expected_documents": [
        {
          "doc_id": "amex-1099int-2025",
          "form_type": "1099-INT",
          "description": "Interest income",
          "expected_by": "2026-01-31",
          "status": "received",
          "received_date": "2026-01-28",
          "document_ref": "amex-1099int-2025",
          "parsed_data": {
            "box1_interest_income": 1842.67,
            "box2_early_withdrawal_penalty": 0,
            "box3_us_savings_bond_interest": 0,
            "box4_federal_withheld": 0,
            "box8_tax_exempt_interest": 0
          }
        }
      ]
    },
    {
      "id": "wells-fargo-87-smith",
      "institution": "National Home Lending",
      "account_type": "mortgage",
      "account_label": "Mortgage — 123 Main Street",
      "source": "profile",
      "expected_documents": [
        {
          "doc_id": "wells-fargo-1098-87smith-2025",
          "form_type": "1098",
          "description": "Mortgage interest statement",
          "expected_by": "2026-01-31",
          "status": "pending",
          "received_date": null,
          "document_ref": null,
          "parsed_data": null
        }
      ]
    },
    {
      "id": "sunrise-ventures-k1",
      "institution": "Sunrise Ventures Fund II LP",
      "account_type": "partnership",
      "account_label": "Angel syndicate investment",
      "source": "profile",
      "expected_documents": [
        {
          "doc_id": "sunrise-k1-2025",
          "form_type": "K-1",
          "description": "Partner's share of income, deductions, credits",
          "expected_by": "2026-03-15",
          "status": "pending",
          "received_date": null,
          "document_ref": null,
          "parsed_data": null,
          "notes": "K-1s frequently delayed. Partnerships may file extension to September 15."
        }
      ]
    },
    {
      "id": "johnson-consulting-1099nec",
      "institution": "Various clients",
      "account_type": "self_employment",
      "account_label": "1099-NEC income for Johnson Consulting LLC",
      "source": "profile",
      "expected_documents": [
        {
          "doc_id": "client-a-1099nec-2025",
          "form_type": "1099-NEC",
          "description": "Nonemployee compensation — Client A",
          "expected_by": "2026-01-31",
          "status": "received",
          "received_date": "2026-01-30",
          "document_ref": "client-a-1099nec-2025",
          "parsed_data": {
            "box1_nonemployee_compensation": 42000.00,
            "box4_federal_withheld": 0,
            "payer_name": "Globex Industries",
            "payer_ein": "33-4455667"
          }
        }
      ]
    },
    {
      "id": "fidelity-hsa",
      "institution": "Fidelity",
      "account_type": "hsa",
      "account_label": "Health Savings Account",
      "source": "profile",
      "expected_documents": [
        {
          "doc_id": "fidelity-1099sa-2025",
          "form_type": "1099-SA",
          "description": "HSA distributions",
          "expected_by": "2026-01-31",
          "status": "not_applicable",
          "received_date": null,
          "document_ref": null,
          "parsed_data": null,
          "notes": "No distributions taken in 2025"
        },
        {
          "doc_id": "fidelity-5498sa-2025",
          "form_type": "5498-SA",
          "description": "HSA contributions",
          "expected_by": "2026-05-31",
          "status": "pending",
          "received_date": null,
          "document_ref": null,
          "parsed_data": null,
          "notes": "5498-SA arrives late (May). Contribution amounts usually known from pay stubs."
        }
      ]
    }
  ],
  "rental_property_expenses": [
    {
      "property_address": "123 Main Street, Unit 2, Newark, NJ 07102",
      "gross_rent_collected": 36000.00,
      "expenses": {
        "advertising": 0,
        "auto_and_travel": 150.00,
        "cleaning_and_maintenance": 2400.00,
        "commissions": 0,
        "insurance": 1800.00,
        "legal_and_professional": 0,
        "management_fees": 0,
        "mortgage_interest": null,
        "other_interest": 0,
        "repairs": 3200.00,
        "supplies": 280.00,
        "taxes": 6800.00,
        "utilities": 0,
        "depreciation": 10363.64,
        "other": 0
      },
      "expenses_complete": false,
      "notes": "Mortgage interest will be populated from 1098 when received"
    }
  ],
  "child_care_expenses": [
    {
      "provider_name": "Bright Horizons Daycare",
      "provider_ein": "22-3344556",
      "provider_address": "456 Oak Avenue, Montclair, NJ 07042",
      "amount_paid": 24000.00,
      "child_name": "Emma Johnson"
    },
    {
      "provider_name": "Bright Horizons Daycare",
      "provider_ein": "22-3344556",
      "provider_address": "456 Oak Avenue, Montclair, NJ 07042",
      "amount_paid": 24000.00,
      "child_name": "Liam Johnson"
    }
  ],
  "charitable_contributions": {
    "cash": [
      {
        "organization": "Montclair Community Foundation",
        "amount": 2500.00,
        "date": "2025-12-15",
        "receipt": true
      }
    ],
    "non_cash": [
      {
        "organization": "Goodwill Industries",
        "description": "Clothing and household items",
        "fair_market_value": 800.00,
        "date": "2025-06-20",
        "receipt": true
      }
    ]
  },
  "summary": {
    "total_accounts": 7,
    "total_expected_documents": 10,
    "received": 5,
    "pending": 4,
    "not_applicable": 1
  }
}
```

### Field Definitions

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `schema_version` | string | **yes** | Always `"1.0"` |
| `tax_year` | integer | **yes** | The tax year |
| `created_at` | string (ISO 8601) | **yes** | Timestamp when the accounts file was first created |
| `updated_at` | string (ISO 8601) | **yes** | Timestamp of the most recent update |
| `accounts` | array | **yes** | Array of account objects |
| `accounts[].id` | string | **yes** | Unique slug identifier (kebab-case). Used for matching and references. |
| `accounts[].institution` | string | **yes** | Financial institution or employer name |
| `accounts[].account_type` | string (enum) | **yes** | One of: `"employer"`, `"brokerage"`, `"bank"`, `"mortgage"`, `"partnership"`, `"s_corp"`, `"trust"`, `"self_employment"`, `"hsa"`, `"retirement"`, `"rental_platform"`, `"insurance"`, `"other"` |
| `accounts[].account_label` | string | **yes** | Human-readable description of the account |
| `accounts[].source` | string (enum) | **yes** | How this account was discovered. One of: `"profile"`, `"monarch"`, `"prior_year"`, `"manual"`, `"document_upload"` |
| `accounts[].expected_documents` | array | **yes** | Tax documents expected from this account |
| `accounts[].expected_documents[].doc_id` | string | **yes** | Unique identifier for this expected document. Format: `{institution-slug}-{form-type}-{year}`. Used as the filename for `documents/{id}.json`. |
| `accounts[].expected_documents[].form_type` | string (enum) | **yes** | One of: `"W-2"`, `"1099-INT"`, `"1099-DIV"`, `"1099-B"`, `"1099-NEC"`, `"1099-K"`, `"1099-R"`, `"1099-SA"`, `"1099-MISC"`, `"1098"`, `"1098-T"`, `"K-1"`, `"5498"`, `"5498-SA"`, `"1095-A"`, `"1095-B"`, `"1095-C"`, `"SSA-1099"`, `"other"` |
| `accounts[].expected_documents[].description` | string | **yes** | Human-readable description of the form |
| `accounts[].expected_documents[].expected_by` | string (YYYY-MM-DD) | **yes** | Typical date by which this form should be available |
| `accounts[].expected_documents[].status` | string (enum) | **yes** | One of: `"pending"`, `"received"`, `"not_applicable"` |
| `accounts[].expected_documents[].received_date` | string (YYYY-MM-DD) or null | **yes** | Date the document was received. `null` if not yet received. |
| `accounts[].expected_documents[].document_ref` | string or null | **yes** | References `doc_id`, which corresponds to `documents/{doc_id}.json`. `null` if not yet received. |
| `accounts[].expected_documents[].parsed_data` | object or null | **yes** | Inline summary of extracted fields. `null` if not yet received. Full detail is in the individual document file. |
| `accounts[].expected_documents[].notes` | string or null | optional | Additional context (e.g., "K-1s frequently delayed") |
| `rental_property_expenses` | array | optional | Per-property expense tracking for Schedule E. Created during Phase 3 as rental documents arrive. |
| `rental_property_expenses[].property_address` | string | **yes** | Must match an address in `profile.json` `rental_properties` |
| `rental_property_expenses[].gross_rent_collected` | number | **yes** | Total rent received for the year |
| `rental_property_expenses[].expenses` | object | **yes** | Schedule E expense categories. Keys match IRS Schedule E line items. |
| `rental_property_expenses[].expenses_complete` | boolean | **yes** | Whether all expense data has been collected |
| `rental_property_expenses[].notes` | string or null | optional | Context about missing or pending data |
| `child_care_expenses` | array | optional | For Child and Dependent Care Credit (Form 2441) |
| `child_care_expenses[].provider_name` | string | **yes** | Daycare or care provider name |
| `child_care_expenses[].provider_ein` | string | optional | Provider's EIN (required for Form 2441) |
| `child_care_expenses[].provider_address` | string | optional | Provider's address |
| `child_care_expenses[].amount_paid` | number | **yes** | Total amount paid during the year |
| `child_care_expenses[].child_name` | string | **yes** | Name of the child receiving care |
| `charitable_contributions` | object | optional | Charitable donation tracking |
| `charitable_contributions.cash` | array | optional | Cash donations |
| `charitable_contributions.cash[].organization` | string | **yes** | Name of the charity |
| `charitable_contributions.cash[].amount` | number | **yes** | Donation amount |
| `charitable_contributions.cash[].date` | string (YYYY-MM-DD) | optional | Date of donation |
| `charitable_contributions.cash[].receipt` | boolean | **yes** | Whether a receipt/acknowledgment letter was obtained |
| `charitable_contributions.non_cash` | array | optional | Non-cash donations |
| `charitable_contributions.non_cash[].organization` | string | **yes** | Name of the charity |
| `charitable_contributions.non_cash[].description` | string | **yes** | Description of items donated |
| `charitable_contributions.non_cash[].fair_market_value` | number | **yes** | Estimated FMV |
| `charitable_contributions.non_cash[].date` | string (YYYY-MM-DD) | optional | Date of donation |
| `charitable_contributions.non_cash[].receipt` | boolean | **yes** | Whether a receipt was obtained |
| `summary` | object | **yes** | Aggregate counts for progress reporting |
| `summary.total_accounts` | integer | **yes** | Total number of accounts |
| `summary.total_expected_documents` | integer | **yes** | Total expected tax documents |
| `summary.received` | integer | **yes** | Documents with `status: "received"` |
| `summary.pending` | integer | **yes** | Documents with `status: "pending"` |
| `summary.not_applicable` | integer | **yes** | Documents with `status: "not_applicable"` |

### Notes

- The `parsed_data` inline on each expected document is a summary for quick reference. The full extracted data lives in `documents/{doc_id}.json`.
- When a document is received, update three things: (1) `status` to `"received"`, (2) `received_date`, (3) `document_ref` to the doc_id, (4) `parsed_data` with key fields.
- The `summary` object must be recalculated every time a document status changes.
- `rental_property_expenses`, `child_care_expenses`, and `charitable_contributions` are collected during Phases 2-3 and live here because they are not tied to a single tax form. They are supplemental data the user provides beyond what appears on official documents.
- When a user uploads a document that does not match any expected item, add a new account entry with `source: "document_upload"`.

---

## 3. reconciliation.json

**Path:** `~/.tax-prep/{year}/reconciliation.json`
**Created by:** Phase 4 (Reconciliation)
**Updated by:** Re-run reconciliation if new documents arrive after initial run.

This file captures every finding from the reconciliation process: completeness gaps, year-over-year comparisons, Monarch discrepancies, and open questions for the CPA.

### Example

```json
{
  "schema_version": "1.0",
  "tax_year": 2025,
  "created_at": "2026-03-10T11:00:00Z",
  "updated_at": "2026-03-15T14:30:00Z",
  "run_count": 2,
  "completeness": {
    "total_expected": 10,
    "received": 7,
    "pending": 2,
    "not_applicable": 1,
    "pending_items": [
      {
        "doc_id": "wells-fargo-1098-87smith-2025",
        "form_type": "1098",
        "institution": "National Home Lending",
        "expected_by": "2026-01-31",
        "days_overdue": 38,
        "category": "potentially_forgotten",
        "suggested_action": "Check National Home Lending online portal or call their customer service number"
      },
      {
        "doc_id": "sunrise-k1-2025",
        "form_type": "K-1",
        "institution": "Sunrise Ventures Fund II LP",
        "expected_by": "2026-03-15",
        "days_overdue": 0,
        "category": "delayed",
        "suggested_action": "K-1s are commonly late. Partnership deadline is March 15 but extensions are frequent. Check with fund manager."
      }
    ]
  },
  "year_over_year": {
    "prior_year": 2024,
    "comparisons": [
      {
        "category": "W-2 Wages",
        "source": "Acme Corp",
        "current_year": 185000.00,
        "prior_year": 172000.00,
        "change_amount": 13000.00,
        "change_percent": 7.6,
        "flag": null,
        "notes": "Normal annual increase"
      },
      {
        "category": "1099-NEC",
        "source": "Johnson Consulting LLC",
        "current_year": 42000.00,
        "prior_year": 0,
        "change_amount": 42000.00,
        "change_percent": null,
        "flag": "new_item",
        "notes": "New self-employment income. Ensure Schedule C is filed and quarterly estimated payments cover SE tax."
      },
      {
        "category": "1099-DIV Ordinary",
        "source": "Charles Schwab",
        "current_year": 3420.18,
        "prior_year": 2950.00,
        "change_amount": 470.18,
        "change_percent": 15.9,
        "flag": null,
        "notes": null
      },
      {
        "category": "Rental Net Income",
        "source": "123 Main Street",
        "current_year": null,
        "prior_year": 8200.00,
        "change_amount": null,
        "change_percent": null,
        "flag": "incomplete_data",
        "notes": "Cannot compare — 1098 not yet received, rental expenses incomplete"
      }
    ],
    "missing_from_prior_year": [
      {
        "category": "1099-INT",
        "source": "First Republic Bank",
        "prior_year_amount": 245.00,
        "explanation": null,
        "suggested_action": "Did this account close or move to a different bank?"
      }
    ]
  },
  "monarch_reconciliation": {
    "performed": true,
    "monarch_export_date": "2026-03-01",
    "discrepancies": [
      {
        "category": "interest_income",
        "institution": "Amex",
        "form_amount": 1842.67,
        "monarch_amount": 1838.42,
        "difference": 4.25,
        "severity": "minor",
        "notes": "Difference likely due to timing of December interest posting. Within acceptable range."
      }
    ],
    "matches": [
      {
        "category": "dividend_income",
        "institution": "Charles Schwab",
        "form_amount": 3420.18,
        "monarch_amount": 3418.90,
        "difference": 1.28,
        "severity": "match",
        "notes": null
      }
    ]
  },
  "gap_detection": [
    {
      "category": "estimated_payments",
      "status": "verified",
      "details": "Federal: $12,000 ($3,000/quarter). NJ: $6,000 ($1,500/quarter). Verified in profile.",
      "action_required": false
    },
    {
      "category": "hsa_contributions",
      "status": "needs_verification",
      "details": "Profile indicates HSA through employer. W-2 Box 12 code W shows $7,300 employer contributions. Need to confirm no additional personal contributions were made outside payroll.",
      "action_required": true
    },
    {
      "category": "capital_loss_carryforward",
      "status": "needs_verification",
      "details": "Prior year had $3,000 capital loss deduction. Check prior year return for remaining carryforward amount.",
      "action_required": true
    },
    {
      "category": "home_office",
      "status": "needs_data",
      "details": "Johnson Consulting LLC uses home office. Need: total home square footage, office square footage, and home expenses (rent/mortgage interest, utilities, insurance) for simplified or regular method.",
      "action_required": true
    }
  ],
  "rental_property_validation": [
    {
      "property_address": "123 Main Street, Unit 2, Newark, NJ 07102",
      "status": "incomplete",
      "issues": [
        {
          "field": "mortgage_interest",
          "issue": "1098 not yet received from National Home Lending",
          "severity": "blocking"
        },
        {
          "field": "depreciation",
          "issue": "Need to verify current depreciation basis and method with CPA",
          "severity": "cpa_question"
        }
      ]
    },
    {
      "property_address": "456 Oak Avenue, Unit 1, Newark, NJ 07105",
      "status": "complete",
      "issues": []
    }
  ],
  "investment_validation": [
    {
      "institution": "Charles Schwab",
      "flags": [
        {
          "type": "wash_sale",
          "details": "1099-B shows $320.00 in wash sale disallowed losses. CPA should verify these are properly handled.",
          "severity": "informational"
        }
      ]
    }
  ],
  "open_questions": [
    {
      "id": "oq-001",
      "category": "depreciation",
      "question": "What is the current adjusted basis and depreciation schedule for 123 Main Street? Need to verify mid-month convention and 27.5-year residential method.",
      "for": "cpa",
      "status": "open"
    },
    {
      "id": "oq-002",
      "category": "safe_harbor",
      "question": "Self-employment income is new this year. Did estimated payments meet the safe harbor threshold (110% of prior year tax since AGI > $150K)?",
      "for": "cpa",
      "status": "open"
    },
    {
      "id": "oq-003",
      "category": "home_office",
      "question": "Simplified method ($5/sqft, max 300 sqft = $1,500) vs regular method — which is more beneficial? Need home expense data to compare.",
      "for": "user",
      "status": "open"
    }
  ]
}
```

### Field Definitions

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `schema_version` | string | **yes** | Always `"1.0"` |
| `tax_year` | integer | **yes** | The tax year |
| `created_at` | string (ISO 8601) | **yes** | First reconciliation run |
| `updated_at` | string (ISO 8601) | **yes** | Most recent reconciliation run |
| `run_count` | integer | **yes** | Number of times reconciliation has been run (increments on re-run) |
| `completeness` | object | **yes** | Document completeness assessment |
| `completeness.total_expected` | integer | **yes** | From `accounts.json` summary |
| `completeness.received` | integer | **yes** | Documents with status `"received"` |
| `completeness.pending` | integer | **yes** | Documents still outstanding |
| `completeness.not_applicable` | integer | **yes** | Documents determined not needed |
| `completeness.pending_items` | array | **yes** | Detail on each pending document |
| `completeness.pending_items[].doc_id` | string | **yes** | References the doc_id in accounts.json |
| `completeness.pending_items[].form_type` | string | **yes** | Form type |
| `completeness.pending_items[].institution` | string | **yes** | Issuing institution |
| `completeness.pending_items[].expected_by` | string (YYYY-MM-DD) | **yes** | Original expected date |
| `completeness.pending_items[].days_overdue` | integer | **yes** | Days past expected date. `0` if not yet due. |
| `completeness.pending_items[].category` | string (enum) | **yes** | One of: `"delayed"` (known-late forms like K-1s), `"potentially_forgotten"` (past due date, user should follow up), `"not_yet_due"` (still within expected window) |
| `completeness.pending_items[].suggested_action` | string | **yes** | Actionable advice for the user |
| `year_over_year` | object or null | **yes** | Year-over-year comparison. `null` if no prior year data. |
| `year_over_year.prior_year` | integer | **yes** | The prior tax year being compared |
| `year_over_year.comparisons` | array | **yes** | Line-item comparisons |
| `year_over_year.comparisons[].category` | string | **yes** | Income or deduction category |
| `year_over_year.comparisons[].source` | string | **yes** | Account or institution |
| `year_over_year.comparisons[].current_year` | number or null | **yes** | Current year amount. `null` if data not yet available. |
| `year_over_year.comparisons[].prior_year` | number | **yes** | Prior year amount |
| `year_over_year.comparisons[].change_amount` | number or null | **yes** | Dollar change. `null` if current year data missing. |
| `year_over_year.comparisons[].change_percent` | number or null | **yes** | Percentage change. `null` if prior year was 0 or current year missing. |
| `year_over_year.comparisons[].flag` | string (enum) or null | **yes** | One of: `"new_item"` (did not exist last year), `"large_increase"` (>20%), `"large_decrease"` (>20%), `"incomplete_data"`, or `null` (normal) |
| `year_over_year.comparisons[].notes` | string or null | optional | Context or explanation |
| `year_over_year.missing_from_prior_year` | array | **yes** | Items present last year but not this year |
| `year_over_year.missing_from_prior_year[].category` | string | **yes** | Form/income type |
| `year_over_year.missing_from_prior_year[].source` | string | **yes** | Institution or account |
| `year_over_year.missing_from_prior_year[].prior_year_amount` | number | **yes** | Amount from last year |
| `year_over_year.missing_from_prior_year[].explanation` | string or null | **yes** | User-provided explanation. `null` until confirmed. |
| `year_over_year.missing_from_prior_year[].suggested_action` | string | **yes** | Question to ask the user |
| `monarch_reconciliation` | object or null | optional | Monarch CSV comparison. `null` if no Monarch export provided. |
| `monarch_reconciliation.performed` | boolean | **yes** | Whether reconciliation was run |
| `monarch_reconciliation.monarch_export_date` | string (YYYY-MM-DD) | **yes** | Date the Monarch export was generated |
| `monarch_reconciliation.discrepancies` | array | **yes** | Items where form and Monarch amounts differ |
| `monarch_reconciliation.discrepancies[].category` | string | **yes** | Type of income (interest, dividends, etc.) |
| `monarch_reconciliation.discrepancies[].institution` | string | **yes** | Financial institution |
| `monarch_reconciliation.discrepancies[].form_amount` | number | **yes** | Amount from the tax form |
| `monarch_reconciliation.discrepancies[].monarch_amount` | number | **yes** | Amount from Monarch transactions |
| `monarch_reconciliation.discrepancies[].difference` | number | **yes** | Absolute difference |
| `monarch_reconciliation.discrepancies[].severity` | string (enum) | **yes** | One of: `"match"` (< $5), `"minor"` ($5-$50), `"major"` (> $50) |
| `monarch_reconciliation.discrepancies[].notes` | string or null | optional | Explanation |
| `monarch_reconciliation.matches` | array | **yes** | Items that reconcile within tolerance |
| `gap_detection` | array | **yes** | Commonly missed items checked against profile |
| `gap_detection[].category` | string | **yes** | What was checked |
| `gap_detection[].status` | string (enum) | **yes** | One of: `"verified"` (confirmed complete), `"needs_verification"` (data exists but needs user confirmation), `"needs_data"` (missing entirely), `"not_applicable"` |
| `gap_detection[].details` | string | **yes** | What was found or what is needed |
| `gap_detection[].action_required` | boolean | **yes** | Whether the user needs to do something |
| `rental_property_validation` | array | optional | Per-property validation (only if rental properties exist) |
| `rental_property_validation[].property_address` | string | **yes** | Matches address in profile and accounts |
| `rental_property_validation[].status` | string (enum) | **yes** | One of: `"complete"`, `"incomplete"`, `"sold"` |
| `rental_property_validation[].issues` | array | **yes** | List of issues found. Empty array if none. |
| `rental_property_validation[].issues[].field` | string | **yes** | Which data point has the issue |
| `rental_property_validation[].issues[].issue` | string | **yes** | Description of the problem |
| `rental_property_validation[].issues[].severity` | string (enum) | **yes** | One of: `"blocking"` (cannot package without this), `"cpa_question"` (needs CPA guidance), `"informational"` (FYI) |
| `investment_validation` | array | optional | Per-institution investment checks (only if investments exist) |
| `investment_validation[].institution` | string | **yes** | Brokerage or custodian |
| `investment_validation[].flags` | array | **yes** | Issues found. Empty array if clean. |
| `investment_validation[].flags[].type` | string (enum) | **yes** | One of: `"wash_sale"`, `"missing_cost_basis"`, `"carryforward"`, `"large_gain"`, `"large_loss"`, `"other"` |
| `investment_validation[].flags[].details` | string | **yes** | Explanation |
| `investment_validation[].flags[].severity` | string (enum) | **yes** | One of: `"blocking"`, `"cpa_question"`, `"informational"` |
| `open_questions` | array | **yes** | Questions that need answers before packaging |
| `open_questions[].id` | string | **yes** | Unique identifier (format: `oq-NNN`) |
| `open_questions[].category` | string | **yes** | Topic area |
| `open_questions[].question` | string | **yes** | The question in plain language |
| `open_questions[].for` | string (enum) | **yes** | Who needs to answer: `"user"` or `"cpa"` |
| `open_questions[].status` | string (enum) | **yes** | One of: `"open"`, `"resolved"` |

### Notes

- Reconciliation can be run multiple times as new documents arrive. Each run increments `run_count` and updates `updated_at`.
- On re-run, the entire file is regenerated from current state (not appended to). This ensures the file always reflects the current picture.
- The `open_questions` array feeds directly into Tab 11 of the CPA package.
- Severity levels have specific meanings: `"blocking"` means the CPA package cannot be finalized without this data; `"cpa_question"` means the CPA needs to make a judgment call; `"informational"` is FYI only.

---

## 4. federal-rates.json

**Path:** `~/.tax-prep/{year}/federal-rates.json`
**Created by:** Phase 1 (Situation Interview) after verifying rates via web search.
**Updated by:** Rarely. Only if the user runs Phase 1 again or rates are corrected.

This file caches IRS data for the tax year so we do not re-fetch it every session. The baseline values come from `references/tax-data-sources.md` and are verified via WebSearch.

### Example

```json
{
  "schema_version": "1.0",
  "tax_year": 2025,
  "fetched_at": "2026-01-18T14:35:00Z",
  "source": "IRS.gov, verified via web search",
  "standard_deduction": {
    "single": 15700,
    "married_filing_jointly": 31400,
    "married_filing_separately": 15700,
    "head_of_household": 23500,
    "additional_65_or_older": 1600,
    "additional_65_or_older_single": 2050
  },
  "tax_brackets": {
    "single": [
      { "min": 0, "max": 11925, "rate": 0.10 },
      { "min": 11925, "max": 48475, "rate": 0.12 },
      { "min": 48475, "max": 103350, "rate": 0.22 },
      { "min": 103350, "max": 197300, "rate": 0.24 },
      { "min": 197300, "max": 250525, "rate": 0.32 },
      { "min": 250525, "max": 626350, "rate": 0.35 },
      { "min": 626350, "max": null, "rate": 0.37 }
    ],
    "married_filing_jointly": [
      { "min": 0, "max": 23850, "rate": 0.10 },
      { "min": 23850, "max": 96950, "rate": 0.12 },
      { "min": 96950, "max": 206700, "rate": 0.22 },
      { "min": 206700, "max": 394600, "rate": 0.24 },
      { "min": 394600, "max": 501050, "rate": 0.32 },
      { "min": 501050, "max": 751600, "rate": 0.35 },
      { "min": 751600, "max": null, "rate": 0.37 }
    ],
    "married_filing_separately": [
      { "min": 0, "max": 11925, "rate": 0.10 },
      { "min": 11925, "max": 48475, "rate": 0.12 },
      { "min": 48475, "max": 103350, "rate": 0.22 },
      { "min": 103350, "max": 197300, "rate": 0.24 },
      { "min": 197300, "max": 250525, "rate": 0.32 },
      { "min": 250525, "max": 375800, "rate": 0.35 },
      { "min": 375800, "max": null, "rate": 0.37 }
    ],
    "head_of_household": [
      { "min": 0, "max": 17000, "rate": 0.10 },
      { "min": 17000, "max": 64850, "rate": 0.12 },
      { "min": 64850, "max": 103350, "rate": 0.22 },
      { "min": 103350, "max": 197300, "rate": 0.24 },
      { "min": 197300, "max": 250500, "rate": 0.32 },
      { "min": 250500, "max": 626350, "rate": 0.35 },
      { "min": 626350, "max": null, "rate": 0.37 }
    ]
  },
  "contribution_limits": {
    "401k_employee": 23500,
    "401k_catch_up_50_plus": 7500,
    "401k_catch_up_60_to_63": 11250,
    "ira_traditional": 7000,
    "ira_catch_up_50_plus": 1000,
    "hsa_individual": 4300,
    "hsa_family": 8550,
    "hsa_catch_up_55_plus": 1000,
    "fsa_healthcare": 3300,
    "fsa_dependent_care": 5000,
    "sep_ira_max": 70000,
    "529_gift_tax_exclusion": 19000
  },
  "capital_gains_thresholds": {
    "zero_percent": {
      "single": 48350,
      "married_filing_jointly": 96700,
      "head_of_household": 64750
    },
    "fifteen_percent": {
      "single": 533400,
      "married_filing_jointly": 600050,
      "head_of_household": 566700
    },
    "twenty_percent": {
      "single": 533401,
      "married_filing_jointly": 600051,
      "head_of_household": 566701
    },
    "net_investment_income_tax": {
      "threshold_single": 200000,
      "threshold_mfj": 250000,
      "rate": 0.038
    }
  },
  "salt_cap": 10000,
  "self_employment_tax_rate": 0.153,
  "self_employment_income_threshold": 400,
  "social_security_wage_base": 176100,
  "estimated_payment_dates": {
    "Q1": "2025-04-15",
    "Q2": "2025-06-16",
    "Q3": "2025-09-15",
    "Q4": "2026-01-15"
  },
  "safe_harbor": {
    "current_year_percent": 0.90,
    "prior_year_percent_under_150k": 1.00,
    "prior_year_percent_over_150k": 1.10,
    "notes": "To avoid underpayment penalty, pay the lesser of 90% of current year tax or 110% of prior year tax (100% if AGI <= $150K)"
  },
  "child_tax_credit": {
    "amount_per_child": 2000,
    "refundable_portion": 1700,
    "phase_out_single": 200000,
    "phase_out_mfj": 400000,
    "qualifying_age": 16
  },
  "child_and_dependent_care_credit": {
    "max_expenses_one_child": 3000,
    "max_expenses_two_plus": 6000,
    "credit_percentage_range": "20% to 35% based on AGI"
  },
  "amt": {
    "exemption_single": 88100,
    "exemption_mfj": 137000,
    "phase_out_single": 626350,
    "phase_out_mfj": 1252700,
    "rate_26_percent_threshold": 242150
  }
}
```

### Field Definitions

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `schema_version` | string | **yes** | Always `"1.0"` |
| `tax_year` | integer | **yes** | The tax year these rates apply to |
| `fetched_at` | string (ISO 8601) | **yes** | When the data was retrieved/verified |
| `source` | string | **yes** | Where the data was verified from |
| `standard_deduction` | object | **yes** | Standard deduction amounts by filing status |
| `standard_deduction.single` | number | **yes** | Amount for single filers |
| `standard_deduction.married_filing_jointly` | number | **yes** | Amount for MFJ |
| `standard_deduction.married_filing_separately` | number | **yes** | Amount for MFS |
| `standard_deduction.head_of_household` | number | **yes** | Amount for HoH |
| `standard_deduction.additional_65_or_older` | number | **yes** | Additional amount for married filers 65+ |
| `standard_deduction.additional_65_or_older_single` | number | **yes** | Additional amount for single/HoH filers 65+ |
| `tax_brackets` | object | **yes** | Marginal tax brackets per filing status |
| `tax_brackets.{status}` | array | **yes** | Array of bracket objects, ordered by `min` ascending |
| `tax_brackets.{status}[].min` | number | **yes** | Lower bound of the bracket (inclusive) |
| `tax_brackets.{status}[].max` | number or null | **yes** | Upper bound (exclusive). `null` for the top bracket. |
| `tax_brackets.{status}[].rate` | number | **yes** | Decimal rate (e.g., `0.22` for 22%) |
| `contribution_limits` | object | **yes** | Annual contribution limits for tax-advantaged accounts |
| `contribution_limits.401k_employee` | number | **yes** | Employee elective deferral limit |
| `contribution_limits.401k_catch_up_50_plus` | number | **yes** | Additional catch-up for age 50+ |
| `contribution_limits.401k_catch_up_60_to_63` | number | **yes** | Enhanced catch-up for SECURE 2.0 (age 60-63) |
| `contribution_limits.ira_traditional` | number | **yes** | Traditional/Roth IRA contribution limit |
| `contribution_limits.ira_catch_up_50_plus` | number | **yes** | IRA catch-up amount |
| `contribution_limits.hsa_individual` | number | **yes** | HSA limit for self-only coverage |
| `contribution_limits.hsa_family` | number | **yes** | HSA limit for family coverage |
| `contribution_limits.hsa_catch_up_55_plus` | number | **yes** | HSA catch-up amount |
| `contribution_limits.fsa_healthcare` | number | **yes** | Healthcare FSA limit |
| `contribution_limits.fsa_dependent_care` | number | **yes** | Dependent care FSA limit |
| `contribution_limits.sep_ira_max` | number | **yes** | SEP-IRA maximum contribution |
| `contribution_limits.529_gift_tax_exclusion` | number | **yes** | Annual gift tax exclusion (per beneficiary) |
| `capital_gains_thresholds` | object | **yes** | Long-term capital gains rate breakpoints |
| `capital_gains_thresholds.zero_percent` | object | **yes** | Taxable income thresholds for 0% rate, by filing status |
| `capital_gains_thresholds.fifteen_percent` | object | **yes** | Upper threshold for 15% rate |
| `capital_gains_thresholds.twenty_percent` | object | **yes** | Threshold where 20% rate begins |
| `capital_gains_thresholds.net_investment_income_tax` | object | **yes** | 3.8% NIIT thresholds |
| `salt_cap` | number | **yes** | State and local tax deduction cap |
| `self_employment_tax_rate` | number | **yes** | Combined SE tax rate (Social Security + Medicare) |
| `self_employment_income_threshold` | number | **yes** | Minimum net SE income to owe SE tax |
| `social_security_wage_base` | number | **yes** | Maximum wages subject to Social Security tax |
| `estimated_payment_dates` | object | **yes** | Due dates for quarterly estimated payments |
| `safe_harbor` | object | **yes** | Safe harbor rules for avoiding underpayment penalty |
| `child_tax_credit` | object | **yes** | CTC amounts and phase-out thresholds |
| `child_and_dependent_care_credit` | object | **yes** | Form 2441 limits |
| `amt` | object | **yes** | Alternative Minimum Tax exemption and phase-out thresholds |

### Notes

- All dollar amounts are integers (no cents) since IRS thresholds are published as whole numbers.
- Tax bracket rates are stored as decimals (e.g., `0.22`) not percentages (e.g., `22`).
- The `tax_brackets` object should include all four filing statuses. The `qualifying_surviving_spouse` status uses the same brackets as `married_filing_jointly`.
- This file is fetched once per tax year and cached. If WebSearch is unavailable (Cowork mode), the values from `references/tax-data-sources.md` are used directly without verification.
- The bracket values in this example are illustrative. Always verify via WebSearch against IRS publications for the actual tax year.

---

## 5. state-rates/{state}.json

**Path:** `~/.tax-prep/{year}/state-rates/{state}.json` (e.g., `state-rates/nj.json`)
**Created by:** Phase 1 after identifying filing states, verified via WebSearch.
**Updated by:** Rarely. Only if corrected or a new state is added.

One file per state the user files in. The filename is the lowercase two-letter state code.

### Example (NJ)

```json
{
  "schema_version": "1.0",
  "tax_year": 2025,
  "state": "NJ",
  "state_name": "New Jersey",
  "fetched_at": "2026-01-18T14:40:00Z",
  "source": "NJ Division of Taxation, verified via web search",
  "income_tax": {
    "filing_statuses": ["single", "married_filing_jointly", "married_filing_separately", "head_of_household"],
    "brackets": {
      "single": [
        { "min": 0, "max": 20000, "rate": 0.014 },
        { "min": 20000, "max": 35000, "rate": 0.0175 },
        { "min": 35000, "max": 40000, "rate": 0.035 },
        { "min": 40000, "max": 75000, "rate": 0.05525 },
        { "min": 75000, "max": 500000, "rate": 0.0637 },
        { "min": 500000, "max": 1000000, "rate": 0.0897 },
        { "min": 1000000, "max": null, "rate": 0.1075 }
      ],
      "married_filing_jointly": [
        { "min": 0, "max": 20000, "rate": 0.014 },
        { "min": 20000, "max": 50000, "rate": 0.0175 },
        { "min": 50000, "max": 70000, "rate": 0.0245 },
        { "min": 70000, "max": 80000, "rate": 0.035 },
        { "min": 80000, "max": 150000, "rate": 0.05525 },
        { "min": 150000, "max": 500000, "rate": 0.0637 },
        { "min": 500000, "max": 1000000, "rate": 0.0897 },
        { "min": 1000000, "max": null, "rate": 0.1075 }
      ]
    },
    "notes": "NJ has separate brackets for MFJ. Does not conform to federal."
  },
  "standard_deductions": {
    "notes": "NJ does not have a standard deduction. Taxpayers claim personal exemptions instead."
  },
  "personal_exemptions": {
    "single": 1000,
    "married_filing_jointly": 2000,
    "dependent": 1500,
    "notes": "NJ personal exemptions are small and have income phase-outs"
  },
  "property_tax_deduction": {
    "max_deduction": 15000,
    "notes": "NJ allows a property tax deduction up to $15,000 for property taxes paid on a primary residence. This is a state-level deduction separate from the federal SALT cap."
  },
  "credits": [
    {
      "name": "Earned Income Tax Credit",
      "description": "NJ EITC is 40% of the federal EITC",
      "eligibility": "Must qualify for federal EITC",
      "notes": null
    },
    {
      "name": "Child and Dependent Care Credit",
      "description": "NJ mirrors the federal credit",
      "eligibility": "Same as federal Form 2441 requirements",
      "notes": null
    },
    {
      "name": "Homestead Benefit",
      "description": "Property tax relief for homeowners. Applied separately, not on the tax return.",
      "eligibility": "Must be NJ homeowner, income limits apply",
      "notes": "Application deadline is typically November. Not a line item on the NJ return but worth mentioning to the user."
    }
  ],
  "estimated_payment_dates": {
    "Q1": "2025-04-15",
    "Q2": "2025-06-16",
    "Q3": "2025-09-15",
    "Q4": "2026-01-15"
  },
  "other": {
    "reciprocity_agreements": ["PA"],
    "local_taxes": "NJ does not have local income taxes. Newark and some cities have payroll taxes but these are employer-side.",
    "pass_through_entity_tax": "NJ allows PTE election for partnerships and S-corps. Check if any K-1 entities elected PTE.",
    "notes": null
  }
}
```

### Field Definitions

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `schema_version` | string | **yes** | Always `"1.0"` |
| `tax_year` | integer | **yes** | Tax year |
| `state` | string | **yes** | Two-letter state code |
| `state_name` | string | **yes** | Full state name |
| `fetched_at` | string (ISO 8601) | **yes** | When data was retrieved/verified |
| `source` | string | **yes** | Source of the data |
| `income_tax` | object | **yes** | State income tax structure |
| `income_tax.filing_statuses` | array of strings | **yes** | Filing statuses the state recognizes |
| `income_tax.brackets` | object | **yes** | Tax brackets per filing status. Same structure as federal: array of `{min, max, rate}` objects. |
| `income_tax.notes` | string or null | optional | State-specific notes about tax structure |
| `standard_deductions` | object | **yes** | State standard deduction. May be `null` or have a `notes` field explaining the state does not use a standard deduction. |
| `personal_exemptions` | object | optional | If the state uses personal exemptions |
| `property_tax_deduction` | object | optional | State-level property tax deduction rules (separate from federal SALT) |
| `property_tax_deduction.max_deduction` | number | **yes** | Maximum deductible amount |
| `property_tax_deduction.notes` | string | **yes** | Explanation of the rule |
| `credits` | array | **yes** | State tax credits relevant to the user's profile. Empty array if none. |
| `credits[].name` | string | **yes** | Credit name |
| `credits[].description` | string | **yes** | What it does |
| `credits[].eligibility` | string | **yes** | Who qualifies |
| `credits[].notes` | string or null | optional | Additional context |
| `estimated_payment_dates` | object | **yes** | State quarterly estimated payment due dates |
| `other` | object | optional | Catch-all for state-specific items |
| `other.reciprocity_agreements` | array of strings | optional | States with reciprocal tax agreements |
| `other.local_taxes` | string | optional | Local/city tax notes |
| `other.pass_through_entity_tax` | string | optional | PTE election notes if applicable |
| `other.notes` | string or null | optional | Anything else |

### Notes

- State tax structures vary wildly. Some states have no income tax (TX, FL, WA, etc.). For those states, the file is still created but `income_tax.brackets` is an empty object and `income_tax.notes` explains "No state income tax."
- Not all fields apply to every state. The schema is flexible -- include what's relevant and omit what isn't.
- The `credits` array should include only credits relevant to the user's profile (based on `profile.json`), not an exhaustive list of all state credits.
- `references/state-guides/{state}.md` provides the detailed guide for user-facing state-specific questions. This JSON file is the cached, structured data.

---

## 6. documents/{id}.json

**Path:** `~/.tax-prep/{year}/documents/{id}.json` (e.g., `documents/schwab-1099div-2025.json`)
**Created by:** Phase 3 (Document Collection) when a document is parsed.
**Updated by:** If the user provides corrections after initial parsing.

Each file stores the complete extracted data from a single tax document. The `id` matches the `doc_id` in `accounts.json`.

### Example (1099-DIV)

```json
{
  "schema_version": "1.0",
  "doc_id": "schwab-1099div-2025",
  "tax_year": 2025,
  "created_at": "2026-02-12T10:30:00Z",
  "updated_at": "2026-02-12T10:30:00Z",
  "form_type": "1099-DIV",
  "institution": "Charles Schwab",
  "payer_ein": "94-1234567",
  "account_ref": "schwab-brokerage",
  "input_method": "pdf_upload",
  "user_confirmed": true,
  "fields": {
    "box1a_ordinary_dividends": 3420.18,
    "box1b_qualified_dividends": 2890.00,
    "box2a_capital_gain_distributions": 410.25,
    "box2b_unrecaptured_1250_gain": 0,
    "box2c_section_1202_gain": 0,
    "box2d_collectibles_gain": 0,
    "box2e_section_897_ordinary": 0,
    "box2f_section_897_capital_gain": 0,
    "box3_nondividend_distributions": 0,
    "box4_federal_withheld": 0,
    "box5_section_199a_dividends": 0,
    "box6_investment_expenses": 0,
    "box7_foreign_tax_paid": 85.30,
    "box8_foreign_country": "Various",
    "box9_cash_liquidation": 0,
    "box10_noncash_liquidation": 0,
    "box11_exempt_interest_dividends": 0,
    "box12_specified_private_activity_bond": 0,
    "box13_state": "NJ",
    "box14_state_id": null,
    "box15_state_tax_withheld": 0
  },
  "notes": null
}
```

### Example (W-2)

```json
{
  "schema_version": "1.0",
  "doc_id": "acme-corp-w2-2025",
  "tax_year": 2025,
  "created_at": "2026-01-25T09:00:00Z",
  "updated_at": "2026-01-25T09:15:00Z",
  "form_type": "W-2",
  "institution": "Acme Corp",
  "payer_ein": "12-3456789",
  "account_ref": "acme-corp-w2",
  "input_method": "pdf_upload",
  "user_confirmed": true,
  "fields": {
    "box1_wages": 185000.00,
    "box2_federal_withheld": 38500.00,
    "box3_ss_wages": 168600.00,
    "box4_ss_withheld": 10453.20,
    "box5_medicare_wages": 185000.00,
    "box6_medicare_withheld": 2682.50,
    "box7_ss_tips": 0,
    "box8_allocated_tips": 0,
    "box10_dependent_care": 0,
    "box11_nonqualified_plans": 0,
    "box12_codes": {
      "D": 23500.00,
      "W": 7300.00
    },
    "box13_statutory_employee": false,
    "box13_retirement_plan": true,
    "box13_third_party_sick_pay": false,
    "box14_other": null,
    "box15_state": "NJ",
    "box16_state_wages": 185000.00,
    "box17_state_withheld": 11200.00,
    "box18_local_wages": 0,
    "box19_local_withheld": 0,
    "box20_locality_name": null
  },
  "notes": "Box 12 code D is 401k contributions. Code W is HSA employer contributions."
}
```

### Example (K-1)

```json
{
  "schema_version": "1.0",
  "doc_id": "sunrise-k1-2025",
  "tax_year": 2025,
  "created_at": "2026-04-02T15:00:00Z",
  "updated_at": "2026-04-02T15:20:00Z",
  "form_type": "K-1",
  "institution": "Sunrise Ventures Fund II LP",
  "payer_ein": "55-1234567",
  "account_ref": "sunrise-ventures-k1",
  "input_method": "manual",
  "user_confirmed": true,
  "fields": {
    "entity_type": "partnership",
    "box1_ordinary_income": -2500.00,
    "box2_net_rental_income": 0,
    "box3_other_net_rental_income": 0,
    "box4_guaranteed_payments": 0,
    "box5_interest_income": 120.00,
    "box6a_ordinary_dividends": 340.00,
    "box6b_qualified_dividends": 280.00,
    "box7_royalties": 0,
    "box8_net_short_term_capital_gain": 0,
    "box9a_net_long_term_capital_gain": 5200.00,
    "box9b_collectibles_gain": 0,
    "box9c_unrecaptured_1250_gain": 0,
    "box10_net_section_1231_gain": 0,
    "box11_other_income": [],
    "box12_section_179_deduction": 0,
    "box13_other_deductions": [],
    "box14_self_employment_earnings": 0,
    "box15_credits": [],
    "box16_foreign_transactions": {
      "country": null,
      "foreign_tax_paid": 0
    },
    "box17_amt_items": [],
    "box18_tax_exempt_income": 0,
    "box19_distributions": 0,
    "box20_other_information": [
      {
        "code": "Z",
        "description": "Section 199A QBI",
        "amount": -2500.00
      }
    ],
    "box21_foreign_tax_credit": 0
  },
  "notes": "Angel investment. Ordinary loss from startup expenses. Long-term capital gain from portfolio company exit."
}
```

### Example (1098)

```json
{
  "schema_version": "1.0",
  "doc_id": "wells-fargo-1098-87smith-2025",
  "tax_year": 2025,
  "created_at": "2026-02-20T11:00:00Z",
  "updated_at": "2026-02-20T11:00:00Z",
  "form_type": "1098",
  "institution": "National Home Lending",
  "payer_ein": "41-0449260",
  "account_ref": "wells-fargo-87-smith",
  "input_method": "pdf_upload",
  "user_confirmed": true,
  "fields": {
    "box1_mortgage_interest": 12450.00,
    "box2_outstanding_principal": 215000.00,
    "box3_origination_date": "2018-05-15",
    "box4_refund_of_overpaid_interest": 0,
    "box5_mortgage_insurance_premiums": 0,
    "box6_points_paid": 0,
    "box7_property_address": "123 Main Street, Unit 2, Newark, NJ 07102",
    "box8_acquisition_date": "2018-05-15",
    "box9_number_of_properties": 1,
    "box10_other": null,
    "box11_property_tax": 6800.00
  },
  "notes": "Rental property mortgage. Interest goes to Schedule E, not Schedule A."
}
```

### Example (1099-INT)

```json
{
  "schema_version": "1.0",
  "doc_id": "amex-1099int-2025",
  "tax_year": 2025,
  "created_at": "2026-01-28T08:30:00Z",
  "updated_at": "2026-01-28T08:30:00Z",
  "form_type": "1099-INT",
  "institution": "Amex",
  "payer_ein": "27-0000000",
  "account_ref": "amex-hysa",
  "input_method": "manual",
  "user_confirmed": true,
  "fields": {
    "box1_interest_income": 1842.67,
    "box2_early_withdrawal_penalty": 0,
    "box3_us_savings_bond_interest": 0,
    "box4_federal_withheld": 0,
    "box5_investment_expenses": 0,
    "box6_foreign_tax_paid": 0,
    "box7_foreign_country": null,
    "box8_tax_exempt_interest": 0,
    "box9_specified_private_activity_bond": 0,
    "box10_market_discount": 0,
    "box11_bond_premium": 0,
    "box12_bond_premium_treasury": 0,
    "box13_bond_premium_tax_exempt": 0,
    "box14_tax_exempt_cusip": null,
    "box15_state": null,
    "box16_state_id": null,
    "box17_state_tax_withheld": 0
  },
  "notes": null
}
```

### Example (1099-NEC)

```json
{
  "schema_version": "1.0",
  "doc_id": "client-a-1099nec-2025",
  "tax_year": 2025,
  "created_at": "2026-01-30T12:00:00Z",
  "updated_at": "2026-01-30T12:00:00Z",
  "form_type": "1099-NEC",
  "institution": "Globex Industries",
  "payer_ein": "33-4455667",
  "account_ref": "johnson-consulting-1099nec",
  "input_method": "pdf_upload",
  "user_confirmed": true,
  "fields": {
    "box1_nonemployee_compensation": 42000.00,
    "box2_direct_sales": false,
    "box4_federal_withheld": 0,
    "box5_state_withheld": 0,
    "box6_state": null,
    "box7_state_id": null
  },
  "notes": null
}
```

### Example (1099-B — summary)

```json
{
  "schema_version": "1.0",
  "doc_id": "schwab-1099b-2025",
  "tax_year": 2025,
  "created_at": "2026-02-12T10:45:00Z",
  "updated_at": "2026-02-12T10:45:00Z",
  "form_type": "1099-B",
  "institution": "Charles Schwab",
  "payer_ein": "94-1234567",
  "account_ref": "schwab-brokerage",
  "input_method": "pdf_upload",
  "user_confirmed": true,
  "fields": {
    "summary": {
      "total_proceeds": 45230.50,
      "total_cost_basis": 38100.00,
      "total_gain_loss": 7130.50,
      "short_term_proceeds": 12500.00,
      "short_term_cost_basis": 11299.50,
      "short_term_gain_loss": 1200.50,
      "long_term_proceeds": 32730.50,
      "long_term_cost_basis": 26800.50,
      "long_term_gain_loss": 5930.00,
      "wash_sale_disallowed": 320.00,
      "federal_withheld": 0
    },
    "transactions": [
      {
        "description": "100 SH AAPL",
        "date_acquired": "2023-06-15",
        "date_sold": "2025-08-20",
        "proceeds": 18500.00,
        "cost_basis": 15200.00,
        "gain_loss": 3300.00,
        "term": "long_term",
        "wash_sale": false,
        "basis_reported_to_irs": true
      },
      {
        "description": "50 SH MSFT",
        "date_acquired": "2025-01-10",
        "date_sold": "2025-03-15",
        "proceeds": 12500.00,
        "cost_basis": 11299.50,
        "gain_loss": 1200.50,
        "term": "short_term",
        "wash_sale": false,
        "basis_reported_to_irs": true
      },
      {
        "description": "200 SH VTI",
        "date_acquired": "2024-02-01",
        "date_sold": "2025-11-10",
        "proceeds": 14230.50,
        "cost_basis": 11600.50,
        "gain_loss": 2630.00,
        "term": "long_term",
        "wash_sale": true,
        "wash_sale_disallowed": 320.00,
        "basis_reported_to_irs": true
      }
    ]
  },
  "notes": "Wash sale on VTI — sold and repurchased within 30 days. Disallowed loss added to replacement shares basis."
}
```

### Field Definitions (Common Fields)

These fields appear on every document file regardless of form type.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `schema_version` | string | **yes** | Always `"1.0"` |
| `doc_id` | string | **yes** | Unique identifier. Matches the `doc_id` in `accounts.json`. Also the filename (without `.json`). |
| `tax_year` | integer | **yes** | Tax year |
| `created_at` | string (ISO 8601) | **yes** | When the document was first parsed |
| `updated_at` | string (ISO 8601) | **yes** | When the document was last updated (e.g., user correction) |
| `form_type` | string (enum) | **yes** | Same enum as `accounts.json` expected_documents form_type |
| `institution` | string | **yes** | Issuing institution or payer name |
| `payer_ein` | string or null | **yes** | Payer's EIN as printed on the form. `null` if not available. |
| `account_ref` | string | **yes** | References `accounts[].id` in accounts.json |
| `input_method` | string (enum) | **yes** | How the data was entered. One of: `"pdf_upload"`, `"image_upload"`, `"manual"` |
| `user_confirmed` | boolean | **yes** | Whether the user has confirmed the extracted values are correct. Must be `true` before the data is used in reconciliation or packaging. |
| `fields` | object | **yes** | Form-specific extracted data. Structure varies by form type. See examples above. |
| `notes` | string or null | optional | Free-text notes about the document |

### Field Definitions (Form-Specific `fields` Object)

The `fields` object structure is determined by `form_type`. Key field naming conventions:

- **W-2:** Fields named `box{N}_{description}` matching IRS box numbers. `box12_codes` is an object keyed by letter code. `box13_*` are booleans.
- **1099-INT:** Fields named `box{N}_{description}`. All numeric except `box7_foreign_country` (string) and `box14_tax_exempt_cusip` (string).
- **1099-DIV:** Fields named `box{N}_{description}`. Box 8 (`foreign_country`) is a string.
- **1099-B:** Contains `summary` (aggregate numbers) and `transactions` (array of individual sales). Each transaction has `term` enum: `"short_term"` or `"long_term"`.
- **1099-NEC:** Fields named `box{N}_{description}`. `box2_direct_sales` is boolean.
- **1098:** Fields named `box{N}_{description}`. Box 3 and Box 8 are date strings.
- **K-1:** Fields named `box{N}_{description}`. Box 11, 13, 15, 17, and 20 are arrays of objects with `{code, description, amount}`. `box16_foreign_transactions` is a nested object.
- **1099-SA:** Key fields: `box1_gross_distributions`, `box2_earnings_on_excess`, `box3_capital_gain`, `box4_fmv_on_date_of_death`, `box5_hsa_msa_archer`.
- **5498-SA:** Key fields: `box1_employee_contributions`, `box2_employer_contributions`, `box3_total_contributions`, `box4_rollover`, `box5_fmv`.

### Notes

- Field names follow the pattern `box{N}_{description}` to maintain a clear mapping back to the IRS form. This makes it easy for CPAs to verify and for TXF export to map correctly.
- For 1099-B, the `transactions` array can be very large (hundreds of trades). The `summary` object provides aggregates for quick reference. The full transaction list is needed for TXF export and wash sale tracking.
- The `user_confirmed` flag is critical. The skill always presents extracted values to the user for confirmation before setting this to `true`. Unconfirmed documents are flagged during reconciliation.
- When a document is corrected, update the relevant fields, set `updated_at` to the current timestamp, and re-confirm with the user.
- Multiple documents of the same form type from different institutions each get their own file (e.g., `schwab-1099div-2025.json` and `fidelity-1099div-2025.json`).
- If a single institution issues a consolidated statement containing multiple form types (e.g., Schwab's consolidated 1099 includes 1099-B, 1099-DIV, and 1099-INT), create separate document files for each form type.