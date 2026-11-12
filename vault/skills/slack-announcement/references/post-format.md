# House post format

Write in the markdown the Slack tools accept: `**bold**`, `-` bullets, `[text](url)` links, `<@USERID>` mentions. This renders correctly when sent through `slack_send_message` or `slack_send_message_draft`.

## Template

```
{emoji} **{Type} alert: {Name of thing}**
{One or two sentence summary. Who launched it, what it is, who it's for. Tag the lead with <@USERID> if in workspace. Include key constraints like amount, eligibility, location, pay.}

{Label for the list, e.g. "Some areas they want to fund:" or "What they're looking for:"}
- {item}
- {item}
- {item}

📅 {Deadline sentence, if any. Bold the date.}

⭐ {Action phrase} [here]({URL})
```

## Emoji conventions

- 🦅 or 🧠 or another thematic emoji for the title. Match the organization or topic.
- 📅 for deadlines
- ⭐ for the closing link line
- Don't stack emojis. One per line, max.

## Title prefixes by type

- New fund alert:
- Grant round open:
- Job alert:
- Fellowship alert:
- Competition alert:
- Event alert:
- New paper: / New report: / New resource:

## Worked example (funding; made up)

```
🧠 **New fund alert: Example University Research Fund**
The Center for Example Studies at Example University, led by <@U0000000>, just launched a new research fund. They're offering small and seed grants for research that advances their agenda. Open to individuals and institutions, and covers direct research expenses only (no PI salary or indirect costs). Most awards will be under <amount>.

Questions they want to fund research on:
- Whether a given approach works at scale
- How much it costs, and who pays
- What it needs, if anything
- What follows for practice and policy

📅 Submit by **November 1** for guaranteed full consideration. Later proposals are reviewed while funds last.

⭐ Apply [here](https://example.org/apply)
```

## Worked example (job, following guideline minimums; made up)

```
💼 **Job alert: ML Researcher at Example Labs**
Example Labs is hiring a machine learning researcher to build monitoring models. Remote, full time. <pay range>. They want 3+ years of applied ML experience. {Optional: I know the team, happy to make an intro.}

What you'd work on:
- Computer vision for early fault detection
- Open-source dataset curation
- Working with field partners on deployment

📅 Applications close **October 15**.

⭐ Full posting and how to apply [here](https://example.com/jobs/ml-researcher)
```

## Topic-channel pointer format

```
🧠 **New fund alert: Example University Research Fund**
Small and seed grants for research on {topic}, deadline November 1. Full details [here]({permalink to the main post})
```
