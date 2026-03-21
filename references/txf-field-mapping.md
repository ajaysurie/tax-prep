# TXF Field Mapping — Tax Exchange Format Reference

TXF (Tax Exchange Format) is a text-based format used to import tax data into
TurboTax, H&R Block, and other tax software. This reference maps parsed document
fields to TXF record codes.

---

## TXF File Structure

A TXF file is plain text with this structure:

```
V042                          # Version line (042 = TXF version)
Atax-prep                     # Program identifier
D MM/DD/YYYY                  # Date generated
^                             # Record separator
TS                            # Start of tax data
record type line              # Record code
detail lines                  # Dollar amounts, descriptions
^                             # Record separator (between records)
...
```

### Record Format

Each record consists of:
1. **Type line:** `TNN` where NN is the record type code
2. **Detail lines:** one or more lines with amounts, descriptions, or codes
3. **Separator:** `^` on its own line

---

## Key TXF Record Codes

### Wages and Employment (W-2)

| Form/Box | TXF Code | Description | Format |
|----------|----------|-------------|--------|
| W-2 Box 1 | N521 | Wages, salaries, tips | `$.cc` amount on separate line |
| W-2 Box 2 | N522 | Federal income tax withheld | `$.cc` amount |
| W-2 Box 17 | N523 | State wages | Prefix with state code |
| W-2 Box 18 | N524 | State income tax withheld | Prefix with state code |

### Interest Income (1099-INT)

| Form/Box | TXF Code | Description |
|----------|----------|-------------|
| 1099-INT Box 1 | N287 | Interest income |
| 1099-INT Box 2 | N288 | Early withdrawal penalty |
| 1099-INT Box 3 | N289 | Interest on US savings bonds |
| 1099-INT Box 4 | N290 | Federal tax withheld |
| 1099-INT Box 8 | N291 | Tax-exempt interest |

### Dividend Income (1099-DIV)

| Form/Box | TXF Code | Description |
|----------|----------|-------------|
| 1099-DIV Box 1a | N292 | Total ordinary dividends |
| 1099-DIV Box 1b | N293 | Qualified dividends |
| 1099-DIV Box 2a | N294 | Total capital gain distributions |
| 1099-DIV Box 3 | N295 | Nontaxable distributions |
| 1099-DIV Box 7 | N296 | Foreign tax paid |

### Capital Gains/Losses (1099-B)

| Category | TXF Code | Description |
|----------|----------|-------------|
| Short-term proceeds | N673 | Total short-term proceeds |
| Short-term cost basis | N674 | Total short-term cost basis |
| Long-term proceeds | N675 | Total long-term proceeds |
| Long-term cost basis | N676 | Total long-term cost basis |
| Wash sale disallowed | N677 | Wash sale loss disallowed |

**Note:** TurboTax can import individual transaction details, but the summary
approach (total proceeds and basis for short-term and long-term) is more reliable
for import. The user should verify detailed transactions in TurboTax.

### Mortgage Interest (1098)

| Form/Box | TXF Code | Description |
|----------|----------|-------------|
| 1098 Box 1 | N297 | Mortgage interest received |
| 1098 Box 2 | N298 | Points paid on purchase |
| 1098 Box 5 | N299 | Mortgage insurance premiums |

### Self-Employment Income (1099-NEC)

| Form/Box | TXF Code | Description |
|----------|----------|-------------|
| 1099-NEC Box 1 | N582 | Nonemployee compensation |

### Rental Income (Schedule E)

| Line | TXF Code | Description |
|------|----------|-------------|
| Line 3 | N600 | Rents received |
| Line 5 | N601 | Advertising |
| Line 6 | N602 | Auto and travel |
| Line 7 | N603 | Cleaning and maintenance |
| Line 8 | N604 | Commissions |
| Line 9 | N605 | Insurance |
| Line 10 | N606 | Legal and professional |
| Line 11 | N607 | Management fees |
| Line 12 | N608 | Mortgage interest |
| Line 13 | N609 | Other interest |
| Line 14 | N610 | Repairs |
| Line 15 | N611 | Supplies |
| Line 16 | N612 | Taxes |
| Line 17 | N613 | Utilities |
| Line 18 | N614 | Depreciation |
| Line 19 | N615 | Other |

**Each rental property is a separate set of records** with the property address
as the description line.

### HSA (1099-SA / 5498-SA)

| Form/Box | TXF Code | Description |
|----------|----------|-------------|
| 5498-SA Box 2 | N680 | Total HSA contributions |
| 1099-SA Box 1 | N681 | HSA distributions |

### Other Common Codes

| Item | TXF Code | Description |
|------|----------|-------------|
| State income tax refund | N300 | 1099-G state refund |
| Estimated tax — federal | N310 | Per quarter |
| Estimated tax — state | N311 | Per quarter, with state code |
| Charitable — cash | N312 | Cash contributions |
| Student loan interest | N313 | 1098-E |
| Child care expenses | N314 | Per provider |

---

## Generating a TXF File

When generating the TXF file:

1. Write the header:
```
V042
Atax-prep
D 03/15/2026
^
```

2. For each parsed document, look up the TXF code in the mapping above.

3. Write each record:
```
TS
N{code}
{description — payer/institution name}
${amount}
^
```

4. For records with multiple amounts (like W-2), write the primary amount first,
then supplementary fields on following lines.

---

## Limitations

- **Not all line items have TXF codes.** Some items require manual entry in TurboTax.
  K-1 pass-through items, in particular, are complex and may not import cleanly.
- **TXF is a legacy format.** TurboTax supports it but doesn't document it well.
  Always instruct the user to review all imported data.
- **Corrected statements:** If the user received a corrected 1099, ensure the TXF
  file uses the corrected amounts, not the original.
- **State-specific items** may not have TXF codes. Include them in the CPA package
  CSV files instead.

---

## Import Instructions

### TurboTax
1. Open TurboTax
2. Go to File → Import → From TXF File
3. Select the generated `.txf` file
4. Review each imported item — TurboTax will show what was imported
5. Continue with the normal TurboTax interview to fill in anything not imported

### H&R Block
H&R Block's import capability varies by year and edition. Generally:
1. Open H&R Block
2. Look for Import → Other Tax Software or Import → TXF File
3. Select the file and review

### FreeTaxUSA
FreeTaxUSA supports TXF import in some editions:
1. Go to Import section
2. Select "Import from TXF file"
3. Upload and review

**Always include this disclaimer in the output:**
"This TXF file was generated from your parsed tax documents. Review ALL imported
data in your tax software before filing. Some items may require manual entry or
adjustment. This tool organizes data — it does not provide tax advice."
