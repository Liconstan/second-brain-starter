---
name: guest-list-crm-match
description: Use when [YOUR_FIRST_NAME] asks to match a guest, attendee or contact list (Luma, Swapcard, a spreadsheet, or an event platform through event-guest-import) to people in [CRM_NAME]. Covers the full CRM pull, matching, the same-person check page, notes and the import file.
purpose: An import file that [CRM_IMPORTER] can load into [CRM_NAME], built from matches [YOUR_FIRST_NAME] settled on a fast check page.
helper_model: sonnet medium
model_why: the pulls are mechanical; the main agent judges the uncertain matches and writes the notes
created_by: agent
created: [SYNC_START_DATE]
last_used: [SYNC_START_DATE]
source: the Memo starter kit
---

# Matching a list of people to the CRM

## Goal

Tell [YOUR_FIRST_NAME] which people on a list [CRM_NAME] already knows and which are new, let [YOUR_FIRST_NAME] settle the doubtful ones fast, and hand [CRM_IMPORTER] one import file in the CRM's own shape. This skill works for any source. Steps that belong to one source live in their own skill and feed into this one: for an event platform, `event-guest-import`.

## Settings

- The CRM: [CRM_NAME]
- Where people live in the CRM (every table, view or list that holds people): [CRM_PEOPLE_TABLES]
- Who imports the file, and how to reach them: [CRM_IMPORTER]
- Where the import file goes: [OUTBOX_PATH]
- Fill in later: until these are set, ask [YOUR_FIRST_NAME] once, then write the answers here.

## When to use

A list of people, with or without emails, to compare with the CRM or to add to it.

## When not to use

- A single person: use the CRM's own person search directly.
- Questions about counts: use the CRM's reports.

## Steps

1. Get the list in the common shape: one row per source profile, with a stable id, the name as the source shows it, a profile link, the email if any, and the events or context it came from. For an event platform, `event-guest-import` makes this.
2. Pull the whole CRM, every person. Read the connector's catalog or schema once. Many CRM connectors have no list-all tool and are read only: then the people universe is the union of every place in [CRM_PEOPLE_TABLES] (for example every program at the widest involvement level, plus the people of each standalone event, since some events hold people found nowhere else). Split the pulls across 3 or 4 helpers [helper: sonnet medium]; each only calls the tools and never retypes rows. Read the rows from the helpers' saved tool results (their transcripts), not from their summaries.
3. Build one deduplicated people file with a small script in `drafts/<date>-<source>-crm/`. It prints OK or GAP for each source against that tool's own total. Do not go on with a GAP.
4. Match with a script in the same folder, adapted to the list's columns. Order: email; exact normalised name; first and last name; nickname or first-name prefix with the same last name. A name the CRM holds more than once is a CRM duplicate, not an uncertain match. A first name alone is never matched.
5. Write the notes and fill the fields (see the two sections below).
6. Build the same-person check page. Every match that is not by email, and every group of several source profiles folded into one person, goes on one page where [YOUR_FIRST_NAME] marks each profile Same person, Not same, or Unsure. One card per person: the CRM record on the left; the source profiles on the right, with photo, the name the profile itself shows, events, and any earlier call on that profile. Marks save as they are made: an artifact page with the `db` capability, collection `regroup`, one document per profile id. Read the marks back with ArtifactData `list`.
7. Build the import file from the marks. Same folds the profile into the CRM record or group. Not same becomes a new person only when the profile carries a full name, with neutral fields and a note that says only what is known. Unsure and first-name-only profiles are left out and listed. Save it in [OUTBOX_PATH] as `<Source> CRM import - <date> v<N>.csv`, and say which earlier version it replaces.
8. One memo: the link to the check page first. Then, after [YOUR_FIRST_NAME] is done, the counts, what is left out and why, and the file path. If an open memo or draft to [CRM_IMPORTER] attaches an earlier version, update it to the new one.

## The import file

One row per person. Columns: `action` (update existing or add new), `crm_record_id`, `crm_existing_name`, `full_name`, `current_title`, `current_affiliation_text`, `city`, `country`, `primary_email`, `other_emails`, `linkedin_url`, `website_url`, `crm_notes_staff`, `crm_notes_admin`, the source profile links and their count, the events and their count, and `owner_notes`. Rename a column only to match the person fields of [CRM_NAME]; ask [CRM_IMPORTER] once if unsure.

## Notes written for the CRM

The CRM is shared by the team, so a note about a person is about them, not about [YOUR_FIRST_NAME].

- Third person and neutral: no "met you", no "a friend of [YOUR_FIRST_NAME]". A made-up example: "Co-director of an example research group. Has funded [YOUR_ORG] projects. On [YOUR_ORG]'s guest lists for 13 events."
- Two fields: `crm_notes_staff` (who they are, how [YOUR_ORG] knows them) and `crm_notes_admin` (money: donations, pledges, grants). Code them for the roles the CRM's views are built for.
- No memo numbers and no agent references. Most private notes from `people/` may go in; keep out anything marked never publish, and any person file with a `sensitive:` line.
- Fill what you can find: location, LinkedIn, current title and organisation, from the vault, the CRM and the web. A title is not a substitute for a note.
- When a match is undone, drop the notes and fields that came from the wrong person.

## Done when

- Every source shows OK in step 3.
- Every non-email match and every folded group has a mark on the check page.
- The memo's numbers equal the import file's counts, and the file names the version it replaces.

## Pitfalls

- A helper that retypes 250-row pages by hand overflows its context and makes typos. Helpers call the tools; scripts read the saved results.
- Asking [YOUR_FIRST_NAME] to settle matches in a long memo instead of on the check page.
- Folding several profiles into one person by a shared first name. Most of those turn out to be different people.
- Matching against a partial CRM pull. A person missing from the pull looks new and gets added twice.
