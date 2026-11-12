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
| `email-reply-drafts` | agent | You triage the email of [YOUR_FIRST_NAME] or draft a reply in Gmail. | strongest tier, medium |
| `inbox-cleanup` | agent | The nightly inbox upkeep, or a request to clean up the inbox. | strongest tier, medium |
| `slack-message-drafts` | agent | You draft an internal chat message for [YOUR_FIRST_NAME] to send. | strongest tier, medium |
| `signable-docs` | agent | [YOUR_FIRST_NAME] wants a document that someone must sign or fill in. | strongest tier, medium |
| `check-work` | agent | Before the output of a helper with stakes reaches [YOUR_FIRST_NAME]. | strongest tier, medium |
| `skill-audit` | agent | A request to audit or test a skill, or a skill was rewritten. | strongest tier, medium (judge) |
| `model-trial` | agent | Only on request, or when a cheaper or faster model tier is released. | strongest tier, medium |
| `slack-announcement` | agent, EXAMPLE | An announcement to [SLACK_CHANNEL_FOR_ANNOUNCEMENTS]. An example of a skill for one organisation: change it or delete it. | strongest tier, medium |
| `my-writing-voice` | hand-made | Drafting anything [YOUR_FIRST_NAME] sends under the name of [YOUR_FIRST_NAME]. The writing skills above read it. | strongest tier |

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
