# tax-prep

A Claude skill that acts as your tax season co-pilot. It walks you through the entire process of preparing materials for a CPA or self-filing via TurboTax: profiling your tax situation, discovering what documents you need, tracking what's arrived, reconciling everything, and producing a clean handoff package.

Works across multiple sessions as documents trickle in throughout tax season.

## Who It's For

Anyone with financial complexity beyond a single W-2:

- Rental property owners
- People with brokerage/investment accounts (1099-B, 1099-DIV, 1099-INT)
- Side business income (1099-NEC, Schedule C)
- K-1s from partnerships, S-corps, or angel investments
- Multi-state filers (NJ, NY, CA, CT guides included — more states welcome)
- People who use a CPA and want to hand off a clean, organized package
- Self-filers who use TurboTax and want to skip manual data entry

## Setup

### Claude Code

```bash
git clone https://github.com/ajaysurie/tax-prep.git
```

Then reference the skill from your project or add it to your skills directory:

```bash
# Option 1: Copy to your skills directory
cp -r tax-prep ~/.claude/skills/tax-prep

# Option 2: Reference directly
# Just invoke from the cloned directory
```

Start a conversation and say:

> "Let's start tax prep for 2025"

or invoke directly with `/tax-prep`.

### Claude Cowork (claude.ai Projects)

1. Create a new project in claude.ai
2. Upload all files from this repo to the project (drag and drop the folder, or upload individually)
3. Start a conversation and say:

> "Let's start tax prep for 2025"

The skill works fully in Cowork — it reads PDFs, parses CSVs, and tracks your progress across conversations. The only difference is that the CPA package outputs as CSV files instead of a multi-tab Excel file.

## How It Works

The skill guides you through five phases:

1. **Situation Interview** — Conversational profiling of your tax situation (filing status, income sources, properties, life changes). Pulls current-year IRS rates and limits.
2. **Account Discovery** — Maps your accounts to expected tax documents. Accepts a Monarch CSV export, manual entry, or prior-year carryforward.
3. **Document Collection** — Ongoing across tax season. Upload PDFs or enter numbers manually. The skill extracts key fields, matches them to your checklist, and tracks progress.
4. **Reconciliation** — Checks for completeness, compares against Monarch data, flags year-over-year anomalies, and catches commonly missed deductions.
5. **CPA Package / TurboTax Export** — Generates a structured handoff (CSV/Excel) or a TurboTax-importable .txf file.

Your progress is saved between sessions in `~/.tax-prep/{year}/`. Come back in two weeks when another K-1 arrives and pick up where you left off.

## Data Privacy

**All your personal tax data stays on your machine.** Nothing is committed to this repo.

- Your tax data lives in `~/.tax-prep/{year}/` (created at runtime, never committed)
- Uploaded PDFs, Monarch exports, and generated packages are never tracked by git
- The repo contains only generic reference materials, templates, and the skill workflow
- Test cases use synthetic data

## Updating

```bash
cd path/to/tax-prep
git pull
```

Reference files (tax rates, state guides) are updated annually. The `references/tax-data-sources.md` file contains current-year numbers and an annual update checklist.

### Keeping Tax Data Current

All tax numbers are sourced from official government publications (IRS.gov, FTB.ca.gov,
tax.ny.gov, nj.gov/treasury, portal.ct.gov/drs). The authoritative sources index at the
bottom of `references/tax-data-sources.md` lists every source URL used.

To update for a new tax year:

1. Check `references/tax-data-sources.md` — follow the "Annual Update Process" section
2. Update federal numbers from the IRS Revenue Procedure (published each November)
3. Update each state guide from the official state tax authority website
4. Update the federal numbers referenced in each state's comparison table
5. Update the "Last Verified" date at the bottom of `tax-data-sources.md`

## Contributing

The `references/` directory is the knowledge base — contributions welcome:

- **State tax guides** (`references/state-guides/`) — add your state
- **Document matrix updates** — new account types or form changes
- **Common gaps** — deductions people miss in your profession or situation
- **TXF field mappings** — corrections or additions for tax software import

## License

MIT
