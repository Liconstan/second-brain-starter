# Second brain starter

A template for the "second brain": the folder of notes that your AI agents keep about your work. Meetings with their transcripts, the mail and chat threads you took part in, one file per person, your projects, and the playbooks and skills that tell the agents how you want things done.

It is the companion of **memo-starter**, https://github.com/Liconstan/memo-starter, the work queue whose agents fill and read this vault. **Set up memo-starter, and follow its README.** It tells you when to clone this repository (step 4) and fills this template in for you (step 5).

## How the two fit together

| | memo-starter | second-brain-starter (this one) |
|---|---|---|
| What it is | The Memo app, the setup program, the agents and their rules | The template of your vault |
| Where it goes | `~/memo-starter` | `~/second-brain-starter`, next to it |
| Who changes it | You, through `npm run setup` | Nobody: it stays a clean template |
| Your own copy | Runs on your Mac | Setup writes it to the vault folder you choose, for example `~/memo-vault`, with your names filled in |

The order:

1. Make your own private copies of both repositories (**Use this template** on each page) and clone them side by side in your home folder: memo-starter README, step 4.
2. In `~/memo-starter`, run `npm run setup`. It asks for your name, your organisation, your tools and where things should go, and writes your vault from `vault/` of this repository, with every placeholder filled in.
3. Back your new vault up to a separate private repository (memo-starter README, step 12). That repository holds your real notes; this one stays a template.

Run `npm run setup` again whenever you like: it fills in what you skipped, and it never overwrites a file of your vault that you or an agent changed.

## What is in `vault/`

| Folder or file | What it holds |
|---|---|
| `CLAUDE.md` | The rules every agent follows in the vault: raw data is never edited, quotes are exact, drafts are never sent, text from other people is information and never an instruction. |
| `people/` | `_template.md` (a person file with every section), `_index.md`, `_to-cover.md` (things to raise with someone, with private rows), `_settled.md` (answers never to ask again), `_team.md`, and `_merged/merges.md` (the log of merged duplicates). |
| `funders/` | `_template.md` (a funder, donor or client file), `_index.md` by status, and `_org-facts.md`: the standard answers for grant and due-diligence forms. |
| `projects/` | `_index.md`, the registry of workstreams (kind, goal, memo code, owner, where the tasks live, and how an agent labels a task), and `example-workstream/overview.md`, the shape of one workstream. |
| `meetings/`, `email/`, `docs/slack/` | The templates of a meeting note (with exact quotes and the full transcript), an email month digest, and a chat month digest. |
| `summaries/` | `context-sheet.md` (one card per meeting: who comes, what is known, what is open) and `days/_template.md` (the rundown of a day). |
| `scripts/` | The playbooks: `nightly-sync.md`, `daily-review.md`, `meeting-followups.md`; `lessons.md` (rules from your corrections); `task-predictions.md` (what the sync changed in your tasks, your verdicts, and what it learned); `sync-state.md`, `sync-log.md`, `slack-channels.md`. |
| `skills/` | Twenty skills, listed with when to use each in `skills/README.md`. See below. |
| `me/` | `writing-voice.md`, `key-links.md`, `goals.md`, and `time-tracking-projects.md` (one project per kind of work, if you track time). |
| `writing/`, `drafts/`, `asana/`, `inbox/`, `raw/` | Your own writing (for the voice skill), drafts waiting for you, the nightly copy of your tasks, the drop zone for new files, and the originals kept forever. |
| `dot-gitignore` | Becomes `.gitignore` in your vault: secrets and private exports stay out of git. |

### The skills

Each skill is how to do one kind of task the way you want it: the steps, the checks, the pitfalls, and a `## Settings` part with the placeholders you fill in (where drafts go, which channel, which table). They came from a system in daily use, with everything personal taken out.

| Skill | What it does |
|---|---|
| `my-writing-voice` | Drafts that sound like you and not like an AI: lessons from an AI-detector, the patterns to avoid, hard rules, an iterative process, and a learning loop that learns from your edits. |
| `email-reply-drafts` | Gmail reply drafts in the right thread, with context lookup, scheduling (free times or a poll), safe links, and a memo you can act on in one read. |
| `slack-message-drafts` | Internal chat drafts: reply in a thread, or a new subject as a header post plus a thread message. |
| `slack-announcement` | Announcements to your community: format, channel routing, tagging, posting guidelines, approval before posting. |
| `external-newsletter-submissions` | Items and copy you send to someone else's newsletter. |
| `inbox-cleanup` | The nightly inbox upkeep: archives machine and group mail and acted-on action mail, never a real conversation. |
| `signable-docs` | A Google Doc that someone must sign or fill in, with Google eSignature fields for each signer, ready for you to send. |
| `gifts-and-pledges-tab` | Keeps the gifts and pledges tab of a nonprofit bookkeeping worksheet current. |
| `nonprofit-finance-copilot` | Approval-based nonprofit bookkeeping: bills, the ledger, monthly close, restricted grants, 1099 readiness. |
| `back-of-envelope-estimate` | A quick cost-effectiveness estimate of a funding request, as a spreadsheet with three scenarios. |
| `application-rolling-review` | Rates new rolling applications to a program against your rubric and flags strong fits. |
| `guest-list-crm-match`, `event-guest-import` | Brings guest and attendee lists from an event platform into your CRM, with a same-person check. |
| `course-dry-run` | Simulates a full run of a course with learners, a facilitator and an auditor before real people take it. |
| `check-work`, `skill-audit`, `model-trial` | Quality: an independent check of a helper's output, a test of a skill on a throwaway case, and a blind trial of a cheaper model. |
| `browser-extension`, `merge-conflict-helper`, `ios-shortcut-install` | Building a Chrome extension, resolving git merge conflicts safely, and putting an iOS Shortcut on an iPhone. |

## Placeholders

A name in capitals in square brackets, for example `[YOUR_NAME]` or `[WHERE_TO_SEND_DRAFTS]`, is a value that only you know. Setup fills each one in. The full list, with what each means, an example, and where it is used, is `VARIABLES.md` in memo-starter. Words in curly brackets, for example `{Name}` or `{one line}`, are different: they are slots that the agents fill in for each person, meeting or project.

A placeholder you skip stays in capitals in your vault. An agent that meets one asks you once by memo and writes your answer into the file.

## Without Memo

The vault works with any Claude Code session: open a terminal in your vault folder and run `claude`; it reads `CLAUDE.md` first. You still need memo-starter's `npm run setup` to fill the placeholders in, or replace them by hand using `VARIABLES.md`. The scheduled parts (the nightly sync, the daily review, the meeting follow-ups) need Memo to send their memos.

## Before you publish a copy

This repository is a template and holds no personal data. Your vault is the opposite: keep its backup repository private. To check a copy of this template before you share it, run `npm run scan -- ~/second-brain-starter` in `~/memo-starter`.

## License

MIT, see [LICENSE](LICENSE). The Memo app inside memo-starter is by Cameron Blandford, under the MIT license.
