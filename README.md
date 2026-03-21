# tax-prep

A Claude Code skill that acts as your tax season co-pilot. It walks you through
organizing everything your CPA needs — or exports a TurboTax-importable file if
you self-file.

Works across multiple sessions as documents trickle in throughout tax season.
Your progress is saved between sessions in `~/.tax-prep/{year}/`.

## Who It's For

Anyone with financial complexity beyond a single W-2:

- Rental property owners (Schedule E)
- Brokerage/investment accounts (1099-B, 1099-DIV, 1099-INT)
- Side business income (1099-NEC, Schedule C)
- K-1s from partnerships, S-corps, or angel investments
- Multi-state filers (NJ, NY, CA, CT guides included — more states welcome)
- People who use a CPA and want to hand off a clean, organized package
- Self-filers who use TurboTax and want to skip manual data entry

## Quick Start

### Option A: Claude Code (CLI)

**Install:**

```bash
git clone https://github.com/ajaysurie/tax-prep.git ~/.claude/skills/tax-prep
```

That's it. The skill is now available in Claude Code.

**Use it:**

Open Claude Code and say any of these:

```
Let's start tax prep for 2025
I need to organize my taxes
Help me get ready for my CPA
I just got my 1099-DIV from Fidelity — here it is
What documents am I still missing?
```

Claude will detect the skill automatically and walk you through the workflow.

### Option B: Claude Projects (claude.ai)

1. Go to [claude.ai](https://claude.ai) and create a new Project
2. In the project knowledge, upload these files from this repo:
   - `SKILL.md` (the core workflow — **this is the most important file**)
   - The entire `references/` folder (tax rates, document guides, schemas)
3. Start a conversation:

```
Let's start tax prep for 2025
```

Everything works in Projects except: CPA package outputs as CSV (not Excel),
and tax rate verification uses the reference file numbers directly (no web search).

### Option C: Just Read It

Don't use Claude Code or Projects? The `references/` folder is still useful on its own:

- `references/document-matrix.md` — what documents you need based on your accounts
- `references/common-gaps.md` — deductions people commonly miss
- `references/tax-data-sources.md` — current 2025 federal and state tax numbers
- `references/state-guides/` — state-specific rules for NJ, NY, CA, CT
- `references/cpa-handoff-format.md` — how to organize your CPA package

## The Workflow

The skill guides you through five phases, one conversation at a time:

```
Phase 1                Phase 2              Phase 3
SITUATION     --->     ACCOUNT      --->    DOCUMENT
INTERVIEW              DISCOVERY            COLLECTION
                                            (ongoing — upload
                                             docs as they arrive)
    |                      |                     |
    v                      v                     v
 profile.json         accounts.json         documents/*.json


Phase 4                Phase 5
RECONCILIATION  --->   CPA PACKAGE or
                       TURBOTAX EXPORT
    |                      |
    v                      v
 reconciliation.json   CSV files + .txf
```

**Phase 1: Situation Interview** — Claude asks about your filing status, income
sources, properties, investments, life changes. One question at a time, explains
why each matters. Pulls current IRS rates and limits. Saves `profile.json`.

**Phase 2: Account Discovery** — You list your financial accounts (or upload a
Monarch CSV export). Claude maps each account to the tax documents you should
expect (e.g., Fidelity brokerage → 1099-B, 1099-DIV, 1099-INT). Saves `accounts.json`.

**Phase 3: Document Collection** — The longest phase. As documents arrive (January
through March), upload the PDF or enter numbers manually. Claude extracts key fields,
shows you what it found for confirmation, matches it to your checklist, and reports
progress. "You have 14 of 22 documents. Still waiting on: K-1 from Fund X, 1099-B
from Schwab..."

**Phase 4: Reconciliation** — Once everything (or almost everything) is in, Claude
checks: Are the numbers consistent? Does your Monarch data match your 1099s? Did you
forget estimated tax payments? Are there deductions you're missing based on your
profile? Flags anything suspicious.

**Phase 5: CPA Package / TurboTax Export** — Generates the final output:
- **For CPA users:** A set of organized CSV files covering income, deductions,
  rental properties, K-1s, state-specific items, and open questions
- **For TurboTax users:** A `.txf` file you can import directly, plus instructions

### Returning Next Year

```
Let's do tax prep for 2026
```

Claude loads your 2025 profile and asks "what changed?" instead of re-interviewing
from scratch. Sold a property? New job? Had a baby? Just tell it the delta.

## What's in This Repo

```
tax-prep/
├── SKILL.md                          # Core workflow (this is the brain)
├── CLAUDE.md                         # Project config for Claude Code
├── README.md                         # You are here
│
├── references/
│   ├── tax-data-sources.md           # 2025 federal numbers + authoritative source URLs
│   ├── document-matrix.md            # Account type → expected tax forms
│   ├── situation-questions.md        # Interview question bank
│   ├── schemas.md                    # JSON schemas for all state files
│   ├── schedule-e-guide.md           # Rental property (Schedule E) reference
│   ├── common-gaps.md                # Commonly missed deductions by profile
│   ├── k1-guide.md                   # K-1 types, key boxes, where they flow
│   ├── cpa-handoff-format.md         # CPA package specification
│   ├── txf-field-mapping.md          # TurboTax import format mapping
│   └── state-guides/
│       ├── NJ.md                     # New Jersey
│       ├── NY.md                     # New York
│       ├── CA.md                     # California
│       └── CT.md                     # Connecticut
│
├── evals/
│   └── evals.json                    # 5 synthetic test scenarios
│
└── state/                            # Gitignored — runtime only
    └── .gitkeep
```

## Data Privacy

**All your personal tax data stays on your machine.** Nothing is committed to this repo.

- Your tax data lives in `~/.tax-prep/{year}/` (created at runtime, never committed)
- Uploaded PDFs, Monarch exports, and generated packages are never tracked by git
- The repo contains only generic reference materials and the skill workflow
- Test cases use entirely synthetic data

## Updating

```bash
cd ~/.claude/skills/tax-prep
git pull
```

Tax rates and state guides are updated annually. Check `references/tax-data-sources.md`
for the "Last Verified" date to see when numbers were last confirmed against official
sources.

### Keeping Tax Data Current

All numbers are sourced from official government publications. The authoritative sources
index at the bottom of `references/tax-data-sources.md` lists every URL used:

| Jurisdiction | Authority | URL |
|-------------|-----------|-----|
| Federal | IRS | https://www.irs.gov/ |
| New Jersey | Division of Taxation | https://www.nj.gov/treasury/taxation/ |
| New York | Dept. of Taxation and Finance | https://www.tax.ny.gov/ |
| California | Franchise Tax Board | https://www.ftb.ca.gov/ |
| Connecticut | Dept. of Revenue Services | https://portal.ct.gov/drs |

To update for a new tax year, follow the "Annual Update Process" checklist in
`references/tax-data-sources.md`.

## Contributing

The `references/` directory is the knowledge base — contributions welcome:

- **State tax guides** (`references/state-guides/`) — add your state! Use an existing
  guide as a template. Cover: brackets, estimated payments, state-specific credits,
  federal differences table, pass-through entity tax, filing requirements.
- **Document matrix updates** — new account types or form changes
- **Common gaps** — deductions people miss in your profession or situation
- **TXF field mappings** — corrections or additions for tax software import

## Disclaimer

This tool organizes your tax documents and data. It does not provide tax advice.
Always review output with a qualified tax professional before filing.

## License

MIT
