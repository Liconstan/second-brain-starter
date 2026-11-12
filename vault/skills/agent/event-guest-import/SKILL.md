---
name: event-guest-import
description: Use when [YOUR_FIRST_NAME] asks to bring guest lists from [EVENT_PLATFORM] into [CRM_NAME], or who came to [YOUR_ORG]'s events there. Covers the export, leaving out unrelated events, profile names and photos, and the handoff to guest-list-crm-match.
purpose: A clean list of event-platform profiles from [YOUR_ORG]'s events, in the common shape guest-list-crm-match takes, with the facts only the platform gives.
helper_model: sonnet medium
model_why: export and cleaning are mechanical; which events count is the owner's call
created_by: agent
created: [SYNC_START_DATE]
last_used: [SYNC_START_DATE]
source: the Memo starter kit
---

# Event guest lists into the CRM

## Goal

Turn the events on [EVENT_PLATFORM] into a list of real people for the CRM. The platform is only the source; matching, the check page, notes and the import file are in `guest-list-crm-match`.

## Settings

- The event platform: [EVENT_PLATFORM] (default Partiful; the facts below are for Partiful, check them for another platform)
- The CRM: [CRM_NAME]
- Where the export goes: [OUTBOX_PATH]
- Fill in later: until the platform is set, use Partiful and say so in the memo.

## When to use

Guest lists on [EVENT_PLATFORM] to match, add or update in the CRM, or a question about who came to [YOUR_ORG]'s events there.

## When not to use

Luma, Swapcard, or a spreadsheet that already has emails: go straight to `guest-list-crm-match`.

## Steps

1. Export the events and guests to [OUTBOX_PATH]: `<Platform> events - <date>.csv` and `<Platform> events and guests - <date>.csv`. Platform pages often need the signed-in browser of [YOUR_FIRST_NAME]: use a browser task (Claude in Chrome), batched, never one page per task.
2. Keep only events run by or tied to [YOUR_ORG]. Many accounts also hold personal events, friends' parties and coworking sessions: leave those out. List any event you are unsure of in one memo before matching, and wait for the answer.
3. One row per profile: the profile id (on Partiful, from `partiful.com/u/<id>`), the guest name as the event shows it, the profile link, and the [YOUR_ORG] events with their count.
4. Read each profile's own name and photo with a small script (one request a second; on Partiful the name is the page's `og:title`, the photo its `og:image`). Do it for every profile that shows a first name only, a guessed name, or one of several profiles with the same name. The profile's own name wins over the guest-list name: two guests called "Sam" on the list can be two different people with different last names.
5. Hand the list to `guest-list-crm-match` from its step 2. Its check page shows the photo and the profile's own name on each card.

## Facts about Partiful that change matching

- Many guests show a first name only. Never match or add one on a first name alone; leave it out and list it.
- One person often has several profiles. Fold them only on a Same mark on the check page, never by name alone.
- Partiful gives no emails, so the match rate is low: most party guests are not in the CRM. Say this up front so a low count is not read as a failure.
- Event counts in notes count each event once per person.

## Done when

- Only events tied to [YOUR_ORG] are in the list, and the unsure ones were asked about.
- Every first-name-only or doubtful profile has its own platform name, and its photo where the platform has one.
- The list is handed to `guest-list-crm-match` in the common shape.

## Pitfalls

- Trusting the guest-list name over the profile's own name.
- Counting a profile twice when it was on several events.
- Leaving personal events in: their guests end up in the shared CRM.
