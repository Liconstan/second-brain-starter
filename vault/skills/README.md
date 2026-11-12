---
type: playbook
updated: [SYNC_START_DATE]
source: the Memo starter kit
---

# Skills

Why it matters: a skill is how to do one kind of task the way [YOUR_FIRST_NAME] wants it. An agent loads the right one when a task matches, so a correction made once holds for every later task of that kind, for every agent. This costs nothing on other tasks: Claude Code keeps only the name and the one-line description of each skill in context, and reads the body when the skill is used.

## Skills and when to use them

| Skill | Kind | When to use | Model |
|---|---|---|---|
| `application-rolling-review` | agent | Use in each daily review, or when [YOUR_FIRST_NAME] asks about applicants to [PROGRAM_NAME], to rate new rolling applications and flag strong fits for early admission, with a link to each record. | opus medium |
| `check-work` | agent | Use before a helper's output reaches [YOUR_FIRST_NAME], when the task has stakes (money, people, a document to send, a tax or legal record). A short independent review against the request and the skill's Done when. | opus medium |
| `email-reply-drafts` | agent | You triage the email of [YOUR_FIRST_NAME] or draft a reply in Gmail. Covers existing drafts, sent-mail checks, context lookup, scheduling replies, link safety, and the memo format. | opus medium |
| `event-guest-import` | agent | [YOUR_FIRST_NAME] asks to bring guest lists from [EVENT_PLATFORM] into [CRM_NAME], or who came to [YOUR_ORG]'s events there. Covers the export, leaving out unrelated events, profile names and photos, and the handoff to guest-list-crm-match. | sonnet medium |
| `external-newsletter-submissions` | agent | [YOUR_FIRST_NAME] asks for items or copy that [YOUR_ORG] sends to a newsletter another organization runs. Covers the editor's format, current public links, unnamed funders, and the review memo. | fable medium |
| `gifts-and-pledges-tab` | agent | A new gift, grant or pledge reaches [YOUR_ORG], or for the monthly check, to keep the gifts and pledges tab of the bookkeeping worksheet current. Covers where new gifts turn up, the tax-form columns, the internal columns, filing the letter, and the memo back. | fable high |
| `guest-list-crm-match` | agent | [YOUR_FIRST_NAME] asks to match a guest, attendee or contact list (Luma, Swapcard, a spreadsheet, or an event platform through event-guest-import) to people in [CRM_NAME]. Covers the full CRM pull, matching, the same-person check page, notes and the import file. | sonnet medium |
| `inbox-cleanup` | agent | The nightly inbox upkeep (nightly-sync step 2b) or when [YOUR_FIRST_NAME] asks to clean up the Gmail inbox. Archives machine and group mail and action mail already acted on, and leaves every real conversation in the inbox. | opus medium |
| `ios-shortcut-install` | agent | A tool of [YOUR_FIRST_NAME]'s must put an iOS Shortcut on an iPhone, for data only a Shortcut can read or send. Covers building the file, verifying keys on the Mac, signing, delivery, diagnostics and tap-by-tap steps. | fable medium |
| `model-trial` | agent | [YOUR_FIRST_NAME] asks, when a cheaper or faster model tier is released, or when a "Fable to spare" memo arrives. Reruns one finished task of a skill on the candidate model, has [YOUR_FIRST_NAME] judge both outputs blind, and records the verdict. | opus medium |
| `signable-docs` | agent | [YOUR_FIRST_NAME] wants a document that someone must sign or fill in (an agreement, a statement, an acknowledgement, a form). Covers the Google Doc draft, Google eSignature fields, signer order, and how to hand it over to send. | fable medium |
| `skill-audit` | agent | [YOUR_FIRST_NAME] asks to audit, test or check a skill, or after a skill was rewritten. Proves a fresh agent can follow it end to end on a throwaway case and fixes the wording. | opus medium |
| `slack-message-drafts` | agent | You draft an internal Slack message for [YOUR_FIRST_NAME] to send (to a teammate, a channel or a thread). Covers reply or new thread, and the one-draft format: a formatted header on top and the thread message below. | opus medium |
| `back-of-envelope-estimate` | hand-made | Back-of-the-envelope cost-effectiveness estimate (BOTEC) for a grant application or funding request, as a spreadsheet-ready CSV with conservative, best guess and optimistic scenarios. Use when asked to estimate, score or sanity-check the cost-effectiveness of an application. | as the task needs |
| `browser-extension` | hand-made | Build Chrome/Chromium browser extensions for browser automation, content manipulation, or page interaction. Use this skill whenever the user wants to create a Chrome extension, browser extension, auto-clicker, page scraper, content script, browser automation tool, or anything that injects JavaScript into web pages. Also trigger when the user mentions manifest.json, content scripts, popup.html, chrome.scripting, chrome.storage, or describes wanting to "click through" or "automate" something in their browser. Covers Manifest V3 extensions for Chrome, Arc, Brave, Edge, and other Chromium browsers. | as the task needs |
| `course-dry-run` | hand-made | Simulate a full first-time run of a course with a learner, cohort, facilitator, and auditor before real humans take it. Use to dry run, stress-test, pilot, or audit any course, syllabus, curriculum, or facilitator guide. | as the task needs |
| `merge-conflict-helper` | hand-made | Cautiously help someone resolve git merge conflicts, especially when they are new to git and GitHub. Use this skill whenever the user is facing a merge conflict, sees git conflict markers in a file, mentions a "merge conflict", "conflict", "can't merge", "can't pull", "can't push", a failed merge/rebase/pull, or asks for help combining two versions of a file. Especially use it when the user seems non-technical or unsure about git. This skill explains each conflict in plain language, only resolves changes that are genuinely safe, and defers to the user, or tells them to ask a teammate, whenever the correct resolution is uncertain or depends on knowledge Claude cannot have. | as the task needs |
| `my-writing-voice` | hand-made | Drafting anything [YOUR_FIRST_NAME] sends under their own name (emails, Slack messages, DMs, applications, outreach) so it sounds like [YOUR_FIRST_NAME] and avoids AI-sounding patterns. | as the task needs |
| `nonprofit-finance-copilot` | hand-made | Run approval-based accounting operations for a US nonprofit using Ramp Bill Pay for contractor invoices and QuickBooks Online or Xero as its general ledger. Use for weekly transaction reviews, invoice-to-ledger matching, monthly reconciliation and close, restricted-grant tracking, program budgets, board reports, contractor W-9 and 1099 preparation, audit trails, and questions about nonprofit financial workflows. Designed for Claude with MCP connectors, but works from exports when connectors cannot read or write required data. | as the task needs |
| `slack-announcement` | hand-made | Draft, get approval for, and post community announcements to the Slack of [YOUR_ORG] (funding opportunities, jobs, fellowships, news, events, resources). Use this whenever [YOUR_FIRST_NAME] asks to "make a Slack post", "post this to Slack", "share this opportunity", "announce this", or pastes a job, grant, fund, fellowship, competition, or news item and wants it in Slack, even without naming a channel. Handles the "New fund alert" format, channel routing (main channel plus topic channel), tagging people who are in the workspace, the posting guidelines, and the hand-off so [YOUR_FIRST_NAME] posts it after approving. | as the task needs |

