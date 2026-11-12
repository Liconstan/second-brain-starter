---
name: course-dry-run
description: "Simulate a full first-time run of a course with a learner, cohort, facilitator, and auditor before real humans take it. Use to dry run, stress-test, pilot, or audit any course, syllabus, curriculum, or facilitator guide."
---

# Course Dry Run

## Why this exists

Course authors know too much. They cannot see where a beginner gets lost, where a facilitator gets stranded by a thin guide, or where the homework quietly asks for knowledge nobody taught. The cheapest time to find those problems is before a single real learner signs up.

This skill runs the course with simulated people who do not know what the author knows. The learner only knows what the target learner would know. The facilitator has read the guide once. The auditor watches both and writes down what worked and what broke.

## The north star

Every judgment the auditor makes answers one question:

**Does someone who finishes this course understand what needs to be done to push the field forward, and are they equipped to do important work in it?**

Not "did they enjoy it." Not "did they finish the readings." A polite pass is a failed audit. If the course produces a graduate who can talk about the field but could not start a project a serious researcher or funder would take seriously, say so.

## Inputs

Collect these before Phase 0. Ask for anything missing. If running unattended, state your assumptions at the top of the log and proceed.

1. **Course materials.** Syllabus plus any companion, facilitator guide, or lesson plans. Accept a Google Doc (read every tab), files, or pasted text.
2. **Readings for each week.** If they are links, fetch and read them. If a reading cannot be fetched, do not fake it. Log a finding ("reading inaccessible to a learner who only has this link") and work from the abstract or description. Check the local course folder first: a reading that will not fetch is often there as a PDF, an HTML copy, or an excerpt in the companion.
3. **Target learner profile.** Background, prior exposure to the field, hours available per week, what they hope to do afterward. If none is given, propose one and confirm it before starting.
4. **Course goals and the destination.** Where graduates are supposed to go next (an incubator, a research program, a job, a funding application). The destination is usually a separate program with its own selection, not part of the course. Use it as the bar the graduate is measured against, not as a hand-off the course guarantees.
5. **Adjacent courses** the course is not supposed to duplicate. Fetch their syllabi if public so the auditor can check overlap concretely.

### Setup rules for the inputs

- **Google Docs with several tabs.** Read every tab, not only the first. List the tabs at the top of the log so it is clear what was read.
- **Missing readings.** Never invent what a reading says. Work from what a real learner would have (the link text, the abstract) and log the gap as a finding.
- **Syllabus and companion disagree.** Log both versions, note which one each persona followed, and resolve it as set out in the behavior rules below.

## Phase 0: set up the personas

Four voices. Keep their knowledge separate.

**Learner.** Load only the background the target learner would plausibly have. Write a short "what I know coming in" note. This note is the firewall. If a reading assumes something not on that note and not taught yet, that is a finding, never something to patch silently.

**Cohort.** Three to five other learners. Each gets a short profile: background, why they enrolled, how prepared they are, and one discussion tendency (over-talks, silent unless asked, pulls toward their own project, pushes back on premises). Vary them so the room looks like the people who would actually sign up. They read and do homework, but only the main learner's work is tracked in full. The cohort exists to make discussions real and to surface facilitation problems a one-on-one would hide.

**Facilitator.** Has read the syllabus and this week's materials once. Has the facilitator guide and appendices for reference. Not a domain expert. Never facilitated this course before. Runs discussion, reviews homework, supports projects. Their job includes noticing when the guide or existing materials do not tell them enough to meet the learner's needs.

**Auditor.** Full context. Never intervenes. Only observes and records.

### The knowledge firewall

- The learner's knowledge is the "what I know coming in" note plus everything the course has taught so far. Nothing else.
- The facilitator's knowledge is the syllabus, this week's materials, the guide, and what happened in earlier sessions. Not the author's intentions.
- The auditor may know everything, but never feeds it to the other voices.

### Run the learner and facilitator as separate subagents

Strongly prefer this. Separate agents keep knowledge separate for real, not by discipline alone. The orchestrator plays the auditor and passes artifacts between agents each week.

What each subagent prompt contains:

- **Learner prompt:** the profile, the "what I know coming in" note, the summary of what has been taught so far, this week's readings and assignment, and the instruction to log confusion honestly and to produce real homework, not a description of it.
- **Facilitator prompt:** the facilitator profile, the syllabus, the guide, this week's materials, the learner's homework and questions, the cohort profiles, and the instruction to run the session from the guide and to log every moment the guide left them unprepared.
- Both prompts: never read ahead in the course, and return their log entries in the format of the weekly loop below.

If subagents are not available, keep the voices in clearly labeled sections and be strict about the firewall. Before writing any learner section, reread the "what I know coming in" note plus everything taught so far, and use nothing else.

## Phase 1: the weekly loop

Run these five steps in order for every week. Do not stop after week one. If the run is long, checkpoint after each week (save the log so far to disk) and continue.

1. **Pre-reading.** The learner reads the assigned material and logs: time taken, new terms and whether they were defined before use, where they got lost, what they think the main point was, and what questions they are bringing to discussion. The facilitator reads the same material plus the guide and logs what they feel unprepared to handle.
2. **Homework.** The learner actually does the assignment. Produce the real artifact, not a description of it. The facilitator reviews it the way a first-time facilitator would, using the course's rubric. No rubric is a finding.
3. **Live session.** Simulate the group session. The facilitator runs it from the guide. The whole cohort is in the room. Each member participates honestly, including confusion, half-formed ideas, tangents, and silence. Log: which prompts produced real thinking, which fell flat, who dominated and who went quiet, where the facilitator improvised or managed the group, whether the main learner's pre-reading questions got answered, and actual length versus planned length.
4. **Project thread.** The learner advances their course project by whatever this week asks for. Track how the idea evolves. The facilitator gives project feedback. Keep a running record so the trajectory is visible at the end.
5. **Weekly audit.** The auditor writes a short entry under these headings: what the learner can now do that they could not do last week; whether that gain was the intended one; concepts used before they were taught; time budget versus reality; facilitator pain points; one specific suggested fix. Also note anything that duplicates a named adjacent course.

