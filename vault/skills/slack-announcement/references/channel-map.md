# Channel map (the Slack of [YOUR_ORG])

Fill this in once: run `slack_search_channels` for each channel name below, write its ID in the table, and put the date here: {date verified}. If a post fails with `channel_not_found`, re-run `slack_search_channels` and update this file.

## Main channels (post the full message here)

| Item type | Main channel | ID |
|---|---|---|
| New fund, grant program, funding application, request for proposals | [SLACK_CHANNEL_FOR_FUNDING] | {fill in} |
| Job, fellowship, incubator, competition, board role (paid or career-relevant) | [SLACK_CHANNEL_FOR_JOBS] | {fill in} |
| Unpaid volunteer ask, request for participants, survey | {a help-requests channel, or the default} | {fill in} |
| Event, conference, workshop, deadline for an event | [SLACK_CHANNEL_FOR_EVENTS] | {fill in} |
| News, launches, reports, papers, newsletters | [SLACK_CHANNEL_FOR_NEWS] | {fill in} |
| Tools, datasets, resources | {a resources channel, or the default} | {fill in} |
| Official announcements of [YOUR_ORG] only | [SLACK_CHANNEL_FOR_ANNOUNCEMENTS] | {fill in} |

A row left unfilled falls back to [SLACK_CHANNEL_FOR_ANNOUNCEMENTS].

Funding items: also cross-post a pointer to the news channel when it's a brand new fund launching. Skip that for routine grant rounds.

## Topic channels (cross-post a short pointer here)

Pick the single best fit. If nothing fits, skip the topic channel.

The list: [SLACK_TOPIC_CHANNELS]. Write it as "topic: #channel", one per line, then add the IDs below.

| Topic | Channel | ID |
|---|---|---|
| {for example: policy, regulation, government} | {#t-policy} | {fill in} |
| {for example: research papers and methods} | {#t-research} | {fill in} |

## Example routings (Example, replace with real ones)

- A university launches a research fund → main funding channel, topic channel for that research area
- A brand new foundation fund → main funding channel, pointer in the news channel
- A machine learning job at a partner organization → main jobs channel, topic channel for its field
- A government consultation open for comment → main news channel, policy topic channel

## People

- [YOUR_FIRST_NAME] (self, for DM drafts): {user ID, from `slack_search_users`}
- {People who are often tagged, with their user ID, for example a fund lead or a partner director}

Always confirm with `slack_search_users` before tagging anyone not listed here.