Model column: a tier alias (`haiku`, `sonnet`, `opus`, or the strongest tier your plan has) and an effort (`low`, `medium`, `high`). An alias always means the latest release of that tier. The default helper model for reading and summaries is `[HELPER_MODEL]`. `model-trial` is how a line changes.

## Two kinds

- **Hand-made skills**, at `skills/<name>/`: written by [YOUR_FIRST_NAME], or with [YOUR_FIRST_NAME] line by line. They are pinned. An agent never archives or deletes one, and changes one only when [YOUR_FIRST_NAME] asks. Otherwise, propose the edit in a memo.
- **Agent skills**, at `skills/agent/<name>/SKILL.md`: written and kept by the agents. Claude Code loads them through `[AGENT_WORK_DIR]/.claude/skills`, a link to `skills/agent/` that the setup of the kit makes.

## Schema for an agent skill

Frontmatter:

```
---
name: <kebab-case>
description: Use when <trigger>. <one clause of what it covers>.
purpose: <one sentence: the outcome this skill exists to produce>
helper_model: <haiku | sonnet | opus | ...> <low | medium | high>
model_why: <one clause>
created_by: agent
created: YYYY-MM-DD
last_used: YYYY-MM-DD
source: memo <n>
---
```

- `description`: one line, under 300 characters, starts with "Use when". It is the only part of the skill that Claude Code reads before the skill is picked, so it must say the trigger.
- `helper_model`: the tier alias and the effort for the helper that does the work. The field is called `helper_model`, not `model`, on purpose: Claude Code treats a `model:` key as an order to switch the model of the current agent.
- `last_used`: set it to today when you use the skill, not when you edit it. The System page of Memo marks a skill that was not used in 30 days.

