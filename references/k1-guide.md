# K-1 Guide — Pass-Through Entity Income

K-1s report your share of income, deductions, and credits from partnerships,
S-corporations, estates, and trusts. They're among the most complex tax documents
and are frequently the last to arrive.

---

## K-1 Types

| Form | Entity Type | Filed By | Due Date | Extended Due Date |
|------|------------|----------|----------|-------------------|
| Schedule K-1 (Form 1065) | Partnership | Partnership | March 15 | September 15 |
| Schedule K-1 (Form 1120-S) | S-Corporation | S-Corp | March 15 | September 15 |
| Schedule K-1 (Form 1041) | Estate or Trust | Fiduciary | April 15 | September 30 |

**Timing warning:** K-1s are due March 15 for partnerships and S-corps, but entities
frequently file extensions. It is common to receive K-1s in August or September.
If the user is waiting on K-1s, they may need to file a personal extension (Form 4868).

---

## Common K-1 Sources

- **Oil and gas MLPs** (e.g., Enterprise Products Partners) — Partnership K-1
- **Real estate syndications** — Partnership K-1
- **Angel investment funds** — Partnership K-1
- **Venture capital fund investments** — Partnership K-1
- **S-corporation ownership** — S-Corp K-1
- **Family trusts** — Estate/Trust K-1
- **Hedge fund investments** — Partnership K-1

---

## Key Boxes and Where They Flow

### Partnership K-1 (Form 1065)

| Box | Description | Flows To | Notes |
|-----|------------|----------|-------|
| 1 | Ordinary business income/loss | Schedule E Part II | Active vs passive matters for loss limitations |
| 2 | Net rental real estate income/loss | Schedule E Part II | Subject to passive activity rules |
| 3 | Other net rental income/loss | Schedule E Part II | Non-real estate rental |
| 4a | Guaranteed payments for services | Schedule E Part II | Also subject to self-employment tax |
| 4b | Guaranteed payments for capital | Schedule E Part II | Not subject to SE tax |
| 5 | Interest income | Schedule B | Taxed as ordinary income |
| 6a | Ordinary dividends | Schedule B | |
| 6b | Qualified dividends | Schedule B | Taxed at preferential rates |
| 7 | Royalties | Schedule E Part I | |
| 8 | Net short-term capital gain/loss | Schedule D / Form 8949 | Taxed as ordinary income rates |
| 9a | Net long-term capital gain/loss | Schedule D / Form 8949 | Preferential rates |
| 9b | Collectibles (28%) gain/loss | Schedule D | Higher rate for collectibles |
| 9c | Unrecaptured section 1250 gain | Schedule D | 25% rate (depreciation recapture) |
| 10 | Net section 1231 gain/loss | Form 4797 | Can be ordinary or capital depending on history |
| 11 | Other income/loss | Various | Code A = other portfolio income, Code F = other income |
| 12 | Section 179 deduction | Form 4562 | |
| 13 | Other deductions | Various | Code A = cash charitable, Code W = other deductions |
| 14 | Self-employment earnings/loss | Schedule SE | Only for general partners / LLC members |
| 15 | Credits | Various | Code A = LIHC, Code P = other credits |
| 16 | Foreign transactions | Form 1116 | Foreign tax credit items |
| 17 | Alternative minimum tax items | Form 6251 | AMT adjustments |
| 18 | Tax-exempt income | Not taxable | But may affect basis |
| 19 | Distributions | Not income | Reduces basis; excess over basis = capital gain |
| 20 | Other information | Various | **Code Z = Section 199A QBI** (very common and important) |

### S-Corp K-1 (Form 1120-S)

Similar structure to partnership K-1 but with some differences:
- No self-employment tax on ordinary income (Box 1)
- Shareholder must take "reasonable compensation" as W-2 wages
- Box 16d: items affecting shareholder basis
- Box 17: most commonly Code V for Section 199A QBI

### Estate/Trust K-1 (Form 1041)

- Box 1: Interest income
- Box 2a: Ordinary dividends
- Box 2b: Qualified dividends
- Box 3: Net short-term capital gain
- Box 4a: Net long-term capital gain
- Box 5: Other portfolio income
- Box 6: Ordinary business income
- Box 9: Directly apportioned deductions
- Box 14: Other information (Code I = Section 199A QBI)

---

## Section 199A / QBI Deduction

The Qualified Business Income (QBI) deduction allows a deduction of up to 20% of
qualified business income from pass-through entities. It's reported on K-1s in:
- Partnership: Box 20, Code Z
- S-Corp: Box 17, Code V
- Trust: Box 14, Code I

This is one of the most valuable K-1 line items. The QBI deduction is subject to
income limitations and specified service trade/business (SSTB) rules.

**How to handle:** Extract the Section 199A information and include it in the CPA package.
The CPA handles the complex QBI calculation.

---

## Basis Tracking

Your basis in a partnership or S-corp determines:
1. How much loss you can deduct (can't deduct losses exceeding basis)
2. Whether distributions are taxable (distributions exceeding basis = capital gain)

**Ask the user:** "Do you know your current basis in {entity}? Your CPA should track this."

Basis increases with: income allocated, additional contributions
Basis decreases with: losses allocated, distributions received

---

## Passive Activity Rules

Most K-1 income/loss is **passive** for limited partners and S-corp shareholders who
don't materially participate. Passive losses can only offset passive income (not wages
or portfolio income). Unused passive losses carry forward.

**Exception:** Real estate professionals who spend 750+ hours in real estate activities
can treat rental losses as non-passive.

**Ask the user:** "Do you actively participate in the management of {entity}, or are you
a passive investor?" This affects whether losses can be used currently.

---

## MLP-Specific Notes (Master Limited Partnerships)

MLPs like Enterprise Products Partners have additional complexity:
- Distributions are largely **return of capital** (reduce basis, not currently taxable)
- When basis reaches zero, distributions become capital gains
- Sale of MLP units triggers ordinary income recapture on accumulated Section 751 items
- State tax filing may be required in states where the MLP operates

The MLP K-1 is often the most complex K-1 a typical investor receives.
Include all boxes in the CPA package — don't try to simplify it.
