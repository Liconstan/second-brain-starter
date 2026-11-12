---
type: meeting
title: {title of the calendar event}
date: YYYY-MM-DD
meeting_at: {start time with zone}
notes_id: {the id of the meeting in [MEETING_NOTES_TOOL]}
source: [MEETING_NOTES_TOOL] {id}
attendees:
  - {Name <address>}: only people the notes tool lists or the transcript confirms
expected_attendees:
  - {Name}: from the calendar invite or the context card, not confirmed
folders: [{folders of the notes tool}]
raw: raw/{tool}/YYYY-MM-DD-{id}.txt
synced: YYYY-MM-DD
---

# {Meeting title}

## Why it matters
One or two lines: what this meeting changes for [YOUR_FIRST_NAME].

## Key points with citations
Each claim about what a person said carries a short exact quote and who said it.
- {point} ("exact quote, 2 to 20 words", {who})

## Decisions and commitments
- Decided: {decision} ("exact quote", {who})
- [ ] {Owner}: {action}, by {date if one was said} ("exact quote")

## People
[[people/first-last]], [[people/first-last]]. Speakers not settled: `[name unknown]`, with the best candidate from the context card.

## Summary of the notes tool (verbatim)
{The summary of [MEETING_NOTES_TOOL], unchanged, so it can be compared with the transcript.}

## Transcript
{The full transcript, unchanged. The transcript outranks the summary.}