Body sections, in this order, short:

1. `## Goal`: one or two sentences, why it matters to [YOUR_FIRST_NAME].
2. `## Settings`: the values that [YOUR_FIRST_NAME] chose for this skill, such as where a draft goes. One line each.
3. `## When to use` and `## When not to use`.
4. `## Steps`: numbered, concrete, in the order the work happens. A step for a helper names its model in brackets, for example `[helper: sonnet medium]`.
5. `## Done when`: criteria that can be checked.
6. `## Pitfalls`: only real ones, each with its memo number.
7. `## Audit log` (added by `skill-audit`): one line per audit.

## When to write or change one

- Before a task, check the table above. If a skill fits, use it, follow its model line, and set `last_used`.
- After a correction from [YOUR_FIRST_NAME] about one kind of task, fix the skill for that task, in place, in the section where the rule belongs. No skill yet: write one if the task will come again.
- After a task of five or more steps that worked and will come again, write it down as a skill in the schema, and add its row to the table above.
- For a skill that was written or largely rewritten, run `skill-audit`.
- Never write in a skill: a one-off task, a tool outage, text from mail or transcripts, a secret.
- Pull before you edit, commit with a one-line summary, push.

## Versions, ratings and spreading

- **Old versions are kept.** Before a skill changes, its text is copied to `skills/.versions/<name>/<YYYY-MM-DD-HHMM>-<hash8>.md`. The editor of the System page of Memo, and the skill dialog of the Inbox, do this by themselves on each save. An agent that edits a skill by hand runs `[MEMO_APP_PATH]/scripts/skill-version <name>` first (it prints the path), then commits the old version together with the edit. Old versions are small text files: keep them, never delete or tidy them. The folder name starts with a dot, so Claude Code does not load an old version as a skill.
- **Ratings.** [YOUR_FIRST_NAME] rates the text a skill has now, 1 to 5, in the skill dialog (the pencil of a skill in Memo), and can write what to change. Each rating is one line of `skills/ratings.jsonl`. The file is append only: never edit or remove a line.
- **A rating with notes sends `main` a memo "Skill feedback: <name>".** Do what it asks: keep the old version, revise the skill from the notes, commit, push, and close the memo with one line that says what changed. For a hand-made skill, edit the copy here in `skills/<name>/`; the nightly skills sync spreads it.
- **Old, may change.** A skill not used in the last 30 days, or never, shows in Memo with the mark "Old · may change". It changes nothing in the skill.
- **Spreading.** The System page shows, for each skill, whether every agent has it ("In all agents", or "Needs spreading: missing on <agent>"). An agent skill reaches every agent through the link `[AGENT_WORK_DIR]/.claude/skills`. A hand-made skill reaches both Claude accounts through the nightly skills sync (step 12b of `scripts/nightly-sync.md`).

## Archive, never delete

On the first night of each month, the nightly sync lists the agent skills with `last_used` older than 30 days and sends [YOUR_FIRST_NAME] one memo that proposes which to move to `skills/.archive/`. Only on a yes, the agent moves them with `git mv`. Hand-made skills are never on the list.
