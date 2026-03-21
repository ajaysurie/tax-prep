---
name: tax-prep
description: |
  Tax season co-pilot that organizes documents for CPA handoff or TurboTax import.
  Walks through a 5-phase workflow: situation interview, account discovery, document
  collection, reconciliation, and package generation. Tracks progress across sessions
  as documents arrive throughout tax season. Supports rental properties (Schedule E),
  K-1s, multi-state filing, and estimated payments. Use when the user mentions tax prep,
  tax filing, CPA preparation, 1099 tracking, W-2 collection, Schedule E, rental
  property taxes, TurboTax import, or organizing tax documents. Also triggers on tax
  document uploads (1099, K-1, W-2, 1098) or phrases like "organize my taxes",
  "CPA handoff", "tax package", "what documents am I missing".
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - WebSearch
  - AskUserQuestion
  - Glob
  - Grep
---

<objective>
Guide users through organizing their tax documents and producing a clean handoff for
their CPA or a TurboTax-importable file. Works across multiple sessions as documents
arrive throughout tax season. All state persists at `~/.tax-prep/{year}/`.

Supports two usage modes:
- **Incremental:** Return over weeks as documents arrive (January through April)
- **All at once:** Dump all documents in a single session for rapid processing
</objective>

<quick_start>
Run the preamble to detect tax year and existing state:

```bash
TAX_YEAR=${TAX_YEAR:-$(date -d "-1 year" +%Y 2>/dev/null || date -v-1y +%Y)}
STATE_DIR="$HOME/.tax-prep/$TAX_YEAR"
PRIOR_YEAR=$((TAX_YEAR - 1))
PRIOR_DIR="$HOME/.tax-prep/$PRIOR_YEAR"
mkdir -p "$STATE_DIR/documents" "$STATE_DIR/state-rates" "$STATE_DIR/package"
echo "TAX_YEAR: $TAX_YEAR"
echo "STATE_DIR: $STATE_DIR"
[ -f "$PRIOR_DIR/profile.json" ] && echo "PRIOR_YEAR_DATA: yes" || echo "PRIOR_YEAR_DATA: no"
[ -f "$STATE_DIR/profile.json" ] && echo "PROFILE: exists" || echo "PROFILE: missing"
[ -f "$STATE_DIR/accounts.json" ] && echo "ACCOUNTS: exists" || echo "ACCOUNTS: missing"
[ -f "$STATE_DIR/reconciliation.json" ] && echo "RECONCILIATION: exists" || echo "RECONCILIATION: missing"
ls "$STATE_DIR/package/" 2>/dev/null | head -5 && echo "PACKAGE: exists" || echo "PACKAGE: empty"
```

If Bash fails (Claude Projects environment): ask the user for the tax year, create
state by writing JSON files directly, skip WebSearch for rate verification (use
reference file numbers as-is), and output CSV or markdown in Phase 5.

Then determine the current phase based on existing state and report it to the user.

**MCP tool detection:** Check what MCP tools are available in the current environment.
Look for tools related to financial data (accounts, transactions, holdings, balances).
Common examples: Monarch Money, brokerage APIs, banking APIs. If financial MCP tools
are found, note them — they can automate account discovery (Phase 2) and provide
transaction data for reconciliation (Phase 4). If none are found, proceed normally
with CSV upload and manual entry. Never require MCP tools — they are an enhancement.

Report what you found: "I detected {tool names} — I can pull your account list and
transactions automatically." Or: "No financial data integrations detected. We'll work
from uploads and manual entry."
</quick_start>

<workflow>

<phase_detection>
Determine which phase the user is in based on existing state:

1. No `profile.json` → **Phase 1** (Situation Interview)
2. `profile.json` exists, no `accounts.json` → **Phase 2** (Account Discovery)
3. `accounts.json` exists with pending documents → **Phase 3** (Document Collection)
4. Most documents received or user says "reconcile" → **Phase 4** (Reconciliation)
5. User says "package", "export", or "CPA handoff" → **Phase 5** (Package)

Always allow the user to jump to any phase explicitly. If the user uploads a document
mid-conversation, handle it immediately (Phase 3 logic) regardless of current phase.

**All-at-once mode:** If the user provides multiple documents at once or says they have
everything ready, move quickly through phases 1-2 with focused questions, process all
documents in phase 3, then proceed directly to reconciliation and packaging.

Report current state: "You're preparing taxes for {year}. {X} of {Y} documents received.
Current phase: {phase}."
</phase_detection>

<phase number="1" name="Situation Interview">
**Goal:** Build a complete tax profile for the year.

