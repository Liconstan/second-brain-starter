---
name: slack-message-drafts
description: "Use when you draft an internal Slack message for [YOUR_FIRST_NAME] to send (to a teammate, a channel or a thread). Covers reply or new thread, and the one-draft format: a formatted header on top and the thread message below."
purpose: One Slack draft in the voice of [YOUR_FIRST_NAME], in the right place, in the shape it is sent from without editing.
helper_model: opus medium
model_why: the voice of [YOUR_FIRST_NAME] needs the strongest tier
created_by: agent
created: [SYNC_START_DATE]
last_used: [SYNC_START_DATE]
source: the Memo starter kit
---

# Internal Slack message drafts

## Goal

[YOUR_FIRST_NAME] sends every Slack message. Agents only make drafts with `slack_send_message_draft`, which renders bold, bullets, mentions and links. A new subject is one draft that [YOUR_FIRST_NAME] splits into a header post and a first thread reply, with nothing to delete in between.

## Settings

- The chat tool: [CHAT_TOOL]. Default: Slack. With another tool, use its draft feature the same way, or put the text in the memo only.
- Where a draft goes: [WHERE_TO_SEND_DRAFTS].
- The internal channel of the team: [SLACK_CHANNEL_FOR_TEAM_UPDATES].
- New subject format: header post plus thread reply (step 2). If [YOUR_FIRST_NAME] prefers one plain message, say so here: {header plus thread}.

## When to use

- An internal message from [YOUR_FIRST_NAME] to a teammate, a channel or a thread.

## When not to use

- Community announcements (funding, jobs, events, news): the hand-made skill in `skills/slack-announcement/`.

## Steps

1. Decide: reply or new subject.
   - Reply: the message answers someone in an existing thread, or the channel is a loose conversation with several people talking outside threads. Draft it as one plain message, in the thread when there is one (`thread_ts`).
   - New subject: the message starts a topic [YOUR_FIRST_NAME] is establishing, or should establish to keep the channel tidy. Use the two-piece format in step 2.
2. Two-piece format for a new subject. One draft, two parts:
   - Top: the header message, formatted, short. An emoji, a bold title, and one line on what the thread is for. Bold is **double asterisks**: `slack_send_message_draft` reads standard markdown, so a single *asterisk* shows as italics. This becomes the top-level post. This holds for a new thread in any channel, internal or community.
   - A blank line, then the thread message: the full content, with tags, numbers and asks. [YOUR_FIRST_NAME] posts the header, opens its thread, and pastes this part as the first reply.
   - Write nothing between the two parts that must be deleted: no labels such as "Header" or "Thread".
   Example (made up), a post to a teammate in a project channel:

   ":newspaper: **Newsletter feeds for the reading tool**: the sources we get that aren't on the list yet

   @Sam here are the newsletters we subscribe to that aren't on Robin's list yet, with RSS links: (grouped bullets, each name a hyperlink)"

   When [YOUR_FIRST_NAME] asks to "rewrite it in the channel with the notation" or similar, that means this two-piece format as a new post, not a reply in an old thread.
   Formatting: hyperlink names instead of pasting raw addresses, group long lists under short bold labels, and leave out anything [YOUR_FIRST_NAME] says to drop.
3. Voice: read `skills/my-writing-voice/SKILL.md`, its section on team posts in particular. Tag people with `<@USERID>` from `slack_search_users`; never guess an id.
4. Where the draft goes: in the channel or DM where it will be sent. Slack allows one attached draft per channel and agents cannot edit or delete a draft, so if `draft_already_exists` comes back, say so in the memo and put the text in the memo instead.
5. In the memo: the channel or DM link, whether it is a reply or a two-piece draft, and the full text to paste, every time, even when the draft was created. A draft can come up blank or vanish in the Slack app, and agents cannot read drafts to check, so the memo text is the fallback. If a draft you made earlier is missing, say what you know and that you do not know why; never only "no longer in Slack".

## Done when

- The draft sits in the channel or DM it is for, or the memo says why it could not.
- A new subject has a header line, a blank line, then the thread message, and no labels between them.
- Every tag is a real `<@USERID>`; every link is a hyperlinked name.
- The memo has the link, the kind (reply or two-piece), and the full text.

## Pitfalls

- A reply in an old thread when the two-piece format was asked for.
- Labels such as "Header" or "Thread" that must be deleted.
- A single asterisk for bold, which shows as italics.
- Raw addresses instead of hyperlinked names; a long list not grouped.
- A guessed user id.
- A memo with links only and no paste text: a blank draft then costs a round trip.
- Items the teammate cannot act on: things [YOUR_FIRST_NAME] does alone or wants for later. Leave them out and keep them as tasks for [YOUR_FIRST_NAME] in [TASK_MANAGER] instead.
