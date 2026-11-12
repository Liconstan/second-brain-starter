---
name: gifts-and-pledges-tab
description: Use when a new gift, grant or pledge reaches [YOUR_ORG], or for the monthly check, to keep the gifts and pledges tab of the bookkeeping worksheet current. Covers where new gifts turn up, the tax-form columns, the internal columns, filing the letter, and the memo back.
purpose: Every gift and pledge has one correct row in the gifts and pledges tab, with its letter filed, so the annual return and its donor schedule come out right.
helper_model: fable high
model_why: finance work that feeds a tax filing, where a wrong legal name or a missing row is costly
created_by: agent
created: [SYNC_START_DATE]
last_used: [SYNC_START_DATE]
source: the Memo starter kit
---

# Keeping the gifts and pledges tab current

## Goal

The gifts and pledges tab is the source for pledges receivable and for the gift lines of the annual return (in the US, Form 990 and its Schedule B). The outside bookkeeper reads from the tab; staff and agents keep it current. A wrong legal name or a missing row ends up in a tax filing.

## Settings

- The bookkeeping worksheet (a link to the Google Sheet): [BOOKKEEPING_SHEET]
- The tab name: [PLEDGES_TAB_NAME]
- The written rules for recording gifts (a link to the procedure document, if there is one): [GIFT_RECORDING_RULES]
- The outside bookkeeper or accounting firm that reads the tab: [BOOKKEEPER_NAME]
- The Drive folder for award letters, agreements and notices: [GRANT_LETTERS_FOLDER]
- Where money arrives (bank and card tools): [BANK_AND_CARD_TOOLS]
- Online giving platforms whose gifts come in through the bank feed and need no row here: [ONLINE_GIVING_PLATFORMS]

Fill in later. The column layout below is the default. If the sheet differs, change this table once and keep the steps.

| Columns | Kind | Content |
|---|---|---|
| B | tax form | grantor's exact legal name, checked by tax ID (EIN in the US) |
| C | tax form | grantor's contact or grants mailbox |
| D | tax form | grantor's own address of record |
| E to H | tax form | one exact value per cell: date, gross amount from the letter, restriction quoted from the letter or "none", and the other filing fields the tab asks for |
| I | internal | brand, platform, program or project name |
| J to P | bookkeeper's | received date and the bookkeeper's review and check columns. Never touch them |
| Q | internal | link to the filed letter, agreement or notice |
| R | internal | link to the thank-you or acknowledgement letter |
| S | internal | the person or fund behind a donor-advised fund (DAF) or platform gift |
| T | internal | status, fee-net amounts, pass-throughs, what to fill in later |
| U | internal | the recommending person's full name, email and mailing address |

## When to use

- A new gift, grant or pledge notice arrives: an award letter, a DAF grant notice, a withdrawal from a giving or regranting platform, a pledge made in Slack or email, an unexplained deposit.
- The monthly sweep.

## When not to use

- Gifts through [ONLINE_GIVING_PLATFORMS]: they come in through the bank feed and need no pledge row, unless the sheet's rules say otherwise.
- Anything in the bookkeeper's columns.
- Sending anything to the bookkeeper or a donor. This skill writes the tab and a memo, nothing else.

## Steps

Run the whole skill in one helper.

1. Read the sheet's own rules first: any Info or Read me tab, and the notes on row 1 of [PLEDGES_TAB_NAME] (header notes often explain the internal columns to the bookkeeper). They are the live rules; this skill is the summary. If the rules and this skill disagree, follow the sheet and say so in the memo.
2. Read [GIFT_RECORDING_RULES] if anything in the gift is unusual: a conditional grant, a pass-through, an in-kind gift, a platform gift.
3. Find new gifts and pledges. On each new gift, and once a month as a sweep, check:
   - Gmail: award letters, grant approval notices, DAF grant notices (Fidelity Charitable, DAFgiving360, Vanguard Charitable and the like).
   - Exports or disbursement reports from giving and regranting platforms, and the organization's balance on any platform that holds money for it.
   - Slack or other chat: pledges made in a thread or a direct message.
   - Deposits in [BANK_AND_CARD_TOOLS].
4. Compare against the tab. Every deposit or notice that is a gift and has no row gets one.
5. Fill the tax-form columns (B to H by default):
   - B is the grantor's exact legal name as registered with the tax authority, checked by tax ID (in the US: the IRS Tax Exempt Organization Search or the IRS Business Master File). Never a brand, platform, program or fund name. Example: DAFgiving360 is registered as Donor Advised Charitable Giving, Inc. A platform gift is recorded under the platform's legal name, not the platform's brand.
   - C is the grantor's grants mailbox.
   - D is the grantor's own address of record. For a DAF or platform gift, never the home address of the person who recommended the gift.
   - E to H: one exact value per cell. The gross amount from the letter. The restriction quoted from the letter, or "none". Never "same" or "as above".
6. Fill the internal columns: I for brand, platform and project names; S for the person or fund behind a DAF or platform gift; T for status, fee-net amounts, pass-throughs and what to fill in later; U for the recommending person's full name, email and mailing address. When you correct a row, never drop personal details: move them to U.
7. Pledge date:
   - An unconditional written promise is logged on the pledge date.
   - A conditional grant gets a blank pledge date and the reason in T until the condition is met.
   - Money held for the organization on a regranting platform is recorded when it is withdrawn, unless the sheet's rules say otherwise.
8. File the award letter, agreement or notice as a PDF in [GRANT_LETTERS_FOLDER] and paste the link in Q. Link the thank-you or acknowledgement letter in R. A DAF or platform gift gets no tax-receipt language in its acknowledgement: the donor got their receipt from the fund.
9. Leave the bookkeeper's columns alone.
10. Read the whole row back (Google Sheets get_values) and compare it cell by cell with the source document. Fix anything that differs.
11. Report to [YOUR_FIRST_NAME] in a memo:
    - For each new or changed row: the row number, each value written in the tax-form and internal columns, the source for the legal name and address (the tax ID and where it was checked), the Drive link, and anything left blank and why.
    - For the monthly sweep: every source checked, and every row added or changed, with a link on each line.

## Done when

- Every gift found in step 3 has a row, or a stated reason it needs none.
- Each row read back matches its source document cell by cell.
- The letter is filed in [GRANT_LETTERS_FOLDER] and linked in Q.
- The bookkeeper's columns are untouched.
- The memo lists each value, the tax ID source and the Drive link.

## Pitfalls

- A brand, platform or fund name in the legal name column instead of the registered legal name.
- A recommending individual's home address in the address column.
- "Same" or "as above" in a tax-form cell.
- Personal details dropped instead of moved to U.
- A net-of-fees amount in the amount column. The tax form wants the gross amount; the fee note goes in T.
- A conditional grant logged with a pledge date before its condition is met.
- Emailing [BOOKKEEPER_NAME] or the donor from this skill. Drafts for [YOUR_FIRST_NAME] only (CLAUDE.md, "Draft, do not send").
