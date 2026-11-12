---
name: slack-announcement
description: Draft, get approval for, and post community announcements to the Slack of [YOUR_ORG] (funding opportunities, jobs, fellowships, news, events, resources). Use this whenever [YOUR_FIRST_NAME] asks to "make a Slack post", "post this to Slack", "share this opportunity", "announce this", or pastes a job, grant, fund, fellowship, competition, or news item and wants it in Slack, even without naming a channel. Handles the "New fund alert" format, channel routing (main channel plus topic channel), tagging people who are in the workspace, the posting guidelines, and the hand-off so [YOUR_FIRST_NAME] posts it after approving.
---

# Community announcement in Slack

For internal messages from [YOUR_FIRST_NAME] (to a teammate, a channel or a thread), use `skills/agent/slack-message-drafts/SKILL.md` instead: a new subject is one draft with a formatted header on top and the thread message below, names as hyperlinks, long lists grouped under short bold labels.

Turn a raw opportunity or news item into a properly formatted Slack draft in the own DM of [YOUR_FIRST_NAME], then give direct links so [YOUR_FIRST_NAME] can post it to the right channels.

## Settings

Fill in later. Until a line is filled, use the default after it.

- Workspace address: [SLACK_WORKSPACE_URL] (for example https://yourteam.slack.com). Default: ask once, or read it from a channel link the Slack connector returns.
- Default main channel for announcements: [SLACK_CHANNEL_FOR_ANNOUNCEMENTS].
- Main channels by type and the topic channels: `references/channel-map.md`, filled from [SLACK_CHANNEL_FOR_FUNDING], [SLACK_CHANNEL_FOR_JOBS], [SLACK_CHANNEL_FOR_EVENTS], [SLACK_CHANNEL_FOR_NEWS] and [SLACK_TOPIC_CHANNELS]. Any unfilled type goes to the default main channel, with no topic channel.
- What the community is about, for the "does it fit" check: [COMMUNITY_SCOPE].
- The community's own posting guidelines, if they exist: [POSTING_GUIDELINES_LINK]. Default: the condensed rules in `references/posting-guidelines.md`.

## Why this exists

Pasting markdown from chat into Slack renders badly (literal asterisks and brackets). The fix is to never hand over text to copy as the only option. Always create the post inside Slack with `slack_send_message_draft`, which renders bold, bullets, mentions, and links correctly.

Messages posted through the Slack tools carry a "sent with Claude" label. Community posts should not carry it. So the agent never posts to a channel. It drafts in the own DM of [YOUR_FIRST_NAME], and [YOUR_FIRST_NAME] sends it from Slack after approving it.

## Inputs

[YOUR_FIRST_NAME] will usually paste one or more of these. Ask only for what's missing and essential.

Required:
- The source content (pasted text, a link, or both)
- The canonical link to apply, learn more, or read the source

Nice to have (infer, or ask if it changes routing):
- Type of item: funding, job, fellowship or incubator, competition, board role, event, news, resource, unpaid volunteer ask
- Deadline
- Who leads it (to tag them if they're in the workspace)
- Location and compensation (jobs only, per guidelines)
- The connection of [YOUR_FIRST_NAME] to the organization (optional, the guidelines like it)

## Workflow

Follow these steps in order.

### 1. Classify and route

Decide the item type, then pick channels from `references/channel-map.md`. Every post gets one **main channel** and usually one **topic channel**. Read the map file before choosing.

If the item is a "New fund alert" (a new fund or grant program launching), tag the fund lead in the body. If the fund has been posted before (search the main channel for its name), use "Grant round open:" instead and flag the repeat to [YOUR_FIRST_NAME].

### 2. Find people to tag

Search the workspace with `slack_search_users` for the fund lead, hiring manager, or director named in the source. If found, use `<@USERID>` in the message. If not found, use their plain name. Never guess a user ID.

### 3. Draft in the house format

Use the format in `references/post-format.md`. Key rules:
- Emoji plus **bold title** on line one
- One short paragraph with the essentials
- Bullets for what they fund, key details, or requirements (use `-` for bullets, never `*`)
- Deadline line with a 📅 emoji if there is one
- Closing ⭐ line with a "here" link
- Only one link preview. Put the main link last so Slack previews that one. Wrap any other links in the body so they don't dominate.
- Single message, never split
- No em dashes anywhere
- Short sentences, skimmable, conversational

Check the draft against `references/posting-guidelines.md` (minimum requirements differ by type).

### 4. Create the DM draft

Find the own user ID of [YOUR_FIRST_NAME] with `slack_search_users` (or the self-lookup of the connector), and create the draft in that DM with `slack_send_message_draft`. This renders exactly as it will post, and once [YOUR_FIRST_NAME] sends it, it carries no Claude label.

If `slack_send_message_draft` returns `draft_already_exists`, ask [YOUR_FIRST_NAME] to send or delete the old DM draft, then retry.

### 5. Hand off with links

Send a review memo right away: a draft is not done until [YOUR_FIRST_NAME] has the memo. Agents cannot read drafts, and a draft can show blank or vanish, so the memo always holds the full post text inline as plain text with no asterisks, ready to paste. The memo also gives:
- A link to the DM where the draft lives: `[SLACK_WORKSPACE_URL]/archives/<DM_ID>`
- A direct link to the **main channel**: `[SLACK_WORKSPACE_URL]/archives/<MAIN_CHANNEL_ID>`, using the ID from the channel map
- A direct link to the **topic channel**, if any: `[SLACK_WORKSPACE_URL]/archives/<TOPIC_CHANNEL_ID>`
- Who you tagged and who you couldn't find
- Anything you assumed or left out

The flow from there: open the DM, send or copy the draft, post the full message in the main channel, then drop a short pointer in the topic channel. Offer to create the topic-channel pointer as a second DM draft, using the pointer format in `references/post-format.md`, once the main post's permalink exists.

### 6. Failure handling

- `channel_not_found`: re-run `slack_search_channels` and update `references/channel-map.md`.
- Slack Connect channels: [YOUR_FIRST_NAME] can still post there by hand, so the hand-off is the same.

## Do not

- Do not post to any channel or DM with `slack_send_message`. [YOUR_FIRST_NAME] posts, so the message carries no Claude label.
- Do not give markdown with asterisks as the paste text. The plain fallback text in the review memo is required.
- Do not use `*` for bullets or single `*` for bold (use `-` and `**`).
- Do not include more than one link preview.
- Do not fabricate user IDs, channel IDs, or links.
- Do not use em dashes.
