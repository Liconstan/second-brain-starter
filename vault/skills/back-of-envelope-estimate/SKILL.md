---
name: back-of-envelope-estimate
description: Back-of-the-envelope cost-effectiveness estimate (BOTEC) for a grant application or funding request, as a spreadsheet-ready CSV with conservative, best guess and optimistic scenarios. Use when asked to estimate, score or sanity-check the cost-effectiveness of an application.
---

## Settings

- The field the estimates are for: [BOTEC_FIELD]
- The outcome the estimate counts, per objective and in total: [BOTEC_OUTCOME_UNIT]
- A sheet of standard estimates the reviewers share (benchmarks, typical sizes, past conversion rates): [BOTEC_REFERENCE_SHEET]

Fill in later. Until they are filled: ask once for the field and the outcome unit. With no reference sheet, every number not taken from the application is "Speculative".

The prompt below is the method. The row labels in it use the outcome unit "Students Helped" as an example; use the outcome unit from Settings instead.

```
ROLE: Skeptical cost-effectiveness analyst for [BOTEC_FIELD]. Favor conservative assumptions.

STEP 1 (First response - do NOT generate the BOTEC yet):

Classify the application, identify ALL distinct program objectives, propose assumptions. Wait for user approval before continuing. CRITICAL: the reviewer has NO data or insights beyond those in the application, so do NOT ask them for such. They have NO more insight into the data provided than you do.

STEP 2 - GENERATE BOTEC:

═══════════════════════════════════════════════════
OUTPUT FORMAT: READ CAREFULLY BEFORE GENERATING
═══════════════════════════════════════════════════

You MUST output the CSV inside a fenced code block so the user can copy it easily. Use triple backticks with the "csv" language tag:

```csv
(rows go here)
```

DELIMITER: Use SEMICOLONS (;) as the column separator. Every row has exactly 8 columns, so exactly 7 semicolons.

LINE BREAKS: Each row MUST be on its own line. Do NOT put multiple rows on one line. Do NOT join rows with literal "\n" text. Use actual newlines.

FORMULAS: For all calculated rows (for example "Students Helped", "Total Students Helped", "Students Helped per $1,000", "Total Cost"), do NOT output static numbers in the Conservative / Best Guess / Optimistic columns. Instead, output the actual Excel or Google Sheets formula starting with =.

Assume the table starts at cell A1. Column B is Conservative, C is Best Guess, D is Optimistic.

Write input values (percentages) as decimals (for example 0.05, not 5%) so the formulas calculate correctly as soon as they are pasted.

═══════════════════════════════════════════════════
ROW TYPES: CRITICAL DISTINCTION
═══════════════════════════════════════════════════

There are THREE types of rows. Handle each differently:

1. HEADER ROWS (for example "[OBJECTIVE 1: Tutoring in partner schools]")
   - Put the header text in column A ONLY.
   - Leave columns B, C, D completely EMPTY (no values, no formulas, no zeros).
   - Leave columns E-H empty too.

2. INPUT ROWS (for example "Schools Reached", "Total Funding Requested")
   - Put the label in column A and static numeric values in B, C, D.
   - Fill columns E-H as specified below.

3. CALCULATED ROWS (for example "Students Helped", "Students Helped per $1,000", "Order of Magnitude Score")
   - Put the label in column A.
   - Put FORMULAS (starting with =) in columns B, C, D.
   - CRITICAL: Every formula MUST be wrapped in IFERROR. Example: =IFERROR(B7*B8*B9, 0)
   - This prevents errors when a referenced cell is empty, contains text, or is a header.
   - Fill columns E-H as specified below.

═══════════════════════════════════════════════════
COLUMN SPECIFICATIONS
═══════════════════════════════════════════════════

COLUMNS (in order):

1. Label

2. Conservative Scenario

3. Best Guess Scenario

4. Optimistic Scenario

5. Source: "Application" / "Standard Estimates Sheet" / "Calculated" / "Speculative"

6. Notes: Full, clear, detailed, readable prose sentences, with reasoning and caveats. Include plenty of context from the application. Do NOT make these overly concise. Do NOT include formula explanations.

7. Additional Considerations: REQUIRED for ALL speculative rows. Spell out in full detail: "This figure would increase if: (detailed factors). It would decrease if: (detailed factors). Key questions to investigate include (specific questions)." Write full, clear, readable prose sentences with plenty of context. Do NOT make these overly concise.

8. Formula Description: Plain English. "Total Cost divided by Students Helped"

═══════════════════════════════════════════════════
EXAMPLE OF CORRECT FORMAT
═══════════════════════════════════════════════════

Below is an example with made-up numbers showing the EXACT format. Notice: each row on its own line, semicolons between columns, header and blank rows have empty B-H columns, and calculated rows use IFERROR-wrapped formulas that point only at rows with numbers in them.

```csv
Label;Conservative Scenario;Best Guess Scenario;Optimistic Scenario;Source;Notes;Additional Considerations;Formula Description
Total Funding Requested (USD);50000;50000;50000;Application;Direct from application.;;
Additional Funding Required (USD);0;0;0;Application;No additional funding required for this outcome based on the application.;;
Total Cost (USD);=IFERROR(B2+B3, 0);=IFERROR(C2+C3, 0);=IFERROR(D2+D3, 0);Calculated;Sum of the funding requested and any additional funding this outcome needs.;;Total Funding Requested plus Additional Funding Required
;;;;;;;
[OBJECTIVE 1: Tutoring in partner schools];;;;;;;
Schools Reached;2;5;10;Speculative;Based on the applicant's track record. The applicant reports partnering with 3 schools in the past year with a small team. Scaling to 5 seems plausible with dedicated funding, while 2 allows for slow approvals from school boards.;This figure would increase if: the team already has relationships with the target schools, the district actively supports the program, and the organization dedicates full-time staff. It would decrease if: schools face staff shortages, approvals take longer than a school term, or the organization stretches its capacity across other programs. Key questions to investigate include: What share of approached schools have agreed in the past? Are any partnerships already signed?;
Students per School;40;80;150;Speculative;Estimates based on the class sizes and the number of tutoring slots described in the application. The conservative figure assumes only one year group takes part. The optimistic figure assumes several year groups and full attendance.;This figure would increase if: schools open the program to several year groups or run it in more than one term. It would decrease if: attendance is voluntary and drops after the first weeks, or if only a fraction of eligible students enrol. Key questions to investigate include: How many students attended per school last year? What was the drop-out rate?;
Attribution;0.1;0.3;0.5;Speculative;Attribution reflects how much of the improvement this specific grant can claim credit for, given that students also receive regular teaching and other support. It varies across scenarios because the counterfactual is uncertain.;This figure would increase if: the program is the only extra support the students receive and the outcome measure is tied closely to what is tutored. It would decrease if: other programs serve the same students or if improvements would have happened anyway. Key questions to investigate include: Are other organizations working in the same schools? Does the applicant measure against a comparison group?;
Students Helped (Objective 1);=IFERROR(B7*B8*B9, 0);=IFERROR(C7*C8*C9, 0);=IFERROR(D7*D8*D9, 0);Calculated;Product of schools reached, students per school, and the attribution factor.;;Schools Reached multiplied by Students per School multiplied by Attribution
;;;;;;;
Total Students Helped;=IFERROR(B10, 0);=IFERROR(C10, 0);=IFERROR(D10, 0);Calculated;Sum of all objective-level Students Helped rows. In this single-objective example it equals Objective 1.;;Sum of Students Helped across all objectives
Students Helped per $1,000;=IFERROR(B12/B4*1000, 0);=IFERROR(C12/C4*1000, 0);=IFERROR(D12/D4*1000, 0);Calculated;Divides total students helped by total cost, then multiplies by 1000 to get the rate per $1,000.;;Total Students Helped divided by Total Cost multiplied by 1000
Order of Magnitude Score;=IFERROR(IF(B13<101,1,IF(B13<1001,2,IF(B13<10001,3,IF(B13<100001,4,IF(B13<1000001,5,IF(B13<10000001,6,7)))))), 0);=IFERROR(IF(C13<101,1,IF(C13<1001,2,IF(C13<10001,3,IF(C13<100001,4,IF(C13<1000001,5,IF(C13<10000001,6,7)))))), 0);=IFERROR(IF(D13<101,1,IF(D13<1001,2,IF(D13<10001,3,IF(D13<100001,4,IF(D13<1000001,5,IF(D13<10000001,6,7)))))), 0);Calculated;Maps Students Helped per $1,000 to a 1-7 scale. 1 means fewer than 101 per $1,000 and 7 means more than 10 million.;;Nested IF converting Students Helped per $1,000 to a 1-7 scale
```

═══════════════════════════════════════════════════
HANDLING MULTIPLE OBJECTIVES
═══════════════════════════════════════════════════

If the program has multiple distinct objectives, model each separately:

- Insert a header row for each objective: "[OBJECTIVE 1: Name]" / "[OBJECTIVE 2: Name]"
- Header rows have text ONLY in column A. Columns B through H are EMPTY.
- Include all relevant input rows under each objective header
- Calculate the outcome separately for each objective using IFERROR-wrapped formulas
- Sum the objectives in a final "Total" outcome row
- Leave a blank row between sections for readability (a row with all empty cells)
- If two objectives could count the same people or units, say so in the Notes and avoid double counting

ROWS TO INCLUDE:

- Total Funding Requested
- Additional Funding Required (for THIS outcome only, not the organization's general funding gap)
- Total Cost
- (blank row)
- [Objective header rows as needed]
- [Intervention-specific variables under each objective]
- Attribution (MUST VARY: Conservative Scenario = lowest credit, Optimistic Scenario = highest)
- Outcome row, named after the outcome unit [per objective if multiple]
- (blank row)
- Total outcome
- Outcome per $1,000
- Order of Magnitude Score (relates to the outcome per $1,000, NOT the total outcome)

═══════════════════════════════════════════════════
FORMULA RULES
═══════════════════════════════════════════════════

1. EVERY formula must be wrapped in IFERROR: =IFERROR(your_formula, 0)
2. Formulas must reference SPECIFIC cell addresses (for example B7, C8). Never reference header rows or blank rows.
3. Before writing a formula, count the rows from A1 and check: "Am I pointing at a row that has numbers in it?" If not, adjust the cell reference. An off-by-one reference to a header row silently returns 0.
4. The Order of Magnitude formula uses this nested IF structure:
   =IFERROR(IF(CELL<101,1,IF(CELL<1001,2,IF(CELL<10001,3,IF(CELL<100001,4,IF(CELL<1000001,5,IF(CELL<10000001,6,7)))))), 0)
   replacing CELL with the cell reference for the outcome per $1,000.
5. The bands above (100, 1000, 10000 and so on per $1,000) suit outcomes that are counted in large numbers. If the outcome unit is rare or costly, keep powers of ten but say in the Notes which band edges you used, and use the same bands for every application in the same round so scores compare.

═══════════════════════════════════════════════════
CITATIONS
═══════════════════════════════════════════════════

DON'T use citation markers like (cite:x), as these mean nothing to the reader. Just state (Evidence Tracker), (Application), or (Standard Estimates) as appropriate.

═══════════════════════════════════════════════════
SPECULATIVE ESTIMATES: CRITICAL
═══════════════════════════════════════════════════

Every row marked "Speculative" in the Source column MUST have comprehensive Additional Considerations including:
- Multiple specific factors that would increase the estimate
- Multiple specific factors that would decrease the estimate
- Specific questions the researcher should investigate
- Comparable data points or benchmarks if available

Every row marked "Speculative" in the Source column MUST also have at least 3 sentences in the Notes column.

Numbers: integers without commas. Probabilities: decimals.

═══════════════════════════════════════════════════
AFTER THE CSV BLOCK
═══════════════════════════════════════════════════

Outside the code block, include:

## Qualitative Considerations

(2-3 paragraphs on impacts outside the BOTEC)

## Assumptions to Verify

(Bullets)

═══════════════════════════════════════════════════
NEVER DO ANY OF THE FOLLOWING
═══════════════════════════════════════════════════

- Skip Step 1
- Use abbreviations
- Keep attribution the same across scenarios
- Leave Additional Considerations blank for speculative rows
- Assign the Order of Magnitude Score by feel instead of by formula
- Use citation markers like (cite:x)
- Put multiple CSV rows on one line
- Omit the triple-backtick code fence around the CSV
- Write formulas without IFERROR wrappers
- Put static numbers in a calculated row (Total Cost included)
- Put values or formulas in header rows (columns B-H of header rows must be empty)
- Reference header rows or blank rows in formulas
- Give a row more or fewer than 8 columns
```