Log template for each week:

```
## Week N: <title>
### Learner: pre-reading
Time taken / New terms (defined before use? yes or no) / Where I got lost / Main point as I understood it / Questions I bring
### Facilitator: preparation
What I feel unprepared to handle
### Homework
The artifact (in 02-learner-artifacts.md) / Facilitator review against the rubric
### Live session
Prompts that worked / Prompts that fell flat / Who dominated, who went quiet / Improvisation / Questions answered or not / Planned versus actual length
### Project thread
Where the project stands / Facilitator feedback
### Auditor
New capability / Intended? / Concepts used before taught / Time budget versus reality / Facilitator pain points / One suggested fix / Overlap with adjacent courses
```

**Do not rewrite course materials during the loop.** Log the issue and keep moving. Fixes come in Phase 3. Rewriting mid-run contaminates later weeks, because the learner would then be reacting to material no real learner has seen.

## Phase 2: end of course

1. The learner produces the final deliverable the course asks for (pitch, one-pager, project plan, whatever it is). Real artifact.
2. The auditor evaluates it against the north star using four questions. Be honest:
   - Does this graduate know the field's open problems?
   - Can they tell an important problem from a merely interesting one?
   - Do they know what methods and evidence count in the field?
   - Could they start a project a serious researcher or funder would take seriously?
3. The facilitator writes a retrospective: what they would need to run this again, what they would cut, where they felt exposed.
4. The learner also writes a retrospective: which parts of the course were the most and least useful, what they feel equipped to do or not do, what confused them, what they would change or keep.

## Phase 3: improvement pass

1. **Prioritized change list.** For each change: week and material affected, the problem, evidence from the simulation logs (quote the log), the proposed fix, and the expected effect on the north star. Rank by impact on learning, not by ease.
2. **Make the top changes.** Rewrite the specific sections of the syllabus, companion, or facilitator guide that need it. Deliver revised text, not advice about text. Produce a change log so the author can see exactly what moved. Make sure all files are updated together (for example, new terms are added to the glossary and the companion, and the facilitator guide matches) and no references become stale.
3. **Structural questions.** Flag decisions the author should be aware of (move a week earlier, cut a component, split a reading). For obvious improvements, make the change, but log the reasoning and keep the older content somewhere so it can be reverted or referenced. For less obvious judgment calls, flag them in the change list and wait for a decision from the author.

Formats:

- Change list: a table with the columns `Rank | Week and material | Problem | Evidence (log quote) | Fix | Effect on the north star`.
- Change log: for each edit, the file and section, the old text, the new text, and the change list rank it answers.
- Structural questions: one short paragraph per question, with the options, your recommendation, and what it depends on.

## Design principles the auditor enforces

Use these as the lens for every weekly audit and the final report. Each line says how to test it.

- **Progressive vocabulary.** Plain language first, then the name, then use. Test: list every term in the week and the first place it is explained. Flag any term used before it is introduced.
- **Chunking.** One idea, then build. Test: count the new ideas per session. Flag weeks that front-load caveats or edge cases.
- **Why before how.** Each week opens with why this matters to the field before mechanics. Test: read the first paragraph of the week alone.
- **Retrieval, not exposure.** Homework makes the learner produce something, not summarize something. Test: could the homework be done by copying the reading?
- **Honest time budgets.** Planned hours versus what the simulation actually took. Test: compare the logged times against the syllabus.
- **Prompts have a job.** Each discussion prompt targets a specific misunderstanding or skill. Test: name the job of each prompt. Flag "what did you think?"
- **The project compounds.** Each week builds on the last. Test: by the end, could a reviewer evaluate the project?

## Output

Deliver these files, in this order:

1. `01-simulation-log.md`: one section per week, learner, facilitator, and auditor voices clearly labeled.
2. `02-learner-artifacts.md`: every homework artifact and the final deliverable, in week order.
3. `03-audit-report.md`: end-of-course evaluation against the north star, prioritized change list, structural questions.
4. `04-revised-materials.md`: revised course text with a change log.

Keep everything readable. Headings and short paragraphs. Never use em dashes anywhere in the output. Use commas, periods, or colons instead.

## Behavior rules

- **Run the whole course.** Week one problems are the easy ones. The expensive problems (project does not compound, week five assumes week two landed) only show up late.
- **Be candid.** The entire value of this skill is finding problems before real people hit them. Softening a finding wastes the author's time.
- **Never let the learner know things they have not been taught.** If you catch it happening, log it as an auditor note and back up.
- **When the syllabus and the companion disagree, make a choice based on best practices for courses.** Take into consideration learning value, practical limits, and potential impact on the field. Rewrite based on the best choice and log this decision and the reasoning behind it. Note which one the learner and facilitator each followed and what confusion resulted.
- **When unsure what the author intended, ask.** If running unattended, state your assumption in the log and proceed.
- **Cite the logs.** Every change in Phase 3 points at the week and the moment in the simulation that motivated it.
