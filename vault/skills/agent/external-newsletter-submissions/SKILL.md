---
name: external-newsletter-submissions
description: Use when [YOUR_FIRST_NAME] asks for items or copy that [YOUR_ORG] sends to a newsletter another organization runs. Covers the editor's format, current public links, unnamed funders, and the review memo.
purpose: Newsletter items in the editor's format, with working public links and no claims [YOUR_FIRST_NAME] did not make, ready to send.
helper_model: fable medium
model_why: the cover note is in the voice of [YOUR_FIRST_NAME] and the items are public copy
created_by: agent
created: [SYNC_START_DATE]
last_used: [SYNC_START_DATE]
source: the Memo starter kit
---

# Items for an external newsletter

## Goal

The editor can paste the items as they are. Every link works for the public, every claim is one [YOUR_FIRST_NAME] made, and the funders that may not be named stay unnamed.

## When to use

- [YOUR_FIRST_NAME] asks for items, copy or a submission for a newsletter another organization sends.

## When not to use

- Slack announcements: the hand-made skill in `skills/slack-announcement/`.
- The own newsletter of [YOUR_ORG]: no skill yet. Ask [YOUR_FIRST_NAME] how it is made.

## Steps

1. Find the newsletter's own format first: its sections, item length and tone. Read two or three recent issues. A common shape: one to three sentences per item, third person, neutral, one link per item where possible. Note the editors' names and the format in the newsletter's organization file in `people/` or `funders/` if there is one, so the next round starts there.
2. Ask what [YOUR_FIRST_NAME] wants to advertise if the memo does not say. Default: upcoming events of [YOUR_ORG] with public RSVP links, then programs and expressions of interest.
3. Use only the sections that fit what [YOUR_ORG] is announcing. Do not add sections because the newsletter has them, such as calls for abstracts or job openings.
4. Link to what is current: this cohort's page, the open application, the next event. Not a past gallery or a closed round. Links are in `me/key-links.md` and on the live website; when they differ, the live site wins.
5. Never name a funder without its approval. Check `funders/<name>.md` for what may be said in public; some funders need mutual approval for any public acknowledgement. When in doubt, describe the program instead (for example "the fellowship awards") and ask [YOUR_FIRST_NAME] in the memo.
6. When a program item follows an event item, invite people into the next program: lead with participation numbers (participants, mentors, projects, taken from the vault, never estimated), then the expression of interest or application forms, and only then any awards or perks. Never lead with the perks.
7. Start from the text of [YOUR_FIRST_NAME] when there is one; keep it short. Do not add claims [YOUR_FIRST_NAME] did not make, such as "first edition" or "largest".
8. Organize: one intro line, then sections, then a short cover note to the editor in the voice of [YOUR_FIRST_NAME] (`skills/my-writing-voice/SKILL.md`). No em dashes.
9. Check every link works for the public before the memo goes out: event pages public with registration open, no private docs, no pages behind a login.
10. Save the draft under `drafts/` in the vault, commit and push, then send [YOUR_FIRST_NAME] a review memo with the items and the cover note in full, and a link to the draft file.

## Done when

- Items match the newsletter's length and tone, with one public link each.
- No funder named without approval; no claim [YOUR_FIRST_NAME] did not make.
- The draft is in `drafts/`, pushed, and the memo shows every item in full.

## Pitfalls

- Sections added because the newsletter has them.
- Linking a past gallery or a closed round instead of the current cohort or open form.
- Leading with awards or perks instead of the numbers and the forms.
- A "first edition" or other claim [YOUR_FIRST_NAME] did not make.
- A funder named in public copy without its approval.
- A link that works only when logged in.