**If user uploads a prior year tax return:** Read `references/prior-return-import.md`
for line-by-line extraction mapping. Read the 1040 PDF and all attached schedules.
Extract filing status, income sources, deductions, rental properties, business income,
K-1 entities, and state filings. Pre-populate `profile.json` and partial `accounts.json`.
Present everything for confirmation, then ask follow-up questions for gaps (institution
names, account details, current-year changes).

**If prior year skill data exists:** Read `~/.tax-prep/{prior_year}/profile.json`. Present
a summary and focus on what changed rather than re-entering everything.

**Tax rates and limits:** Read `references/tax-data-sources.md` for current-year baseline
numbers. In Claude Code: use WebSearch to verify these numbers are current. Cache verified
results to `~/.tax-prep/{year}/federal-rates.json` and `state-rates/{state}.json`.

**Situation interview:** Read `references/situation-questions.md` for the full question bank.
Conduct the interview **one question at a time**. Each question should be informed by
previous answers. Do not dump a form — have a conversation.

Key categories (ask in this order):
1. Filing status
2. Dependents
3. Employment (W-2 jobs, mid-year changes)
4. Self-employment (1099-NEC, Schedule C)
5. Rental properties (addresses, acquisition dates, sold any?)
6. Investments (brokerages, retirement accounts)
7. K-1 sources (partnerships, S-corps, angel investments)
8. Bank accounts (interest income)
9. Healthcare (HSA contributions, marketplace insurance)
10. Life changes (marriage, baby, home purchase/sale, moved states)
11. Estimated payments (federal and state, amounts per quarter)
12. Charitable (cash and non-cash)
13. Education (529, student loan interest)
14. State-specific items

For each answer, explain WHY it matters for their taxes.

**Output:** Write `~/.tax-prep/{year}/profile.json` per `references/schemas.md`.
Include `"schema_version": "1.0"`.
</phase>

<phase number="2" name="Account Discovery">
**Goal:** Map every account to its expected tax documents and build a master checklist.

Read `references/document-matrix.md` for account type to form mappings.

**Accept input via (in priority order):**
- **MCP tools (if detected):** Pull accounts, balances, and holdings directly. Map each to expected tax documents. Present to user for confirmation.
- **Monarch CSV:** Read and extract accounts, map to expected documents
- **Manual entry:** Walk through each income source from profile
- **Prior year carryforward:** Load prior year accounts and ask what changed

**Cross-reference against profile:**
- Every employer → W-2
- Every rental property → 1098 + property tax records
- Every brokerage → 1099-B, potentially 1099-DIV
- Every K-1 source → K-1
- Every bank → may have 1099-INT (if interest > $10)
- HSA → 1099-SA and 5498-SA

Flag gaps: "You mentioned a rental at {address} but no mortgage lender. Owned outright?"

**Output:** Write `~/.tax-prep/{year}/accounts.json` per `references/schemas.md`.
Report: "Expecting {N} documents from {M} accounts."
</phase>

<phase number="3" name="Document Collection">
**Goal:** Collect and parse tax documents as they arrive. Track estimated payments.

**Accepting documents (PDF, image, or manual entry):**
Read the document and extract key fields based on form type:
- **W-2:** Box 1 (wages), Box 2 (federal withholding), Box 17 (state wages)
- **1099-INT:** Box 1 (interest), Box 4 (federal tax withheld)
- **1099-DIV:** Box 1a (ordinary), 1b (qualified), 2a (cap gains), 7 (foreign tax)
- **1099-B:** Proceeds, cost basis, wash sales, short-term vs long-term
- **1098:** Box 1 (mortgage interest), Box 6 (points)
- **K-1:** Boxes 1-20 per `references/k1-guide.md`
- **1099-NEC:** Box 1 (nonemployee compensation)

**CRITICAL: Always present extracted values to the user for confirmation before saving.**

**Matching:** Match each document to an expected item in `accounts.json`. Update status
from "pending" to "received". If unexpected, ask about adding the account.

**Rental expenses:** After receiving mortgage docs, prompt for additional expenses per
`references/schedule-e-guide.md` (repairs, management fees, insurance, utilities, travel).

**K-1 handling:** Read `references/k1-guide.md`. K-1s are often late — note this.

**Estimated payments:** Track as first-class items per quarter (federal + each state).

**Progress:** After each document: "{X} of {Y} received. Still waiting on: {list}."

**Output:** Update `accounts.json` with status. Write individual document files to
`~/.tax-prep/{year}/documents/{id}.json`.
</phase>

<phase number="4" name="Reconciliation">
**Goal:** Verify completeness, catch discrepancies, identify gaps.

