---
name: inbox-cleanup
description: Use for the nightly inbox upkeep (nightly-sync step 2b) or when [YOUR_FIRST_NAME] asks to clean up the Gmail inbox. Archives machine and group mail and action mail already acted on, and leaves every real conversation in the inbox.
purpose: The inbox holds only mail from people and things that still need an action.
helper_model: opus medium
model_why: judgment on each bulk query, and a real conversation must never be archived
created_by: agent
created: [SYNC_START_DATE]
last_used: [SYNC_START_DATE]
source: the Memo starter kit
---

# Inbox cleanup

## Goal

The work inbox, [YOUR_EMAIL], shows real people and open actions, nothing else. Each run covers the whole inbox, not only the new mail. A first run on a neglected inbox can halve it; keep the plan, the queries and the counts of that run in a file under `drafts/` so later runs reuse them.

## Settings

Fill in later. An unfilled line means: skip that rule and ask [YOUR_FIRST_NAME] once in the first-run memo.

- The mailbox: [YOUR_EMAIL].
- Group addresses to archive at any age: [GROUP_ADDRESSES_TO_ARCHIVE]. For example: courses@, newsletter@, team-internal@.
- Group addresses to archive after 14 days, unless [YOUR_FIRST_NAME] replied in the thread: [GROUP_ADDRESSES_ARCHIVE_AFTER_14_DAYS]. For example: ops@.
- Group addresses that always stay (people write there in person): [GROUP_ADDRESSES_TO_KEEP]. For example: hiring@ (applicant conversations).
- A label that marks mail to answer, from an older triage tool, if any: [TO_RESPOND_LABEL]. Default: none.
- Labels that may stay on threads: every existing label. Never create a new one.
- [YOUR_FIRST_NAME]'s own email rules, if written down somewhere (an ops guide, an onboarding doc): {link}. A common rule: group and machine mail gets filtered out of the inbox; only truly important mail stays unread.

## When to use

- Step 2b of `scripts/nightly-sync.md`, after the first yes (below).
- [YOUR_FIRST_NAME] asks to clean up the inbox.

## When not to use

- Answering mail: `email-reply-drafts`.
- Before the first yes: send the first-run memo (step 1) and stop.

## Steps

1. Before the first run: send [YOUR_FIRST_NAME] one memo with the Settings and the lists in steps 3 to 5, and ask for a yes, with changes. Write the changes into this file. Run nothing before that yes. Then put the date here: {not approved yet}.
2. Confirm the account is [YOUR_EMAIL]. The rules for every run:
   - Archive and mark as read. Never delete, trash, unsubscribe, send, draft or create a filter. Never mark the mail of a person as read.
   - No new labels. Existing labels stay on their threads.
   - Always skip starred threads.
3. Archive, whatever its age:
   - Google Docs and Drive comment and activity notices, except a comment or reply written by a person (step 5); "shared with you" notices, including those sent through a Google Group.
   - Calendar accepted, declined, updated and cancelled mail, and invitations for past dates.
   - Share notices of [MEETING_NOTES_TOOL]. Leave other meeting-notes mail until [YOUR_FIRST_NAME] says otherwise.
   - Newsletters, Substack and promotions; product notices from tools; the own mass program mail of [YOUR_ORG].
   - Notifications of tools: [TASK_MANAGER], Slack, Airtable, Notion, Zoom, GitHub, event reminders, form tools.
   - Receipts and payment notices that need no action: "payment initiated", "delivered", "receipt matched, no action required".
   - Login and verification codes; automatic replies such as out of office, leave, offline, "no longer at".
   - Mail to the group addresses in Settings, by their rule.
4. Action mail: approval, signature, verify or "action required" mail. Check the live tool first, such as the status of the bill in the payments tool or of the signing request.
   - Done: archive.
   - Not done: leave it, and list it for "Emails to answer" in `scripts/daily-review.md`.
   - Done but carrying [TO_RESPOND_LABEL]: leave it, since the nightly sync skips that label. List it for the daily review once, as a count with "done in the tool, can archive".
   - No tool can check it (a signing service with no connector, old verify-your-email links): leave it and list it for the daily review.
5. Keep in the inbox:
   - Any thread where a person wrote to [YOUR_FIRST_NAME] personally, or where [YOUR_FIRST_NAME] replied. A label such as "To respond" or "Human" left by an old tool does not make a notification personal, and does not make a person's thread machine mail.
   - A comment notice whose comment or reply a person wrote, such as a teammate answering a comment on a job description. Only edit, share and resolve notices with no text from a person get archived.
   - Invitations for future events. Mail to the group addresses to keep. Real grant, donation and invoice threads, including in the Forums tab. Starred threads.
   - Unsure: password manager account mail, admin notices of tools, suspicious-login alerts, event invitations, share requests for the docs of [YOUR_FIRST_NAME]. Leave them.
6. After each bulk query: spot-check the first page for real conversations and move any back. If [TO_RESPOND_LABEL] is set, search `label:"<label>" -in:inbox newer_than:1d` and move those threads back.
7. Write the log line.

## Done when

- No machine mail of the kinds above is in the inbox, and no real conversation left it.
- The log line reads `inbox archived N, action open M, inbox now T`.

## Pitfalls

- Gmail search matches per message, so `-label:"<label>"` still catches a thread with one labelled message. Check after each bulk archive (step 6).
- Bulk queries catch real conversations: staff of a payments tool, vendor support threads [YOUR_FIRST_NAME] replied to, calendar replies with a personal note. Spot-check the first page of every query, and skip threads with a message from [YOUR_FIRST_NAME].
- The Gmail connector may cap counts (around 200). For bulk work, Gmail in Chrome has "Select all conversations that match this search". Confirm the account in Chrome is [YOUR_EMAIL] first.
- A new label to sort mail: not allowed.
