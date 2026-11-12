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
| `scripts/` | The playbooks: `nightly-sync.md` (meetings, mail, chat, documents and people, each night), `daily-review.md` (the weekday memo), `meeting-followups.md`, `lessons.md` (rules from your corrections), `sync-state.md` and `sync-log.md` (blank, filled by the runs), `slack-channels.md`. |
| `skills/` | `README.md` (the schema and the rules for skills), seven agent skills (email reply drafts, inbox cleanup, chat message drafts, documents to sign, checking work, auditing a skill, trying a cheaper model), one marked EXAMPLE (`slack-announcement`), and `my-writing-voice`, a template for how you write. |
| `meetings/`, `email/`, `docs/`, `funders/`, `projects/`, `me/`, `writing/`, `summaries/`, `drafts/`, `asana/`, `inbox/`, `raw/` | Skeleton folders with templates and indexes. The nightly sync fills them. |
| `dot-gitignore` | Becomes `.gitignore` in your vault: secrets and private exports stay out of git. |

## Placeholders

A name in capitals in square brackets, for example `[YOUR_NAME]` or `[WHERE_TO_SEND_DRAFTS]`, is a value that only you know. Setup fills each one in. The full list, with what each means, an example, and where it is used, is `VARIABLES.md` in memo-starter. Words in curly brackets, for example `{Name}` or `{one line}`, are different: they are slots that the agents fill in for each person, meeting or project.

A placeholder you skip stays in capitals in your vault. An agent that meets one asks you once by memo and writes your answer into the file.

## Without Memo

The vault works with any Claude Code session: open a terminal in your vault folder and run `claude`; it reads `CLAUDE.md` first. You still need memo-starter's `npm run setup` to fill the placeholders in, or replace them by hand using `VARIABLES.md`. The scheduled parts (the nightly sync, the daily review, the meeting follow-ups) need Memo to send their memos.

## Before you publish a copy

This repository is a template and holds no personal data. Your vault is the opposite: keep its backup repository private. To check a copy of this template before you share it, run `npm run scan -- ~/second-brain-starter` in `~/memo-starter`.

## License

MIT, see [LICENSE](LICENSE). The Memo app inside memo-starter is by Cameron Blandford, under the MIT license.