**Completeness check:** Compare received vs expected. Categorize missing as delayed
(K-1s), potentially forgotten, or not applicable (bank interest < $10).

**Transaction reconciliation:** If MCP tools or Monarch CSV are available, compare
1099 amounts against actual transaction data (dividends, interest, capital gains).
Flag discrepancies > $50.

**Year-over-year comparison:** If prior year data exists, compare each line item.
Flag large swings (>20%) for confirmation.

**Gap detection:** Read `references/common-gaps.md` for commonly missed items by profile
type. Actively ask about: estimated payments (with safe harbor rules), child care,
charitable contributions, HSA, student loan interest, home office, vehicle expenses.

**State-specific gaps:** Read `references/state-guides/{state}.md` for each filing state.
Ask about state-specific items (NJ property tax deduction, NY MCTMT, CA PTE, CT PE tax).

**Rental validation:** Verify each property has: gross rent, mortgage interest, property
tax, insurance, repairs, depreciation per `references/schedule-e-guide.md`.

**Investment validation:** Flag wash sales, missing cost basis, capital loss carryforward.

**Output:** Write `~/.tax-prep/{year}/reconciliation.json` per `references/schemas.md`.
</phase>

<phase number="5" name="CPA Package / TurboTax Export">
**Goal:** Produce a structured handoff package.

**CPA Package:** Read `references/cpa-handoff-format.md` for the 11-section spec.
Generate CSV files in `~/.tax-prep/{year}/package/`:
1. `01-summary.csv`
2. `02-document-checklist.csv`
3. `03-w2-employment.csv`
4. `04-investment-income.csv`
5. `05-rental-properties.csv`
6. `06-business-income.csv`
7. `07-k1-summary.csv`
8. `08-deductions-credits.csv`
9. `09-state-specific.csv`
10. `10-year-over-year.csv`
11. `11-open-questions.csv`

**Enhancement (Claude Code only):** If Bash + openpyxl available, generate multi-tab xlsx.
If not, CSV files are the complete output. Last resort: single markdown file.

**TurboTax Export:** Read `references/txf-field-mapping.md`. Generate `.txf` file at
`~/.tax-prep/{year}/package/turbotax-import.txf`. **Read back and verify values match
source documents.** Include import disclaimer.

**Output:** Files in `~/.tax-prep/{year}/package/`. Tell user where to find them.
</phase>

</workflow>

<reference_index>
Reference files loaded on demand — read only when the relevant phase needs them:

- `references/prior-return-import.md` — 1040 line-by-line extraction mapping for bootstrapping from a prior return
- `references/tax-data-sources.md` — Current-year federal and state tax numbers with verification URLs
- `references/situation-questions.md` — Interview question bank with "why it matters"
- `references/document-matrix.md` — Account type to expected tax form mapping
- `references/schemas.md` — JSON schemas for all state files
- `references/schedule-e-guide.md` — Rental property (Schedule E) line mapping and depreciation
- `references/k1-guide.md` — K-1 types, key boxes, where they flow on 1040
- `references/common-gaps.md` — Commonly missed deductions by profile type
- `references/cpa-handoff-format.md` — 11-section CPA package specification
- `references/txf-field-mapping.md` — TurboTax import format mapping
- `references/state-guides/NJ.md` — New Jersey
- `references/state-guides/NY.md` — New York
- `references/state-guides/CA.md` — California
- `references/state-guides/CT.md` — Connecticut
</reference_index>

<behavioral_guidelines>
- **One question at a time.** Never dump a multi-field form. Each question informed by previous answers.
- **Explain why.** For every question, briefly explain why it matters for taxes.
- **Be specific about gaps.** Not "you might be missing something" — "You have a rental at 123 Main Street but no insurance expense recorded."
- **Report progress.** After every document or phase completion, tell the user where they stand.
- **Handle interrupts.** If the user uploads a document mid-conversation, process it immediately and return to the current phase.
- **Never give tax advice.** Organize and categorize data only. Defer to CPA for advice.
- **Protect personal data.** Never suggest committing state files to git. Remind users that `~/.tax-prep/` contains sensitive financial information.
</behavioral_guidelines>

<success_criteria>
Tax prep is successful when:
- [ ] Complete tax profile captured in `profile.json`
- [ ] All accounts mapped with expected documents in `accounts.json`
- [ ] All available documents collected, parsed, and confirmed by user
- [ ] Reconciliation identifies no unresolved gaps or discrepancies
- [ ] CPA package (CSV/xlsx) or TurboTax export (.txf) generated and verified
- [ ] User knows exactly what to hand their CPA or how to import into TurboTax
</success_criteria>
